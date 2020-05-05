# Ошибки

#### dmenu не отображает программу

Удалить кэш

```
sudo rm ~/.cache/dmenu-recent/all

```

#### xset r rate не работает с автозагрузки

Добавить задержку

```
sleep 5 && xset r rate 250 40

```

#### polybar не отображает модули wlan, network-speed-down и network-speed-ip

Установить правильный интерфейс беспроводной сети в настройке модуля

```
ip link

```

#### Пропадает звук после воспроизведение аудио

Установить пакет pulseaudio-alsa

```
pacman -S pulseaudio-alsa

```

#### Тиринги на видео

Включаить опцию "TearFree" в /etc/X11/xorg.conf.d/20-intel.conf

```
Section "Device"
        Identifier  "Intel Graphics"
        Driver      "intel"
        Option      "DRI" "2"             # DRI3 is now default 
        Option      "TearFree" "true"     # Tearing
EndSection

```

#### Не запускается flameshot gui

Необходимо запускать X через dbus-launch

```
exec dbus-launch i3

```
