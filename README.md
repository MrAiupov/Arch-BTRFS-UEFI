# Arch-BTRFS-UEFI

Автоустановщик Арч линукс на BTRFS раздел nvme.
Скрипт создаёт три раздела и устанавливает Arch Linux (вместе с Grub2)
1. `/boot` 2Gb (Fat32)
2. `/swap` 12Gb (swap)
3. `/` всё остальное (Btrfs)

Запуск скрипта
1. Проверяем разделы `lsblk`
2. Обновляем базы `pacman -Sy`
3. Устанавливаем wget `pacman -S wget`
4. Запускаем скрипт Arch BTRFS UEFI Clear 1
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
10. Запускаем скрипт Arch BTRFS UEFI Clear 3 установки Plasma и дополнительных программ и драйверов
   `wget git.io/JMfrV && sh JMfrV`
11. Перезагружаемся
   `sudo reboot`

Многие данные взяты со статьи https://www.nishantnadkarni.tech/posts/arch_installation/
