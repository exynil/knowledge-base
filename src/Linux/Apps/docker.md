# docker

## Подготовка

Добавление пользователя в группу
~~~~
# gpasswd -a max docker
~~~~

Запуск службы
~~~~
# systemctl start docker
~~~~

## Команды

Просмотр контейнеров
~~~~
$ docker images
~~~~

Вход в контейнер
~~~~
$ docker exec -it <container_id> bash
~~~~

Список запущенных контейнеров
~~~~
$ docker ps -a -q
~~~~

Удаление всех ресурсов не связанных с контейнерами
~~~~
$ docker system prune
~~~~

Удаление всеx контейнеров и неиспользуемые образы
~~~~
$ docker system prune -a
~~~~

Удалление всех контейнеров
~~~~
$ docker rm $(docker container ls -aq)
~~~~

Информация
~~~~
$ docker info
~~~~

### хештеги:  #docker