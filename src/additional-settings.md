# Дополнительные настройки

### Переключение раскладки

Добавляем следующую строку в автозагрузку

```
setxkbmap -option grp:alt_shift_toggle us,ru &

```

### Автомонтирование жесткого диска

1. Определяем UUID и файловую систему диска.

```
blkid

```

2. Добавляем следующую строку в таблицу `/etc/fstab`

```
UUID=fbde5f72-0f38-4847-adcf-4ccc502edca2 /home/max/hdd ext4

```

### Авто включение Numlock

Необходимые пакеты: `numlockx`

1. Добавляем следующую строку в автозагрузку

```
numlockx on

```

### Изменение размера шрифта терминала rxvt-unicode на лету

Необходимые пакеты: `urxvt-perls`, `urxvt-resize-font-git`

1. Добавляем следующие строки в `~/.Xresources`

```
URxvt.perl-lib: /usr/lib64/urxvt/perl
URxvt.perl-ext-common: default,resize-font
URxvt.keysym.C-KP_Subtract: resize-font:smaller
URxvt.keysym.C-KP_Add: resize-font:bigger

```

### Синхронизация времени с серверами NTP

```
timedatectl set-ntp true

```

### Задержка и частота повтора клавиш

1. Установливаем задержку и частоту

```
xset r rate 350 62

```
2. Проверяем установленные параметры

```
xset -q

```

### Polybar на всех мониторах

1. Добавляем следующую строку в модуль `bar`

```
monitor = ${env:MONITOR:}

```

2. Запускаем Polybar следующими командами

```
if type "xrandr"; then
    for m in $(xrandr --query | grep " connected" | cut -d" " -f1); do
        MONITOR=$m polybar --reload example &
    done
else
    polybar --reload example &
fi

```

### Просмотр видео из YouTube в плавающем окне

Необходимые пакеты: `mpv`, `youtube-dl`, `xdotool`, `xclip`

1. Устанавливаем запуск команды `~/.config/i3/config`

```
bindsym $mod+Shift+y exec sleep 0.5 && xdotool key "ctrl+l" && xdotool key "ctrl+c" && mpv $(xclip -o)

```

2. Установливаем запуск **mpv** в плавающем состоянии `~/.config/i3/config` [опционально]

```
for_window [class="mpv"] floating enable

```

3. Настраиваем размер плеера `~/.config/mpv/mpv.conf` [опционально]

```
window-scale=0.4

```

4. Настраиваем качество видео `~/.config/mpv/mpv.conf` [опционально]

```
ytdl-format=bestvideo[height<=?720]+bestaudio/best

```

Принцип работы:

1. `xdotool key "ctrl+l"` - выделяет URL в адресной строке браузера
2. `xdotool key "ctrl+c"` - копирует выделенный URL в буфер
3. `xclip -o` -передает текст из буфера в параметры `mpv`
