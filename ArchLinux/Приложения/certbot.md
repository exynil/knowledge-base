### Certbot

#### Установка
~~~~bash
sudo apt update
sudo apt install certbot python3-certbot-nginx -y
~~~~

#### Получение сертификатов
~~~~bash
sudo certbot --nginx -d exynil.net
~~~~

#### Получение установленных сертификатов
~~~~bash
sudo certbot certificates
~~~~