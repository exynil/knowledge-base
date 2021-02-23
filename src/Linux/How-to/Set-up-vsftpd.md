# Общий доступ через ftp

1. Необходимые пакеты: `vsftpd`

2. Открываем доступ локальным пользователя: /etc/vsftpd.conf

~~~~
local_enable=YES
~~~~

3. Открываем возможность редактирвоания: /etc/vsftpd.conf

~~~~
write_enable=YES
~~~~

3. Отключаем песочницу: /etc/vsftpd.conf

~~~~
seccomp_sandbox=NO
~~~~

4. Запускаем сервис
~~~~
$ systemctl start vsftpd.service
~~~~

4. Подключаемся на другом устройстве

### хештеги:  #ftp #vsftpd