# Гибридная графика

## Система
LAPTOP: `DELL G5 5587`
GPU: `NVIDIA GeForce GTX 1060 Mobile `
GPU: `Intel UHD Graphics 630`
OS: `ArchLinux`
WM: `Bspwm`

## Зачем это всё

Здесь собраны данные по настройке гибридной графики, успешные варианты настройки xorg, результаты экспериметов и другая полезная информация.

## Свободные драйвера

1. Необходимые пакеты: `xf86-video-intel` `xf86-video-nouveau`

### Вариант 1

2. Конфигурационный файл `xorg.conf`

~~~~
Section "Device"
	Identifier "Intel"
	Driver "intel"
	BusID "PCI:0:2:0"
	Option "TearFree" "true"
EndSection

Section "Device"
	Identifier "Nvidia"
	Driver "nouveau"
	BusID "PCI:1:0:0"
EndSection
~~~~

### Результат
Тиринг: только на внешнем мониторе
Встроенный монитор: Работает
Внешний монитора: Работает

## Несвободные драйвера

1. Необходимые пакеты: `xf86-video-intel` `nvidia` `lib32-nvidia-utils` `nvidia-utils` `nvidia-settings`

### Варинат 1

2. Конфигурационный файл `xorg.conf`

~~~~
Section "Device"
	Identifier "Card0"
	Driver "intel"
	BusID "PCI:0:2:0"
	Option "TearFree" "true"
EndSection

Section "Device"
	Identifier "Card1"
	Driver "nvidia"
	BusID "PCI:1:0:0"
	VendorName "NVIDIA Corporation"
	Option "NoLogo" "true"
EndSection

Section "Monitor"
	Identifier "Monitor0"
	Option "DPMS" "true"
EndSection

Section "ServerFlags"
	Option "StandbyTime" "4"
	Option "SuspendTime" "5"
	Option "OffTime" "5"
EndSection

Section "ServerLayout"
	Identifier "ServerLayout0"
EndSection

Section "InputClass"
	Identifier "system-keyboard"
	MatchIsKeyboard "on"
	Option "XkbLayout" "us,ru"
	Option "XkbOptions" "grp:win_space_toggle"
EndSection

Section "InputClass"
	Identifier "touchpad"
	Driver "libinput"
	MatchIsTouchpad "on"
	Option "Tapping" "on"
	Option "TappingDrag" "on"
	Option "AccelSpeed" "0.3"
	Option "AccelProfile" "adaptive"
	Option "ScrollMethod" "twofinger"
	Option "MiddleEmulation" "on"
	Option "DisableWhileTyping" "on"
	Option "TappingButtonMap" "lrm"
EndSection
~~~~

### Результат
Тиринг: нету
Встроенный монитор: Работает
Внешний монитора: Работает
Nvidia: Не работает

### Варинат 2

~~~~
Section "ServerLayout"
    Identifier     "Layout0"
    Screen      0  "Screen0"
    InputDevice    "Keyboard0" "CoreKeyboard"
    InputDevice    "Mouse0" "CorePointer"
EndSection

Section "Files"
EndSection

Section "InputDevice"
    # generated from default
    Identifier     "Mouse0"
    Driver         "mouse"
    Option         "Protocol" "auto"
    Option         "Device" "/dev/psaux"
    Option         "Emulate3Buttons" "no"
    Option         "ZAxisMapping" "4 5"
EndSection

Section "InputDevice"
    # generated from default
    Identifier     "Keyboard0"
    Driver         "kbd"
EndSection

Section "Monitor"
    Identifier     "Monitor0"
    VendorName     "Unknown"
    ModelName      "Unknown"
    Option         "DPMS"
EndSection

Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
EndSection

Section "Screen"
    Identifier     "Screen0"
    Device         "Device0"
    Monitor        "Monitor0"
    DefaultDepth    24
    SubSection     "Display"
        Depth       24
    EndSubSection
EndSection
~~~~

Добавить в автозагрузку
~~~~
nvidia-settings --assign CurrentMetaMode="nvidia-auto-select +0+0 { ForceFullCompositionPipeline = On }"
~~~~

### Результат
Тиринг: нету
Встроенный монитор: Не работает
Внешний монитора: Работает
Nvidia: Работает