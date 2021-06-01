# git


## Первоначальная настройка
~~~~
$ git config --global user.name "Maxim Kim"
$ git config --global user.email exynil@gmail.com
~~~~

## Команды

Список локальных веток
~~~~
$ git branch
~~~~

Список удаленных веток
~~~~
$ git branch -r
~~~~

Список всех веток
~~~~
$ git branch -a
~~~~

Добавить все изменения
~~~~
$ git add .
~~~~

Добавить коммит
~~~~
$ git commit -m "added index.html"
~~~~

Отправка на удаленный репозиторий
~~~~
$ git push origin master
~~~~

Скачать изменения с удаленного репозитория
~~~~
$ git pull
~~~~


## Изменение ссылки https на ssh

1. Просмотр текущей ссылки
~~~~
git remote -v
~~~~

2. Изменение ссылки
~~~~
$ git remote set-url origin git@github.com:exynil/example.git
~~~~

## Доп. команды

Полный список неотслеживаемых файлов
~~~~
$ git status -u
~~~~



## Ветки

Создание ветки
~~~~
git branch <branchname>
~~~~

Переключиться на ветку
~~~~
git checkout <branchname>
~~~~

Скачать определенную ветку
~~~~
$ git clone -b <branchname> <remote-repo-url>
~~~~


### хештеги: #git #система_контроля_версий