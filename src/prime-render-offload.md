# PRIME Render Offload

1. Удаляем драйвер **videо-hybrid-intel-nvidia-xxx.xx-bumlblebee**

2. Устанавливаем драйвер **video-nvidia-xxx.xx**

3. Удаляем старый конфиг 

```
sudo rm /etc/X11/xorg.conf.d/90-mhwd.conf

```
4. Создаем конфиг 10-nvidia.conf

```
sudo nano /etc/X11/xorg.conf.d/10-nvidia.conf

```

Команда для опредеения BusID

```
lspci | grep -E "VGA|3D"

```

Содержимое конфига 10-nvidia.conf

```
Section "ServerLayout"
	Identifier     "Layout0"
    Option         "AllowNVIDIAGPUScreens"
    Screen      0  "iGPU" 0 0
EndSection

Section "Device"
    Identifier     "iGPU"
    Driver         "modesetting"
    BusID          "PCI:0:2:0"
EndSection

Section "Device"
    Identifier     "dGPU"
    Driver         "nvidia"
    BusID          "PCI:1:0:0"
EndSection

Section "Screen"
    Identifier     "iGPU"
    Device         "iGPU"
    DefaultDepth    24
    SubSection     "Display"
		Viewport    0 0
    EndSubSection
EndSection

Section "OutputClass"
    Identifier "iGPU"
    MatchDriver "i915"
    Driver "modesetting"
EndSection

Section "OutputClass"
    Identifier "dGPU"
    MatchDriver "nvidia-drm"
    Driver "nvidia"
    Option "AllowEmptyInitialConfiguration"
    Option "PrimaryGPU" "yes"
    ModulePath "/usr/lib/nvidia/xorg"
    ModulePath "/usr/lib/xorg/modules"
EndSection

```

5. Удаляем остатки конфигов

```
ls /etc/modprobe.d/mhwd*

```

6. Перезагружаемся

7. Устанавливаем PRIME

8. Устанавливаем xorg-xrandr

9. Проверяем провайдеры

```
xrandr --listproviders

```

> Вывод
> ```
> Providers: number : 2
> Provider 0: id: 0x49 cap: 0xf, Source Output, Sink Output, Source Offload, Sink Offload crtcs: 3 outputs: 7 associated providers: 0 name:modesetting
> Provider 1: id: 0x245 cap: 0x0 crtcs: 0 outputs: 0 associated providers: 0 name:NVIDIA-G0
>
> ```

10. Проверяем графические карты

```
inxi -G

```

> Вывод
> ```
> Providers: number : 2
> Provider 0: id: 0x49 cap: 0xf, Source Output, Sink Output, Source Offload, Sink Offload crtcs: 3 outputs: 7 associated providers: 0 name:modesetting
> Provider 1: id: 0x245 cap: 0x0 crtcs: 0 outputs: 0 associated providers: 0 name:NVIDIA-G0
> 
> ```
