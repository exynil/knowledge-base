# imagemagick

Замена одного черного цвета на белый
~~~~
$ convert wallpaper.png -fuzz 50% -fill white -opaque black result.png
~~~~

Поиск наиболее часто встречающегося цвета
~~~~
$ convert "image.png" -format %c +dither -depth 5  histogram:info: | sort -nr | head -1 | grep -Eo '#[A-F0-9]{6}'
~~~~

Конвертировать все png в jpg
~~~~
$ magick mogrify -format jpg *.png
~~~~

### хештеги:  #imagemagick