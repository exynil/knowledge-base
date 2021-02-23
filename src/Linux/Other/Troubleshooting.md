# Решение проблем


## Jupyter Notebook

### Ошибка при чтении больших файлов

<span style="color:#bf616a">Вывод ошибки</span>

~~~~
IOPub data rate exceeded.
The notebook server will temporarily stop sending output
to the client in order to avoid crashing it.
To change this limit, set the config variable
`--NotebookApp.iopub_data_rate_limit`.

Current values:
NotebookApp.iopub_data_rate_limit=1000000.0 (bytes/sec)
NotebookApp.rate_limit_window=3.0 (secs)
~~~~

Увеличить в настройках максимальный размер выходного потока `NotebookApp.iopub_data_rate_limit`

## Polybar

### В polybar не работают модули wlan, network-speed-down и network-speed-ip

Установить правильный интерфейс беспроводной сети в настройке модуля

~~~~
ip link
~~~~


## Flameshot

### Не запускается flameshot gui

Необходимо запускать X через dbus-launch

~~~~
exec dbus-launch i3
~~~~


## PyCharm

### Серое окно

Экспортировать переменную в окружение

~~~~
export _JAVA_AWT_WM_NONREPARENTING=1
~~~~

## Разное

### Пропадает звук после воспроизведение аудио

Установить пакет pulseaudio-alsa

~~~~
pacman -S pulseaudio-alsa
~~~~

### Тиринг

Включить опцию "TearFree" в /etc/X11/xorg.conf.d/20-intel.conf

~~~~
Section "Device"
    Identifier "Intel"
    Driver "intel"
    Option "TearFree" "true"
EndSection
~~~~