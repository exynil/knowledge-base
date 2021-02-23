# dotfiles

## Подготовка

1. Необходимые пакеты: `git`

2. Создаем репозиторий `dotfiles`

3. Клонируем куда нибудь

4. Переходим в каталог репозитория

Предствим что мы хотим управлять конфигурацией `git` и `i3`. За их настройки у нас отвечают два файла:
`~/.gitconfig`
`~/.config/i3/config`

5. В каталоге нашего репозитория создаем папки `git` и `i3`

Эти папки должны содержать файлы настроек `git`  и `i3`. Распологаем их в тех же папках и по тому же пути по которому они распологаются относительно домашней директории.

~~~~
dotfiles
├── i3
│   └── .config
│       └── i3
│           └── config
└── git
    └── .gitconfig
~~~~

6. Создайте скрипт `install` в корне репозитория
~~~~
#!/bin/bash

# все файлы в подпапках
mapfile -t files < <(find ./*/ -type f)

for file in "${files[@]#*/}"; do
    # создание папок в домашнем каталоге
    mkdir -p "$HOME/$(dirname "${file#*/}")"

    # создание ссылки с перезаписью существующего файла
    ln -sf "$PWD/$file" "$HOME/${file#*/}"
done
~~~~

7. Теперь нам необходимо запустить этот скрипт.
~~~~
$ ./install
~~~~
 
Этот скрипт создасть симлинки в домашней папке на конфиги в папках нашего репозитория.
Теперь всё работает как раньше, только настройки всех наших программ лежат в одной папке. Осталось загрузить все настройки в облако.

## Развёртка на новой системе

1. Клонируем куда нибудь

2. Устанавливаем симлинки

~~~~
$ ./install
~~~~

[Пример](https://github.com/exynil/dotfiles)

### хештеги:  #бэкап #dotfiles