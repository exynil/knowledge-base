# Общий доступ через ftp

1. Необходимые пакеты: `vsftpd`

2. Открываем доступ локальным пользователя: `/etc/vsftpd.conf`

~~~~
anonymous_enable=NO
local_enable=YES
write_enable=YES
local_umask=022
dirmessage_enable=YES
xferlog_enable=YES
connect_from_port_20=YES
ascii_upload_enable=YES
ascii_download_enable=YES
ftpd_banner=Welcome to My FTP.
chroot_local_user=YES
allow_writeable_chroot=YES
listen=YES
pam_service_name=vsftpd
userlist_deny=NO
userlist_file=/etc/vsftpd/list_user_ftp
local_root=/media/hdd/ftp
pasv_min_port=50000
pasv_max_port=50088
seccomp_sandbox=NO
~~~~

3. Создаём группу
~~~~
groupadd ftpgroup
~~~~

4. Создаём пользователя
~~~~
useradd -G ftpgroup ftpuser
~~~~

5. Устанавливаем пароль
~~~~
passwd ftpuser
~~~~

6. Создаём папку
~~~~
mkdir -p /media/hdd/ftp
~~~~

7. Изменяем владельца
~~~~
chown -R root:ftpgroup /media/hdd/ftp
~~~~

8. Изменяем доступ к папке
~~~~
chmod 770 /media/hdd/ftp
~~~~

9. Запускаем сервис
~~~~
systemctl start vsftpd.service
~~~~

10. Подключаемся на другом устройстве


## `VSFTPD` для анониманым пользователей

1. Конфигурация `vsftpd`
~~~~
anonymous_enable=YES
local_enable=YES
write_enable=YES
local_umask=022
anon_upload_enable=YES
anon_mkdir_write_enable=YES
anon_root=/media/ftp
no_anon_password=YES
allow_writeable_chroot=YES
dirmessage_enable=YES
xferlog_enable=YES
connect_from_port_20=YES
chroot_local_user=YES
listen=YES
pam_service_name=vsftpd
userlist_deny=NO
pasv_min_port=50000
pasv_max_port=50088
seccomp_sandbox=NO
~~~~

2. Создать папку
~~~~
mkdir /media/ftp
~~~~

3. Изменить права
~~~~
chmod -R 775 /media/ftp
~~~~

4. Изменить владельца
~~~~
chown -R nobody:nogroup /media/ftp
~~~~


#ftp #vsftpd