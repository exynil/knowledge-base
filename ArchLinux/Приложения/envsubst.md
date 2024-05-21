`envsubst` — это утилита из набора инструментов GNU, которая заменяет переменные окружения в текстовом файле на их текущие значения. Она полезна для шаблонизации конфигурационных файлов или других текстовых документов, где необходимо использовать переменные окружения.

### Простейшая замена переменных

Создадим файл `template.txt` с содержимым:
~~~~
Hello, $USER! Your home directory is $HOME.
~~~~

Команда для замены переменных:
~~~~bash
envsubst < template.txt
~~~~

Если текущий пользователь max, а его домашняя директория /home/max, результат будет:
~~~~
Hello, max! Your home directory is /home/max.
~~~~

### Замена переменных окружения в новый файл

Предположим, у нас есть файл `config.template`:
~~~~
DATABASE_HOST=$DB_HOST
DATABASE_PORT=$DB_PORT
~~~~

Перед запуском команды envsubst, определим переменные окружения:

~~~~
export DB_HOST=localhost
export DB_PORT=5432
~~~~

Теперь выполним команду и сохраним результат в `config.conf`:
~~~~bash
envsubst < config.template > config.conf
~~~~

Файл `config.conf` будет содержать:
~~~~bash
DATABASE_HOST=localhost
DATABASE_PORT=5432
~~~~


### Ещё пример
~~~~bash
TEMPLATES=("wg0.conf.template" "wg-client.conf.template")
OUTPUT_DIR="/etc/wireguard/"

# Вынесение подстановки переменных окружения в отдельную переменную
ENV_VARS="$(env | awk -F '=' '{print "${"$1"}"}')"

# Обработка шаблонов
envsubst "$ENV_VARS" <"${TEMPLATES[0]}" >"${OUTPUT_DIR}${TEMPLATES[0]%.template}"
envsubst "$ENV_VARS" <"${TEMPLATES[1]}" >"${OUTPUT_DIR}${TEMPLATES[1]%.template}"
~~~~


#envsubst #env