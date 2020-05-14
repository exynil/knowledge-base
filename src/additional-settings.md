# Дополнительные настройки

### Переключение раскладки

Добавить в файл ~/.profile

```
setxkbmap -option grp:alt_shift_toggle us,ru &

```

### Монтирование жесткого диска

1. Определяем UUID и файловую систему диска.

```
blkid

```

2. Добавляем новую запись в таблицу fstab

```
UUID=fbde5f72-0f38-4847-adcf-4ccc502edca2 /home/max/hdd ext4

```

### Временное монтирование диска до перезагрузки

```
mount /dev/[имя_раздела] /[путь_до_папки]/[имя_папки]

```

### Авто включение Numlock

1. Добавить **numlockx on** в автозагрузку


### Изменение размера шрифта терминала rxvt-unicode на лету

1. Устанавливаем **urxvt-perls**

```
yay -S urxvt-perls

```

2. Устанавливаем **urxvt-resize-font-git**

```
yay -S urxvt-resize-font-git

```

3. Добавляем настройки в ~/.Xresources

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

1. Установка задержки

```
xset r rate 350 62

```
2. Просмотр установленной конфигурации

```
xset -q

```

### Polybar на всех мониторах

1. Добавить строку в модуль **bar**

```
monitor = ${env:MONITOR:}

```

2. Запускать Polybar следующими командами

```
if type "xrandr"; then
    for m in $(xrandr --query | grep " connected" | cut -d" " -f1); do
        MONITOR=$m polybar --reload example &
    done
else
    polybar --reload example &
fi

```


