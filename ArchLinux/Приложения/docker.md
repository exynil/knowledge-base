Добавление пользователя в группу
~~~~
gpasswd -a max docker
~~~~

Запуск службы
~~~~
systemctl start docker
~~~~

## Команды

Просмотр контейнеров
~~~~
docker images
~~~~

Вход в контейнер
~~~~
docker exec -it <container_id> bash
~~~~

Список запущенных контейнеров
~~~~
docker ps -a -q
~~~~

Удаление всех ресурсов не связанных с контейнерами
~~~~
docker system prune
~~~~

Удаление всеx контейнеров и неиспользуемые образы
~~~~
docker system prune -a
~~~~

Удалление всех контейнеров
~~~~
docker rm $(docker container ls -aq)
~~~~

Удалление всех томов
~~~~
docker volume rm $(docker volume ls -q)
~~~~

Информация
~~~~
docker info
~~~~

### Как скопировать файлы в контейнер докера?

В контейнер
~~~~
docker cp foo.txt container_id:/foo.txt
~~~~

Из контейнера
~~~~
docker cp container_id:/foo.txt foo.txt
~~~~

#docker