# Проблемы

#### xset r rate не работает из автозагрузки

Добавить задержку

```
sleep 5 && xset r rate 350 62

```

#### В polybar не работают модули wlan, network-speed-down и network-speed-ip

Установить правильный интерфейс беспроводной сети в настройке модуля

```
ip link

```

#### Пропадает звук после воспроизведение аудио

Установить пакет pulseaudio-alsa

```
pacman -S pulseaudio-alsa

```

#### Тиринг

Включить опцию "TearFree" в /etc/X11/xorg.conf.d/20-intel.conf

```
Section "Device"
    Identifier "Intel"
    Driver "intel"
    Option "TearFree" "true"
EndSection

```

#### Не запускается flameshot gui

Необходимо запускать X через dbus-launch

```
exec dbus-launch i3

```
