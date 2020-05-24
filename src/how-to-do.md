# Как сделать 

`OS: Arch Linux`

`WM: i3`

`Terminal: urxvt`

## Как сделать просмотр видео из YouTube в плавающем окне


1. Необходимые пакеты: `mpv`, `youtube-dl`, `xdotool`, `xclip`

2. Настраиваем оконный менеджер `~/.config/i3/config`

- Привязываем выполнение команды к горячим клавишам

```
bindsym $mod+Shift+y exec sleep 0.5 && xdotool key "ctrl+l" && xdotool key "ctrl+c" && mpv $(xclip -o)

```

- Делаем mpv плавающим окном

```
for_window [class="mpv"] floating enable

```

3. Настраиваем mpv `~/.config/mpv/mpv.conf`

```
window-scale=0.4
loop
ytdl-format=bestvideo[height<=?720]+bestaudio/best

```

`window-scale=0.4` - размер окна проигрывателя

`loop` - повторное воспроизведение

`ytdl-format=bestvideo[height<=?720]+bestaudio/best` - качество видео

### Использование

1. Открываем видео на YouTube

2. Нажимаем установленные комбинации клавиш


## Как сделать выпадающий терминал

Настраиваем оконный менеджер `~/.config/i3/config`

- Добавляем запуск терминала с именем `dropdown` в автозагрузку

```
exec --no-startup-id sleep 2 && $TERMINAL -name dropdown

```

- Делаем все окна с именем `dropdown` плавающими

```
for_window [instance="dropdown"] floating enable

```

- Устанавливаем размер окнам с именем `dropdown`

```
for_window [instance="dropdown"] resize set 800 500

```

- Перемещаем окна с именем `dropdown` в `scratchpad`

```
for_window [instance="dropdown"] move scratchpad

```

- Привязываем выполнение команды к горячим клавишам

```
bindsym $mod+z [instance="dropdown"] scratchpad show; [instance="dropdown"] move position center

```
