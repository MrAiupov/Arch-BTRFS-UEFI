# Arch-BTRFS-UEFI

`Bash` скрипты автоустановки `Arch Linux` c `UEFI` на `btrfs` раздел `nvme0`, с поддержкой снимков от `Timeshift`, и загрузкой данных снимков напрямую через `grub-btrfs`. Скрипт автоматически создаёт три раздела и устанавливает чистый `Arch Linux` (вместе с `Grub2`), с возможностью доустановить `Plasma`, `SDDM` и драйверами `Nvidia`, и минимальным набором важных программ, список которых можно посмотреть в скрипте `Arch BTRFS UEFI Clear 3`.

В скрипте `Arch BTRFS UEFI Clear 1` вы можете заранее сами изменить размер разделов и диск на который идёт установка, в пунктах `2.4 создание разделов`, `2.4.2 Форматирование дисков`, `2.4.3 Монтирование дисков и создание томов и папок`.

По умолчанию установка осуществляется на диск `nvme0` с созданием трёх разделов по порядку:

1. Раздел `nvme0n1p1` это `/boot` 2Gb (fat32)
2. Раздел `nvme0n1p2` это `/swap` 12Gb (swap)
3. Раздел `nvme0n1p3` это `/` (btrfs)

Но вы можете изменить диск `nvme0` с разделами `nvme0n1p1`,`nvme0n1p2`,`nvme0n1p3`,

на любой другой диск, например `sda` с разделами `sda1`,`sda2`,`sda3`, или на диск `sdb` с разделами `sdb1`,`sdb2`,`sdb3`.

Какие подтомы `@` создаются, и какие функции выполняют, они в основном названы в честь системных каталогов:

* `@` - это основной корневой подтом, поверх которого будут монтироваться все подтомы.
* `@home` - это домашний каталог. Он состоит из большей части ваших данных, включая Рабочий стол и Загрузки.
* `@var` - содержит логи, временные файлы, кэши, игры и т. д.
* `@opt` - содержит сторонние программы
* `@temp` - содержит определенные временные файлы и кэши
* `@.snapshots` - каталог для хранения снимков (для `Timeshift` он не нужен, поэтому его нет по умолчанию в установке, но если вы используете другие программы для создания снимков, вы можете заранее добавить его вручную)

Скрипты можно заранее скачать и запустить локально во время уставноки Arch Linux, либо клонировать их в свой гитхаб, и создать на каждый скрипт сокращённую ссылку через git.io, для это будет достаточно загрузить их на свой гитхаб, открыть каждый скрипт в режиме просмотра `RAW`, скопировать данную ссылку и сократить через генератор `git.io`. Я собственно этим способом и воспользовался. Я мог бы сократить четыре скрипта до одного, но есть пару моментов, которые я не смог реализовать на `bash`. Так что пришлось идти на данные компромиссы. Если вам нужен чистый Arch Linux без программ и Plasma, просто не запускайте скрипт `Arch BTRFS UEFI Clear 3`, просто потом сами установите рабочий стол и программы на своё усмотрение. 

Порядок запуска скриптов через `wget` сокращенных через`git.io` и других команд установки. Естественно вы должны будете иметь доступ в интернет, как это сделать, вы можете почитать в вики страницах Arch Linux.
1. Обязательно проверяем имена разделов командой `lsblk`, чтобы имя нашего диска для установки, совпало с разделом для установки в скрипте `Arch BTRFS UEFI Clear 1`.
3. Обновляем базы командой `pacman -Sy`
4. Устанавливаем wget командой `pacman -S wget`
5. Запускаем скрипт `Arch BTRFS UEFI Clear 1` командой `wget git.io/JMfV9 && sh JMfV9`
5. Запускаем скрипт `Arch BTRFS UEFI Clear 2` командой `wget git.io/JMfwh && sh JMfwh`
6. Отредактируем файл `mkinitcpio.conf` командой `nano /etc/mkinitcpio.conf`
   
   добавим модуль `btrfs` в строке `MODULES=(btrfs)`
   
   сохраним файл `Ctrl+O` и выйдем `Ctrl+X`
   
   cоздадим загрузочный RAM диск командой `mkinitcpio -p linux`
7. Запускаем скрипт `Arch BTRFS UEFI Clear 2.1` командой `wget git.io/JMfrY && sh JMfrY`
8. Перезагружаемся в систему командой `sudo reboot`
9. Даём права sudo командой `sudo su`
10. Запускаем скрипт `Arch BTRFS UEFI Clear 3` командой `wget git.io/JMfrV && sh JMfrV`

    установки Plasma и дополнительных программ и драйверов
   
11. Выходим и перезагружаемся командами `exit`, `sudo reboot`
12. Незабываем удалить скрипты из раздела `/` и раздела `/home`, через команду `sudo rm имя_скрипта`, если вы их запускали через `git.io`
13. После создания первого снимка в `Timeshift`, не всегда появляется пункт загрузки снимка в `grub-btrfs`, для этого обязательно после создания хотя бы одного снимка, обновить список пукнтов `Grub2` командой `sudo grub-mkconfig -o /boot/grub/grub.cfg`, после этого дынный пункт появится в меню загрузки `Grub2`.

Многие данные взяты и адаптированы для установки со статьи https://www.nishantnadkarni.tech/posts/arch_installation/

и скрипта автоустановки Arch Linux https://github.com/ordanax/arch2018
