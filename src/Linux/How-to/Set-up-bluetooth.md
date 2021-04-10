# Bluetooth


1. Необходимые пакеты:
- GUI: `blueman` 
- CLI: `bluez`, `bluez-utils`
- Модуль для наушников: `pulseaudio-modules-bt`

2. Загружаем универсальный драйвер
~~~~
# modprobe btusb
~~~~

3. Включаем службы
~~~~
systemctl enable bluetooth.service
~~~~

3. Добавляем пользователя в группу
~~~~
gpasswd -a max lp
~~~~

4. Добавляем blueman-applet в автозагрузку (Если вы установили `blueman`)

5. Перезагружаемся


## Подключение через bluetoothctl

~~~~
# bluetoothctl
~~~~

Начасить поиск устройв
~~~~
[bluetooth]# scan on
~~~~

Добавить в список доверенных устройст
~~~~
[bluetooth]# trust xx:xx:xx:xx:xx
~~~~

Сопряжение
~~~~
[bluetooth]# pair xx:xx:xx:xx:xx
~~~~

Подсоединиться
~~~~
[bluetooth]# connect xx:xx:xx:xx:xx
~~~~


### хештеги: #bluetooth 