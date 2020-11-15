# Clonezilla Live USB

Необходимые пакеты: `unzip`, `mtools`

1. Загружаем zip архив Clonezilla на сайте [clonezilla.org](https://clonezilla.org/downloads.php)

2. Подготавливаем USB устройство с разделом не менее `512МБ`, с файловой системой `FAT16`, `FAT32` или `NTFS`

3. Монтируем раздел

```
mount /dev/sdc1 /mnt/usb

```

4. Распаковываем архив

```
unzip ~/Downloads/clonezilla-live-2.6.6-15-amd64.zip -d /mnt/usb

```

5. Отключаем звуковой сигнал при загрузке clonezilla [опционально]

- комментируем строку `play 960 440 1 0 4 440 1` в файле `/mnt/usb/boot/grub/grub.cfg`

- удаляем символ `^G` в файле `/mnt/usb/syslinux/syslinux.cfg`

6. Делаем раздел загрузочным 

- переходим в папку `/mnt/usb/utils/linux`

- запускаем скрипт `makeboot.sh`
