# ffmpeg

## Конвертация видео в gif
~~~~
ffmpeg -i test.mp4. test.gif
~~~~

## Обрезка видео

~~~~
$ ffmpeg -ss 00:00:00 -i input.mp4 -to 00:02:00 -c copy output.mp4
~~~~

## Конвертация в mp3
~~~~
ffmpeg -i input.wav -codec:a libmp3lame -qscale:a 2 output.mp3
~~~~

### хештеги:  #ffmpeg