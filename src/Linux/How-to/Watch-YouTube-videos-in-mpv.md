# Просмотр видео с YouTube в mpv

1. Необходимые пакеты: `mpv`, `youtube-dl`, `xdotool`, `xclip`

2. Настравиваем горячие клавиши: `~/.config/i3/config`

~~~~
bindsym $super+y exec sleep 0.5 && xdotool key "ctrl+l" && xdotool key "ctrl+c" && mpv $(xclip -o) &
~~~~

3. Делаем mpv плавающим окном: `~/.config/i3/config`

~~~~
for_window [class="mpv"] floating enable
~~~~

3. Настраиваем mpv `~/.config/mpv/mpv.conf`

~~~~
window-scale=0.4
loop
ytdl-format=bestvideo[height<=?720]+bestaudio/best
~~~~

`window-scale=0.4` - размер окна проигрывателя

`loop` - повторное воспроизведение

`ytdl-format=bestvideo[height<=?720]+bestaudio/best` - качество видео

## Использование

1. Переходим в браузер

2. Открываем любое видео на YouTube

3. Нажимаем установленные комбинации клавиш

### хештеги:  #youtube #mpv #youtube-dl