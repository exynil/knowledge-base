# Команды

## youtube-dl

1. Просмотр возможных вариантов для скачивания

```
youtube-dl -F [url]

```

2. Скачивание определенного формата

```
youtube-dl -f 140 [url]

```

3. Извлечение аудио в формате `mp3`

```
youtube-dl --output "%(title)s.%(ext)s" --extract-audio --audio-format mp3 [url]

```

## xrandr 
Вывод провайдеров

```
xrandr --listproviders

```

## ffmpeg

Обрезка видео

```
ffmpeg -ss 00:00:00 -i input.mp4 -to 00:02:00 -c copy output.mp4

```
## Остальное

Вывод UUID разделов

```
blkid

```
Изменение владельца файла или каталога

```
chown -R $USER

```
Удаление каталога или файла

```
rm file.txt

```

Информация о дисках и разделах

```
fdisk -l

```

Установка фонового изображения

```
feh --bg-scale ~/Pictures/Wallpapers/001.jpg

```

Монтирование раздела

```
mount /dev/sda1 /mnt/storage

```

Календарь

```
cal

```

Объем свободного пространства на дисках

```
df

```

Объем свободного пространства в памяти

```
free

```

Полная очистка кеша Pacman

```
pacman -Scc

```

Список устройств

```
xinput list

```

Регистрация нажатий клавиш

```
xev

```
Генерация файла настроек xorg на основе текущих

```
X :2 -configure

```
Запуск команды с повторением через 1 секунду

```
watch -n1 "date '+%D%n%T'"

```

Поиск по всем мануалам установленных программ

```
apropos compress

```

Поиск файла

```
find / -type f -name "20-intel.conf"

```
