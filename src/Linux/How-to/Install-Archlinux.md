# Установка  ArchLinux

## Установочный носитель

1. Скачать образ [Archlinux](https://archlinux.org/download/)

2. Определяем флешку
~~~~
$ lsblk
~~~~ 

3. Записываем образ на флешку
~~~~
$ sudo dd bs=4M if=archlinux-2021.02.01-x86_64.iso of=/dev/sdc status=progress oflag=sync
~~~~

## Базовая установка

### Подключение к сети по wi-fi

1. Запускаем iwctl
~~~~
$ iwctl
~~~~

2. Получаем список устройств 
~~~~
[iwd]# device list
~~~~

3. Получаем список доступных сетей
~~~~
[iwd]# station <устройство> get-networks
~~~~

4. Подключаемся
~~~~
[iwd]# station <устройство> connect <SSID>
~~~~

5. Проверяем
~~~~
ping 8.8.8.8
~~~~

### Синхронизация времени

1. Включаем синхронизацию системных часов
~~~~
timedatectl set-ntp true
~~~~

2. Проверяем
~~~~
timedatectl status
~~~~

### Разметка дисков

1. Проверяем подлюченные диски
~~~~
lsblk
~~~~

2. Запускаем fdisk
~~~~
fdisk /dev/sdb
~~~~

| Раздел | Размер      | Тип раздела      | Файловая система |
|--------|-------------|------------------|------------------|
| sdb1   | 550MB       | EFI System       | vfat             |
| sdb2   | Больше 20GB | Linux filesystem | ext4             |

2. Форматируем загрузочный раздел
~~~~
mkfs.fat -F32 /dev/sdb1
~~~~

3. Подключаем устройство как подкачку
~~~~
swapon /dev/sdb2
~~~~

4. Форматируем корневой раздел
~~~~
mkfs.ext4 /dev/sdb3
~~~~

### Установка основных пакетов

1. Монтируем корневой раздел
~~~~
mount /dev/sdb2 /mnt
~~~~

2. Устанавливаем пакеты
~~~~
pacstrap /mnt base base-devel linux-lts linux-firmware vim
~~~~

### Генерация таблицы файловой системы

~~~~
genfstab -U /mnt >> /mnt/etc/fstab
~~~~

### Переход к корневому каталогу

~~~~
arch-chroot /mnt
~~~~

### Настройка часов

1. Установка часового пояса
~~~~
ln -sf /usr/share/zoneinfo/Asia/Almaty /etc/localtime
~~~~

2. Установка аппаратных часов
~~~~
hwclock --systohc
~~~~

### Настройка локали
1. Раскомментировать `en_US.UTF-8 UTF-8` и другие необходимые локали в файле `/etc/locale.gen`

2. Сгенерировать локаль
~~~~
locale-gen
~~~~

3. Установка системной локали
~~~~
echo "LANG=en_US.UTF-8" > /etc/locale.conf
~~~~

### Настройка имени хоста

~~~~
echo arch > /etc/hostname
~~~~

### Настройка доменных имён

~~~~
echo "127.0.0.1 localhost" >> /etc/hosts
echo "::1 localhost" >> /etc/hosts
echo "127.0.1.1 arch.localdomain arch" >> /etc/hosts
~~~~

### Установка загрузчика

1. Устанавливаем пакеты
~~~~
pacman -S grub efibootmgr dosfstools os-prober mtools
~~~~

2. Созадем папку `EFI`
~~~~
mkdir /boot/EFI
~~~~

3. Монтируем загрузочный раздел
~~~~
mount /dev/sdb1 /boot/EFI
~~~~

4. Устанавливаем `grub`
~~~~
grub-install --target=x86_64-efi --bootloader-id=grub_uefi --recheck
~~~~

5. Некоторые косметические изменения в `/etc/default/grub`
В `GRUB_TIMEOUT` устанавливаем `0`
В `GRUB_CMDLINE_LINUX_DEFAULT` удаляем параметр `quiet`

5. Генерируем конфиг `grub`
~~~~
grub-mkconfig -o /boot/grub/grub.cfg
~~~~

### Установка пароля администратора

~~~~
passwd
~~~~

### Установка пакетов для подключения к сети

1. Установка
~~~~
pacman -S networkmanager wpa_supplicant
~~~~

2. Автоподключение после старта системы
~~~~
systemctl enable NetworkManager
~~~~

### Изменение шрифта tty

1. Копируем необходимый шрифт в папку /usr/share/kbd/consolefonts

2. В файле /etc/vconsole.conf создать переменную FONT со значением имени шрифта
~~~~
FONT=ter-u16n
~~~~

## Создание пользователя

1. Добавление пользователя `max`
~~~~
useradd -m max
~~~~

2. Установка пароля для `max`
~~~~
passwd max
~~~~

3. Добавление пользователя `max` в группы
~~~~
usermod -aG wheel,audio,video,storage,optical,input max
~~~~

4. Расскоментировать строку `#%wheel ALL=(ALL) ALL` в `/etc/sudoers`

## Графический сервер

### xorg-server

1. Установка `xorg-server`
~~~~
pacman -S xorg-server xorg-xinit
~~~~

2. Установка `xorg-xinit`
~~~~
pacman -S xorg-xinit
~~~~

3. Установка драйверов для видеокарты
~~~~
pacman -S xf86-video-intel nvidia nvidia-utils nvidia-settings
~~~~

4. Установка драйверов для звуковой карты
~~~~
pacman -S pulseaudio pulseaudio-alsa alsa-lib alsa-firmware playerctl pamixer
~~~~

5. Настройка `/etc/X11/xorg.conf`
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
    Option "SHMConfig" "on"
EndSection
~~~~

### Bluetooth

1. Необходимые пакеты `blueman`

2. Включаем службы

~~~~
$ systemctl enable bluetooth.service
~~~~

3. Добавляем пользователя в группу
 
~~~~
# gpasswd -a max lp
~~~~

4. Добавляем blueman-applet в автозагрузку
