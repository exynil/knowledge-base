# Синхронизация файлов

## Синхронизация локальных каталогов

```
rsync -av --delete [источник] [приемник]

```

```
rsync -av --delete ~/Pictures /media/flash-drive/backup

```

`-a` - архивирование

`-v` - подробный вывод

`-d` - удаление файлов отсутствующий в исходной папке

## Синхронизация по сети

```
rsync -av --delete --rsh=ssh [источник] [удаленный_узел]:[приемник]

```

```
rsync -av --delete --rsh=ssh ~/Pictures alex@alex-pc:~/backup

```
