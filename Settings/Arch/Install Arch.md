
___
##### Launching with a boot flash drive!

#### 1 option: Установщик
 **archinstall**: официальный инсталлятор для Arch Linux, который упрощает процесс установки. Он разработан на языке Python и распространяется под лицензией GPLv3.
#### 2 option: Ручная установка

1. Если подключение к сети беспроводное, то нужно через утилиту iwctl выбрать сеть wi-fi и подключится к ней.
2. Далее нужно по пути /etc/pacman.d/mirrorlist выбрать зеркала. Ставлю от yandex
3. Диск:
	- lsblk для проверки наличия дисков
	- cfdisk /dev/ваш диск для начала разметки диска
	- Далее выбираем тип разметки диска. На EFI берем gpt
	- Теперь размечаем диск:
		-  Выделяем 256M для загрузочного раздела и меняем тип на EFI system
		- Остальное место отдаем под основной раздел (type Linux filesystem) или разделяем его на нужные вам части
	- Форматируем разделы:
		- Форматируем загрузочный раздел: mkfs.vfat /dev/загрузочный раздел
		- Форматируем основной раздел: mkfs.ext4 /dev/основной раздел
	- Монтируем диски:
		- Монтируем основной раздел: mount /dev/основной раздел /mnt
		- Монтируем загрузочный раздел: сначала создаем директорию mkdir -p /mnt/boot/efi потом монтируем  mount /dev/загрузочный раздел /mnt/boot/efi
4. Ставим пакеты: pacstrap /mnt base base-devel linux linux-firmware linux-header nano bash-completion grub efibootmgr networkmanager
	- base - базовая система
	- base-devel - утилиты для сборки программ
	- linux - ядро
	- linux-firmware - прошивки для линукс
	- linux-header - хедеры 
	- nano - текстовый редактор
	- bash-completion - автодополнение для команд bash
	- grub -загрузчик
	- efibootmgr - утилита для efi
	- networkmanager - менеджер для интернета
5. Генерация fstab: genfstab /mnt и перенаправляем genfstab /mnt >> /mnt/etc/fstab
6. Меняем корень системы: arch-chroot /mnt
7. Запускаем networkmanaget:  systemctl enable Networkmanager
8. Создаем пользователя:
	- useradd -m user
	- passwd user
9. Пароль рута: passwd root
10. Даем пользователю права sudo: 
	- Меняем /etc/sudoers и добавляем себя рядом с root и такими же правами
11. Локализация:
	- Заходим в /etc/locale.gen
	- раскоментируем en_ES и ru_RU
12. Ставим стандартную локализацию: /etc/locale.conf и пишем LANG="en_US.UTF-8" или другую локаль
13. Генерация локализаций: locale-gen 
14. Ставим загрузчик: grub-install /dev/диск (/dev/sda) и grub-mkconfig -o /boot/grub/grub.cfg
15. Размонтировка разделов: umount -R /mnt
16. reboot