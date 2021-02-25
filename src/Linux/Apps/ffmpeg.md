# ffmpeg

## Конвертация видео в gif
~~~~
ffmpeg -i test.mp4. test.gif
~~~~

## Обрезка видео

~~~~
$ ffmpeg -ss 00:00:00 -i input.mp4 -to 00:02:00 -c copy output.mp4
~~~~

### хештеги:  #ffmpeg