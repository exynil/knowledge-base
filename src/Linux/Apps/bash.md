# bash

## Bash Parameter Expansion

Вывести длину строки
~~~~
$ os="linux"
$ echo ${#os}
5
~~~~

Вывести диапазон строки
~~~~
$ name="maxim"
$ echo ${name:0:3}
max
~~~~

Сделать первую букву заглавной
~~~~
$ name="maxim"
$ echo ${name^}
Maxim
~~~~

Сделать все буквы заглавными
~~~~
$ name="maxim"
$ echo ${name^^}
MAXIM
~~~~

Сделать первую букву прописной
~~~~
$ name="MAXIM"
$ echo ${name,}
mAXIM
~~~~

Сделать все буквы заглавными
~~~~
$ name="MAXIM"
$ echo ${name,,}
maxim
~~~~

Замена текста (только первого совпадения)
~~~~
$ text="My name is Maxim. What is your name?"
$ echo "${text/name/NAME}"
My NAME is Maxim. What is your name?
~~~~

Замена текста (глобально)
~~~~
$ text="My name is Maxim. What is your name?"
$ echo "${text//name/NAME}"
My NAME is Maxim. What is your NAME?
~~~~

Удаление части текста символа точка
~~~~
$ text="My name is Maxim. What is your name?"
$ echo "${text/*./}"
What is your name?
~~~~

Получение имени файла без расширений
~~~~
$ path="home/.config/ranger/rc.conf"
$ echo "${path%.*}"
home/.config/ranger/rc
~~~~

Получение расширения файла
~~~~
$ path="home/.config/ranger/rc.conf"
$ echo "${path##*.}"
conf
~~~~

Получение имени каталога
~~~~
$ path="home/.config/ranger/rc.conf"
$ echo "${path%/*}"
home/.config/ranger
~~~~

Получение имени файла
~~~~
$ path="home/.config/ranger/rc.conf"
$ echo "${path##*/}"
rc.conf
~~~~


### хештеги:  #bash