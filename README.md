# Arch-BTRFS-UEFI

Автоустановщик Арч линукс на BTRFS раздел `nvme0`.
Скрипт создаёт три раздела и устанавливает Arch Linux (вместе с Grub2) и драйверами Nvidia.
1. Раздел `nvme0n1p1` это `/boot` 2Gb (fat32)
2. Раздел `nvme0n1p2` это `/swap` 12Gb (swap)
3. Раздел `nvme0n1p3` это `/` (btrfs)

В скрипте `Arch BTRFS UEFI Clear 1` вы можете изменить диск на который идёт установка.

Например изменив диск `nvme0` с разделами `nvme0n1p1`,`nvme0n1p2`,`nvme0n1p3`.

На диск `sda` с разделами `sda1`,`sda2`,`sda3`, или на диск `sdb` с разделами `sdb1`,`sdb2`,`sdb3`

Запуск скрипта
1. Проверяем разделы

   `lsblk`
3. Обновляем базы

   `pacman -Sy`
4. Устанавливаем wget

   `pacman -S wget`
5. Запускаем скрипт Arch BTRFS UEFI Clear 1

   `wget git.io/JMfV9 && sh JMfV9`
5. Запускаем скрипт Arch BTRFS UEFI Clear 2

   `wget git.io/JMfwh && sh JMfwh`
6. Отредактируем файл mkinitcpio

   `nano /etc/mkinitcpio.conf`
   
   добавим модуль btrfs в строке `MODULES=(btrfs)`
   
   сохраним файл `Ctrl+O` и выйдем `Ctrl+X`
   
   cоздадим загрузочный RAM диск
   
   `mkinitcpio -p linux`
7. Запускаем скрипт Arch BTRFS UEFI Clear 2.1

   `wget git.io/JMfrY && sh JMfrY`
8. Перезагружаемся в систему

   `sudo reboot`
9. Даём права sudo

   `sudo su`
10. Запускаем скрипт Arch BTRFS UEFI Clear 3 установки Plasma 
и дополнительных программ и драйверов

   `wget git.io/JMfrV && sh JMfrV`
   
11. Перезагружаемся

   `sudo reboot`

Многие данные взяты со статьи https://www.nishantnadkarni.tech/posts/arch_installation/
