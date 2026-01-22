1.
https://hub.docker.com/repository/docker/shaw927/custom-nginx/tags

2.
<img width="1499" height="558" alt="image" src="https://github.com/user-attachments/assets/e0c345eb-cfc8-46b2-9053-f6470c71df83" />

3.
Ну я так понимаю после подключение через docker attach, мои сигнал прерывания проксируются внутрь контейнера и SIGINT отправился nginx и он остановился, после этого у контейнера больше нет работающего процесса, а он в таком случае останавливается

Ну проблема в том что поменяли порт работы nginx, но не поменяли прокидывание портов на хосте и он все еще стучится на 80

<img width="957" height="843" alt="image" src="https://github.com/user-attachments/assets/18dd70ca-c715-42e1-86d7-5f37d89fd8b6" />

4.

<img width="829" height="509" alt="image" src="https://github.com/user-attachments/assets/00507c85-d5f2-4746-94ea-808e3a4c70c0" />

<img width="835" height="498" alt="image" src="https://github.com/user-attachments/assets/2f0b51f2-9ad9-4336-bdcd-f7f9946664dd" />

5.
Запущен был compose.yaml так как он более приоритетный чем docker-compose.yaml
После удаление compose.yaml контейнер который был описан в нем был потерян а контейнер который был включен в другой композе осиротел и что удалить все контейнеры которые больше не описанны в манифестах надо использовать команду
docker compose down --remove-orphans

<img width="1499" height="838" alt="image" src="https://github.com/user-attachments/assets/17f498ef-2204-4f0e-be84-60a31da858e1" />

<img width="1496" height="705" alt="image" src="https://github.com/user-attachments/assets/376527e1-dc45-4f06-b3b9-5e52d9173c37" />
