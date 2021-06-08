# youtube-dl

## Скачивание максимального качества видео и аудио + объединение в формат mp4
~~~~
$ youtube-dl -f 'bestvideo+bestaudio/bestvideo+bestaudio' --merge-output-format mp4 [url]
~~~~


## Загрузка видео

1. Смотрим возможные варианты для скачивания

~~~~
$ youtube-dl -F [url]
~~~~

2. Скачиваем выбранный формат

~~~~
$ youtube-dl -f 140 [url]
~~~~

## Загрузка плейлиста
~~~~
$ youtube-dl -i -f mp4 --yes-playlist [url]
~~~~

## Загрузка аудио в формате mp3

~~~~
$ youtube-dl --output "%(title)s.%(ext)s" --extract-audio --audio-format mp3 [url]
~~~~

### хештеги: #youtube-dl  #youtube 