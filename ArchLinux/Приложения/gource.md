~~~~
gource -1920x1080 -o - | ffmpeg -y -r 60 -f image2pipe -vcodec ppm -i - -vcodec libx264 -preset ultrafast -pix_fmt yuv420p -crf 1 -threads 0 -bf 0 ~/Videos/gource.mp4
~~~~

### Визуализация двух репозиториев

Структура папок

~~~~
.
├── avatars
├── backend
├── frontend
└── script.sh
~~~~


Скрипт
~~~~bash
gource --output-custom-log backend.txt ./backend
gource --output-custom-log frontend.txt ./frontend

sed -i -r "s#(.+)\|#\1|/BACKEND#" backend.txt
sed -i -r "s#(.+)\|#\1|/FRONTEND#" frontend.txt


cat frontend.txt backend.txt | sort -n > combined.txt


gource combined.txt --user-image-dir ./avatars   -1920x1080 -o - | \
ffmpeg -y -r 60 -f image2pipe \
 -vcodec ppm -i - -vcodec libx264 \
 -preset ultrafast -pix_fmt yuv420p \
 -crf 1 -threads 0 -bf 0 video.mp4
~~~~

#git #gource