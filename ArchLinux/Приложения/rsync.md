## Синхронизация локальных каталогов

~~~~bash
rsync -av --delete [источник] [приемник]
~~~~

~~~~bash
rsync -av --delete ~/Pictures /media/flash-drive/backup
~~~~

`-a` - архивирование

`-v` - подробный вывод

`--delete` - удаление файлов отсутствующий в исходной папке

`--progress` - показывать прогресс


## Синхронизация по сети

~~~~bash
rsync -av --delete --rsh=ssh [источник] [удаленный_узел]:[приемник]
~~~~

### Из локального на удаленный сервер
~~~~bash
rsync -av --delete --rsh=ssh ~/Pictures alex@alex-pc:~/backup
~~~~

### Из удаленного сервера на локальный
~~~~bash
rsync -av --delete --rsh=ssh itp@dms-dev.keu.kz:/opt/itp ~/backup/itp
~~~~

### Отправка файлов в защищенные папки
~~~~bash
rsync -av --delete --progress ./build/ student@yandex.kz:/usr/share/nginx/html --rsync-path="sudo rsync"
~~~~

#файлы #синхронизация #бэкап #rsync