## Создание отдельных ssh ключей под разные репизитории

У нас есть два репозитория `test-server` и `test-client`

~~~~
git@github.com:organization/test-server.git
~~~~

~~~~
git@github.com:organization/test-client.git
~~~~

Мы хотим создать для них отдельные ssh ключи и добавить их в Deploy Keys на гитхаб.

1. Создание отдельных ssh ключей для каждого репозитория

~~~~bash
ssh-keygen -t rsa -b 4096 -C "exynil@gmail.com" -f ~/.ssh/id_rsa_test_server
~~~~

~~~~bash
ssh-keygen -t rsa -b 4096 -C "exynil@gmail.com" -f ~/.ssh/id_rsa_test_client
~~~~

2. Настройка конфига `~/.ssh/config`

~~~~
Host github.com-test-server
    Hostname github.com
    IdentityFile=/home/user/.ssh/id_rsa_test_server

Host github.com-test-client-spa
    Hostname github.com
    IdentityFile=/home/user/.ssh/id_rsa_test_client_spa
~~~~

3. Добавление публичных ключей в репозиторий

~~~~
cat ~/.ssh/id_rsa_test_server.pub
~~~~

https://github.com/organization/test-server/settings/keys

4. Клонирование репоизториев

~~~~bash
git clone git@github.com-test-server:organization/test-server.git
~~~~

#ssh