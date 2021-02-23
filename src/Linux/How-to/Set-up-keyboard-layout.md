# Переключение раскладки

## Инструкция

1. Создаем конфигурационный файл для клавиатуры

~~~~
# touch /etc/X11/xorg.conf.d/40-keyboard.conf
~~~~

~~~~
Section "InputClass"
    Identifier "system-keyboard"
    MatchIsKeyboard "on"
    Option "XkbLayout" "us,ru"
    Option "XkbOptions" "grp:win_space_toggle"
EndSectio
~~~~

### хештеги:  #клавиатура #раскладка