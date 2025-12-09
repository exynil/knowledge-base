## Rclone

~~~~bash
sudo apt install rclone -y
~~~~

~~~~bash
rclone config
~~~~

1. n → New remote.
2. Введи имя, например: mygdrive
3. Тип хранилища — выбери drive
4. Client ID/Secret — можешь просто нажать Enter
5. Scope — выбери 3 (drive.file)
6. Service account file — Enter
7. Edit advanced config — n
8. Auto config — y (или n, если на сервере без браузера, тогда будет инструкция с кодом)
9. Configure this as a Shared Drive (Team Drive)? - n