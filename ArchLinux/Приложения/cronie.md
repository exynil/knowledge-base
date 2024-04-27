1. Необходимые пакеты: `cronie`

2. Включение службы
~~~~
systemctl enable cronie
~~~~

## Пример

Запуск скрипт каждый рабочий день в 12:00
~~~~
SHELL=/bin/sh

Запускать скрипт test
0 12 * * 1-5 /media/hdd/arch/dotfiles/bin/.local/bin/test
~~~~

Содержимое скрипта
~~~~
#!/bin/bash

export DISPLAY=:0

URL="https://google.com"

# Проверяем доступность ресурса
wget -q --spider "$URL"

if ! wget -q --spider "$URL"; then
    exit 1
fi

# Открываем ссылку в firefox в приватном режиме
firefox --private-window "$URL" &
~~~~


#планирование_задач #cron