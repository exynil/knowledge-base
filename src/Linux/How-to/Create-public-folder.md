# Общая папка

1. Создаем общую папку

~~~~
# mkdir /usr/local/share/music
~~~~

2. Создаем группу

~~~~
# groupadd music
~~~~

3. Создаем пользователя

~~~~
# useradd -m alex
~~~~ 

4. Устанавливаем пароль новому пользователю

~~~~
# passwd alex
~~~~

5. Добавляем пользователя в группу

~~~~
# gpasswd -a alex music5
~~~~

6. Изменяем группу каталога

~~~~
# chown :music /usr/local/share/music
~~~~

7. Изменяем права на каталог

~~~~
# chmod 775 /usr/local/share/music
~~~~

8. Проверяем результат

~~~~
$ ls -ld /usr/local/share/music
~~~~


~~~~
drwxrwxr-r 2 root music 4096 Mar 18 20:36 /usr/local/share/music
~~~~

9. Перезагружаемся

>В действительности здесь наблюдаются две проблемы. Во-первых, маска umask. в этой системе имеет значение 0022, что не позволяет членам группы записывать. в файлы, принадлежащие другим членам группы. Это не проблема, если общий каталог хранит только файлы, но так как в данном каталоге предполагается хранить музыкальные произведения, а музыкальные произведения обычно принято организовывать в иерархии по исполнителям и альбомам, членам группы может понадобиться создавать файлы в каталогах, принадлежащих другим членам. Нам нужно изменить маску umask для пользователей max и alex на 0002.

>Во-вторых, каждый файл и каталог, созданный одним членом группы, будет принадлежать основной группе пользователя, а не группе music. Исправить этот недостаток можно установкой бита setgid на каталог:

~~~~
sudo chmod g+s /usr/local/share/music
~~~~

### хештеги: #общий_доступ