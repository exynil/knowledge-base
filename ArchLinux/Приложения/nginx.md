## Ошибки


### Сбой системного вызова getpwnam
~~~~
getpwnam("nginx") failed
~~~~

Решение:

~~~~bash
sudo useradd -r -s /sbin/nologin nginx
~~~~