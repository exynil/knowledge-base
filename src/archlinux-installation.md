# Установка ArchLinux

## Базовая установка

1. Соединение с интернетом

```
wifi-menu

```
2. Проверка интернета

```
ping google.com

```

3. Синхронизация системных часов

```
timedatectl set-ntp true

```

4. Проверка времени

```
timedatectl status

```

5. Просмотр списка устройств

```
lsblk

```

6. Разметка дисков

```
cfdisk /dev/sdb

```
Точка монтирования `/mnt/boot` размер `512МB`, тип раздела `EFI System`, файловая система `vfat`

Точка монтирования `/mnt` размер `более 20GB`, тип раздела `Linux root (x86-64)`, файловая система `ext4`

7. Форматирование загрузочного раздела

```
mkfs.vfat /dev/sdb1

```

8. Форматирование корневого раздела

```
mkfs.ext4 /dev/sdb2

```

9. Монтирование корневого разделов

```
mount /dev/sdb2 /mnt

```

10. Создание папки boot в корневом разделе

```
mkdir /mnt/boot

```

11. Монтирование загрузочного раздела

```
mount /dev/sdb1 /mnt/boot

```

12. Установка пакетов

```
pacstrap /mnt base base-devel linux linux-firmware vim intel-ucode man-db man-pages wpa_supplicant inetutils netctl dhcpcd dialog

```

13. Генерация файла `fstab`

```
genfstab -U /mnt >> /mnt/etc/fstab

```

14. Переход к корневому каталогу

```
arch-chroot /mnt

```

15. Установка часового пояса

```
ln -sf /usr/share/zoneinfo/Asia/Almaty /etc/localtime

```

16. Установка аппаратных часов

```
hwclock --systohc

```

17. Настройка локали

Раскомментировать `en_US.UTF-8 UTF-8` и другие необходимые локали

```
vim /etc/locale.gen

```

```
locale-gen

```

18. Содание файла local.conf 

```
echo "LANG=en_US.UTF-8" > /etc/locale.conf

```

19. Настройка `/etc/hostname`

```
echo arch > /etc/hostname

```

20. Настройка `/etc/hosts`

```
echo "127.0.0.1 localhost" >> /etc/hosts
echo "::1 localhost" >> /etc/hosts
echo "127.0.1.1 arch.localdomain arch" >> /etc/hosts
```

21. Установка пароля для администратора

```
passwd

```

22. Установка загрузчика

```
bootctl --path=/boot install

```

23. Установка меню загрузки по умолчанию

```
echo "default arch-*" > /boot/loader/loader.conf

```

24. Установка параметров ядра

```
vim /boot/loader/entries/arch.conf

```

```
title Arch Linux
linux /vmlinuz-linux
initrd /intel-ucode.img
initrd /initramfs-linux.img
options root=UUID=f140e1cd-43af-423f-9e53-2f9477e82dd5 rw

```

>UUID корневого раздела

25. Перезагрузка

## Дополнительная настройка [опционально]

### Тихая загрузка

Добавляем параметр quiet splash в параметры загрузчика

```
vim /boot/loader/entries/arch.conf

```

```
title Arch Linux
linux /vmlinuz-linux
initrd /intel-ucode.img
initrd /initramfs-linux.img
options root=UUID=f140e1cd-43af-423f-9e53-2f9477e82dd5 rw quiet splash

```

### Автомонтирование доп. жесткого диска

1. Определяем UUID и файловую систему жесткого диска

```
blkid

```

2. Добавляем запись в fstab

```
vim /etc/fstab

```

```
UUID=fbde5f72-0f38-4847-adcf-4ccc502edca2 /mnt/hdd ext4

```

### Автоподключение к wifi

1. Подключаемся к wifi

```
wifi-menu

```

2. Определяем имя беспроводного сетевого интерфейся

```
ip link

```

3. Создаем службу для сетевого интерфейся wlp0s20f3

```
systemctl enable netctl-auto@wlp0s20f3.service

```

### Изменение шрифта tty

1. Выбираем шрифт из папки /usr/share/kbd/consolefonts

2. В файле /etc/vconsole.conf создать переменную FONT со значением имени шрифта

```
FONT=ter-u16n

```

## Создание пользователя

1. Добавление пользователя `max`

```
useradd -m max

```

2. Установка пароля для `max`

```
passwd max

```

3. Добавление пользователя `max` в группы

```
usermod -aG wheel,audio,video,storage,optical,input max

```

4. Доступ к sudo все пользователям группы `wheel`

```
vim /etc/sudoers

```

Убираем комментарий строки #%wheel ALL=(ALL) ALL


## Графический сервер

### xorg-server

1. Установка `xorg-server`

```
pacman -S xorg-server xorg-xinit

```

2. Установка `xorg-xinit`

```
pacman -S xorg-xinit

```

### Тачпад

1. Создаем конфигурационный файл для тачпада.

```
vim /etc/X11/xorg.conf.d/20-touchpad.conf

```

```
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

```

### Клавиатура

1. Создаем конфигурационный файл для клавиатуры

```
vim /etc/X11/xorg.conf.d/20-keyboard.conf

```

```
Section "InputClass"
    Identifier "system-keyboard"
    MatchIsKeyboard "on"
    Option "XkbLayout" "us,ru"
    Option "XkbOptions" "grp:win_space_toggle"
EndSection

```

### Установка и настройка драйверов видео

1. Установка драйверов видеокарты

```
pacman -S xf86-video-intel xf86-video-nouveau

```

2. Создание конфигурационного файла для `intel graphics`

```
vim /etc/X11/xorg.conf.d/20-intel.conf

```

```
Section "Device"
    Identifier "Intel"
    Driver "intel"
    BusID "PCI:0:2:0"
    Option "TearFree" "true"
EndSection

```
3. Создание конфигурационного файла для `nvidia graphics`

```
vim /etc/X11/xorg.conf.d/20-nouveau.conf

```

```
Section "Device"
	Identifier "Nvidia"
	Driver "nouveau"
	BusID "PCI:1:0:0"
EndSection

```

### Установка драйверов звуковой карты

```
pacman -S alsa-lib pulseaudio pulseaudio-alsa alsa-lib alsa-firmware playerctl pamixer

```









