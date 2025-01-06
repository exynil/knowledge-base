## HTTP Basic Authentication

1. Установка необходимых пакетов:

Ubuntu
~~~~bash
apt install apache2-utils
~~~~

Arch
~~~~bash
yay -S apache
~~~~

2. Создание нового файла паролей:

~~~~bash
htpasswd -c /path/to/.htpasswd username
~~~~

или

Добавление пользователя в существующий файл:

~~~~bash
htpasswd /path/to/.htpasswd username
~~~~

3. Настройка nginx:

~~~~
location / {
    auth_basic "Restricted Area";
    auth_basic_user_file /etc/nginx/.htpasswd;
}
~~~~

### Устранение конфликта заголовков Authorization

Если заголовок Authorization, передаваемый от клиента, конфликтует с внутренней авторизацией вашего сайта (например, API или сессиями), вы можете очистить его, добавив настройку `proxy_set_header Authorization ""`.
~~~~
location / {
    auth_basic "Restricted Area";
    auth_basic_user_file /etc/nginx/.htpasswd;
    proxy_set_header Authorization "";
}
~~~~

### Docker compose

Файл паролей можно прокунить через `volumes`

~~~~
  nginx:
    container_name: nginx
    image: nginx:stable-alpine
    ports:
      - "443:443"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
      - ./ssl:/etc/nginx/ssl
      - ./logs:/var/log/nginx
      - .htpasswd:/etc/nginx/.htpasswd:ro
~~~~

#nginx #auth #security