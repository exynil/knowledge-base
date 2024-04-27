## Bash Parameter Expansion

Вывести длину строки
~~~~bash
os="linux"
echo ${#os}
5
~~~~

Вывести диапазон строки
~~~~bash
name="maxim"
echo ${name:0:3}
max
~~~~

Сделать первую букву заглавной
~~~~bash
name="maxim"
echo ${name^}
Maxim
~~~~

Сделать все буквы заглавными
~~~~bash
name="maxim"
echo ${name^^}
MAXIM
~~~~

Сделать первую букву прописной
~~~~bash
name="MAXIM"
echo ${name,}
mAXIM
~~~~

Сделать все буквы заглавными
~~~~bash
name="MAXIM"
echo ${name,,}
maxim
~~~~

Замена текста (только первого совпадения)
~~~~bash
text="My name is Maxim. What is your name?"
echo "${text/name/NAME}"
My NAME is Maxim. What is your name?
~~~~

Замена текста (глобально)
~~~~bash
text="My name is Maxim. What is your name?"
echo "${text//name/NAME}"
My NAME is Maxim. What is your NAME?
~~~~

Удаление части текста символа точка
~~~~bash
text="My name is Maxim. What is your name?"
echo "${text/*./}"
What is your name?
~~~~

Получение имени файла без расширений
~~~~bash
path="home/.config/ranger/rc.conf"
echo "${path%.*}"
home/.config/ranger/rc
~~~~

Получение расширения файла
~~~~bash
path="home/.config/ranger/rc.conf"
echo "${path##*.}"
conf
~~~~

Получение имени каталога
~~~~bash
path="home/.config/ranger/rc.conf"
echo "${path%/*}"
home/.config/ranger
~~~~

Получение имени файла
~~~~bash
path="home/.config/ranger/rc.conf"
echo "${path##*/}"
rc.conf
~~~~


#bash