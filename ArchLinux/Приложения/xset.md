### Получение текущей раскладки
~~~~
xset -q|grep LED| awk '{ print $10 }'
~~~~

#xset