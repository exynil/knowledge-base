## Первоначальная настройка

~~~~bash
git config --global user.name "Maxim Kim"
git config --global user.email exynil@gmail.com
~~~~

## Основные команды

Список локальных веток
~~~~bash
git branch
~~~~

Список удаленных веток
~~~~bash
git branch -r
~~~~

Список всех веток
~~~~bash
git branch -a
~~~~

Добавить все изменения
~~~~bash
git add .
~~~~

Добавить коммит
~~~~bash
git commit -m "added index.html"
~~~~

Отправка на удаленный репозиторий
~~~~bash
git push origin master
~~~~

Скачать изменения с удаленного репозитория
~~~~bash
git pull
~~~~

Полный список неотслеживаемых файлов
~~~~bash
git status -u
~~~~

Сокращенный `git diff`
~~~~bash
git diff --unified=0
~~~~

## Stash

Откладывание кода
~~~~bash
git stash
~~~~

Применение изменений к рабочей копии без удаления из архива
~~~~bash
git stash apply
~~~~

Откладывание кода для не отслеживаемых файлов
~~~~bash
git stash -u
~~~~

## Изменение ссылки https на ssh

1. Просмотр текущей ссылки
~~~~
git remote -v
~~~~

2. Изменение ссылки
~~~~
git remote set-url origin git@github.com:exynil/example.git
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
git clone -b <branchname> <remote-repo-url>
~~~~

## Работа с тэгами

### Добавление тега к уже имеющемумя коммиту

~~~~
git tag -a v0.0.52 c1d6553fbe4d1016a80cd266d5814027c074d0e3
~~~~

~~~~
git push origin --tags
~~~~

## Отмена последнего коммита
~~~~
git reset --soft HEAD~1
~~~~

## Отмена git add
~~~~
git reset
~~~~

## Изменение сообщения последнего коммита
~~~~
git commit --amend
~~~~

---

Если файл, который вы добавили в `.gitignore`, уже находится под контролем версий Git, вам также нужно удалить его из репозитория. Для этого выполните следующую команду в терминале или командной строке:
~~~~
git rm --cached example.txt
~~~~

## Сброс истории коммитов

1. Клонируем
~~~~
git clone https://github.com/USERNAME/REPO_NAME.git
cd REPO_NAME
~~~~
2. Вносим изменения

3. Сбрасываем историю
~~~~
git reset $(git commit-tree HEAD^{tree} -m "Initial commit")
~~~~

4. Добавление изменений и коммит
~~~~
git add .
git commit --amend --no-edit
~~~~
5. Принудительная отправка
~~~~
git push --force
~~~~

## Изменение коммита

git rebase -i abc1234^

edit abc1234 Your old commit message

git add путь/к/файлу

git commit --amend --no-edit

git rebase --continue


## Чтобы посмотреть что было сделано за последние 13 коммитов

git reset --soft HEAD~13

Это "отменит" 13 последних коммитов, оставив все изменения в рабочем дереве, как будто ты их только что внёс, но ещё не закоммитил.

#git