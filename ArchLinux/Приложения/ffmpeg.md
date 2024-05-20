## Конвертация видео в gif
~~~~
ffmpeg -i test.mp4. test.gif
~~~~

## Обрезка видео

~~~~
ffmpeg -ss 00:00:00 -i input.mp4 -to 00:02:00 -c copy output.mp4
~~~~

## Конвертация в mp3
~~~~
ffmpeg -i input.wav -codec:a libmp3lame -qscale:a 2 output.mp3
~~~~

## Обрезка видео и конвертация в аудио для телеграм
~~~~
ffmpeg -i input.mp4 -ss 00:18:06.5 -to 00:18:08.6 -vn -c:a libopus 1.ogg
~~~~


## Обьединение видео без звука и аудио
~~~~
ffmpeg -i input_video.mp4 -i input_audio.opus -c:v copy -c:a aac -strict experimental output.mp4
~~~~

## Убираем черные поля сверху и снизу видео

Воспроизводим видео через команду
~~~~
ffplay -i input.mp4 -vf cropdetect
~~~~

В выводе запомните значение `crop` напирмер: `crop=1904:784:6:148`

Далее запустите команду
~~~~
ffmpeg -i input.mp4 -vf "crop=1904:784:6:148" -c:v libx264 -preset slow -crf 22 -c:a copy output.mp4
~~~~

## Сжатие видео
~~~~
ffmpeg -i input.mp4  -vcodec libx265 -crf 28 output.mp4
~~~~

~~~~
ffmpeg -i input.mp4 -vcodec h264 -acodec mp2 output.mp4
~~~~

#ffmpeg #видео