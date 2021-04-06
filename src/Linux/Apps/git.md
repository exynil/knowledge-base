# git

## Изменение ссылки https на ssh

 1. Просмотр текущей ссылки
 ~~~~
 git remote -v
 ~~~~
 
 2. Изменение ссылки
 ~~~~
 $ git remote set-url origin git@github.com:exynil/example.git
 ~~~~

 3. Полный список неотслеживаемых файлов
 ~~~~
$ git status -u
 ~~~~

 4. Скачать определенную ветку
 ~~~~
$ git clone -b <branchname> <remote-repo-url>
 ~~~~


 ### хештеги: #git #система_контроля_версий