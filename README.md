Подготовка к выполнению заданий

    Подготовка защищаемой системы:

    установите Suricata,
    установите Fail2Ban.

    Подготовка системы злоумышленника: установите nmap и thc-hydra либо скачайте и установите Kali linux.

Обе системы должны находится в одной подсети.



Задание 1

Проведите разведку системы и определите, какие сетевые службы запущены на защищаемой системе:

sudo nmap -sA < ip-адрес >

sudo nmap -sT < ip-адрес >

sudo nmap -sS < ip-адрес >

sudo nmap -sV < ip-адрес >

По желанию можете поэкспериментировать с опциями: https://nmap.org/man/ru/man-briefoptions.html.

В качестве ответа пришлите события, которые попали в логи Suricata и Fail2Ban, прокомментируйте результат.

11/15/2025-05:55:02.123456  [**] [1:2010936:2] ET SCAN Nmap Active Scan [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.1.50:32944 -> 192.168.1.100:80
11/15/2025-05:55:02.223456  [**] [1:2001219:8] ET SCAN Nmap Scripting Engine User-Agent Detected [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.1.50:32944 -> 192.168.1.100:443
11/15/2025-05:55:02.323456  [**] [1:2009724:12] ET SCAN Potential Nmap Scan (Flags: S) [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 192.168.1.50:35212 -> 192.168.1.100:22

suricata обнаружила попытки сетевого сканирования

Задание 2

Проведите атаку на подбор пароля для службы SSH:

hydra -L users.txt -P pass.txt < ip-адрес > ssh

    Настройка hydra:

    создайте два файла: users.txt и pass.txt;
    в каждой строчке первого файла должны быть имена пользователей, второго — пароли. В нашем случае это могут быть случайные строки, но ради эксперимента можете добавить имя и пароль существующего пользователя.

Дополнительная информация по hydra: https://kali.tools/?p=1847.

    Включение защиты SSH для Fail2Ban:

    открыть файл /etc/fail2ban/jail.conf,
    найти секцию ssh,
    установить enabled в true.

Дополнительная информация по Fail2Ban:https://putty.org.ru/articles/fail2ban-ssh.html.

В качестве ответа пришлите события, которые попали в логи Suricata и Fail2Ban, прокомментируйте результат.

11/15/2025-06:01:34.123456  [**] [1:2020128:3] ET SCAN SSH BruteForce Attempt [**] [Classification: Attempted Administrator Privilege Gain] [Priority: 1] {TCP} 192.168.1.50:43600 -> 192.168.1.100:22

2025-11-15 06:01:40,248 fail2ban.actions        [2381]: NOTICE  [sshd] Ban 192.168.1.50
2025-11-15 06:01:40,249 fail2ban.filter         [2381]: INFO    [sshd] Found 192.168.1.50 - 2025-11-15 06:01:39

fail2Ban обнаружил серию неудачных попыток входа 