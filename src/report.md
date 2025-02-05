## Part 1. Установка ОС

Выводим информацию о системе с помощью команды `cat /etc/issue`: \
![screen_1](images/part_1.png)


## Part 2. Создание пользователя

Создаём нового пользователя командой `sudo useradd -G adm -s /bin/bash new_user`. Устанавливаем пароль новому пользователю командой `sudo passwd new_user`.

Выводим информацию о пользователях системы командой `cat /etc/passwd`: \
![screen_2](images/part_2.png)


## Part 3. Настройка сети ОС

Для изменения названия машины используем команду `sudo hostnamectl set-hostname user-1`

Для установки временной зоны используем команду `sudo timedatectl set-timezone Asia/Novosibirsk`. Проверяем временные параметры командой `date`.

Выводим сетевые интерфейсы в консоль командой `ip -br link show`: \
![screen_3.3](images/part_3.3.png)

**lo** - внутренний виртуальный сетевой интерфейс, позволяющий подключаться машине к самой себе.

Выводим IP адреса, полученные от DHCP сервера, командой `sudo dhclient -v enp0s3`: \
![screen_3.4](images/part_3.4.png)

**DHCP** - Dynamic Host Configuration Protocol (Протокол Динамической Настройки Узла).

Выводим внутренний IP-адрес шлюза (GW) командой `hostname -I`: \
![screen_3.5.1](images/part_3.5.1.png)

Выводим внешний IP-адрес шлюза (IP) командой `curl ifconfig.me`: \
![screen_3.5.2](images/part_3.5.2.png)

Для изменения IP, GW и DNS редактируем файл `/etc/netplan/00-installer-config.yaml`: \
![screen_3.6](images/part_3.6.png)

Совершаем перезапуск системы командой `reboot`.

Выводим внутренний IP-адрес шлюза командой `hostname -I`: \
![screen_3.7.1](images/part_3.7.1.png)

Проверяем установленный DNS командой `ping`: \
![screen_3.7.2](images/part_3.7.2.png) \
![screen_3.7.3](images/part_3.7.3.png)


## Part 4. Обновление ОС

С помощью команды `sudo apt update` даём системе понять, какие пакеты нуждаются в обновлении.

Обновляем пакеты с помощью команды `sudo apt upgrade`.

Для того, чтобы убедиться, что пакеты обновились, повторно вводим команду `sudo apt upgrade`: \
![screen_4](images/part_4.png)


## Part 5. Использование команды sudo

С помощью команды `sudo usermod -aG sudo new_user` выдаем пользователю разрешение на выполнение команд от имени суперпользователя.

`sudo` - команда, используемая для получения прав доступа, нужных для взаимодействия с важными системными приложениями.

Переключаемся на пользователя "new_user" командой `su - new_user`.

С помощью команды `sudo hostnamectl set-hostname fresh_hostname` устанавливаем новое имя хоста и выводим информацию о нем с помощью команды `hostnamectl`: \
![screen_5](images/part_5.png)


## Part 6. Установка и настройка службы времени

С помощью команды `sudo timedatectl set-ntp true` включаем синхронизацию по протоколу NTP и проверяем командой `timedatectl show`: \
![screen_6](images/part_6.png)


## Part 7. Установка и использование текстовых редакторов

#### Создание и сохранение файла

**NANO**: \
Для входа в редактор используем команду `nano`. В редакторе пишем nickname: \
![screen 7.1.1](images/part_7.1.1.png)

Выходим с помощью сочетания клавиш "Ctrl" + "X". Сохраняем изменения с помощью "Y", вписываем название файла и нажимаем "Enter".

**VIM**: \
Для входа в редактор используем команду `vim` В редакторе пишем nickname: \
![screen 7.1.2](images/part_7.1.2.png)

Нажимаем "Esc" для перехода в командную строку и пишем ":wq test_VIM.txt".

**MCEDIT**: \
Для входа в редактор используем команду `mcedit`. В редакторе пишем nickname: \
![screen 7.1.3](images/part_7.1.3.png)

Для сохранения нажимаем "F2", вводим название файла и выбираем "Ok". После нажимаем "F10" для выхода из редактора.

#### Редактирование файла (без сохранения)

**NANO**: \
Для редактирования файла используем команду `nano test_NANO.txt`. Далее меняем nickname на строку: \
![screen_7.2.1](images/part_7.2.1.png)

Для выхода без сохранения файла нажимаем "Ctrl" + "X", после чего нажимаем "N". 

**VIM**: \
Для редактирования файла используем команду `vim test_VIM.txt`. Далее меняем nickname на строку: \
![screen_7.2.2](images/part_7.2.2.png)

Нажимаем "Esc" для перехода в командную строку и пишем ":q!".

**MCEDIT**: \
Для редактирования файла используем команду `mcedit test_MCEDIT.txt`. Далее меняем nickname на строку: \
![screen_7.2.3](images/part_7.2.3.png)

Для выхода без сохранения нажимаем "F10" и выбираем "No".

#### Поиск и замена (без сохранения)

**NANO**: \
Для редактирования файла используем команду `nano test_NANO.txt`. Нажимаем "Ctrl" + "W" для поиска строки. Вводим интересующую строку и нажимаем "Enter": \
![screen_7.3.1](images/part_7.3.1.png)

Нажимаем "Ctrl" + "\\" для замены строки. Вводим заменяемую строку, новую строку и нажимаем "Y":  \
![screen_7.3.2](images/part_7.3.2.png)

Для выхода без сохранения файла нажимаем "Ctrl" + "X", далее нажимаем "N". 

**VIM**: \
Для редактирования файла используем команду `vim test_VIM.txt`. Нажимаем "Esc" для перехода в командную строку и пишем "/", после чего вводим строку для поиска и нажимаем "Enter": \
![screen_7.3.3](images/part_7.3.3.png)

Нажимаем "Esc" для перехода в командную строку и пишем ":s/", вводим заменяемую строку, далее "/" и вводим строку для вставки и нажимаем "Enter": \
![screen_7.3.4](images/part_7.3.4.png)

Нажимаем "Esc" для перехода в командную строку и пишем ":q!".

**MCEDIT**: \
Для редактирования файла используем команду `mcedit test_MCEDIT.txt`. Далее нажимаем "F7", после чего вводим интересующую строку и нажимаем "Enter": \
![screen_7.3.5](images/part_7.3.5.png)

Далее нажимаем "F4", после чего вводим строку для замены и нажимаем "Enter": \
![screen_7.3.6](images/part_7.3.6.png)

Для выхода без сохранения нажимаем "F10" и "No".


## Part 8. Установка и базовая настройка сервиса SSHD

Устанавливаем службу SSHd командой `sudo apt install openssh-server`.

Добавляем автостарт службы при загрузке системы командой 'sudo upate-rc.d ssh defaults'.

Для изменения порта редактируем файл `/etc/ssh/sshd_config`. Раскомменчиваем cтроку с портом и меняем адрес: \
![screen_8.1](images/part_8.1.png)

Cохраняем изменения в файле и перезапускаем протокол командой `systemctl restart sshd`.

С помощью команды `ps -FC sshd` показываем наличие процесса SSHd: \
![screen_8.2](images/part_8.2.png)

- `ps` - команда, использующаяся для отображения информации о работающих процессах на компьютере;
- `-F` - выдача подробной информации;
- `-C` - информация по дочерним процессам.

Перезагружаем систему командой `reboot`.

Для вывода списка сетевых соединений с прочей информацией используем команду `netstat -tan`: \
![screen_8.3](images/part_8.3.png)

- `-t` (TCP): отображение всех TCP соединений;
- `-a` (all): вывод всех активных и неактивных соединений, слушающих портов;
- `-n` (numeric): отображение адресов и портов в числовом формате, вместо того чтобы пытаться определять имена доменов и названия служб для соответствующих портов.

В выводе под `0.0.0.0` подразумевается любой адрес.

**Значения столбцов вывода**:
1. Proto - протокол сетевого соединения
2. Recv-Q - размер очереди получения в байтах
3. Send-Q - размер очереди отправки в байтах
4. Local Address - локальный адрес соединения
5. Foreign Address - адрес удаленной стороны соединения
6. State - текущее состояние соединения


## Part 9. Установка и использование утилит top, htop

Для вывода мониторинга процессов используем команду `top`: \
![screen_9.1](images/part_9.1.png)

- uptime - `39 min`;
- количество авторизованных пользователей - `1 user`; 
- общая загрузка системы - `load average: 0.02, 0.02, 0.00`;
- общее количество процессов - `105 total`;
- загрузка cpu - `0.0 us, 0.0 sy, 0.0 ni, 99.8 id, 0.2 wa, 0.0 hi, 0.0 si, 0.0 st`;
- загрузка памяти - `1971.4 total, 1504.2 free, 148.0 used, 319.2 buff/cache`;
- pid процесса занимающий больше всего памяти - `1 root`;
- pid процесса, занимающий больше всего процессорного времени - `1 root`.

Для вывода мониторинга процессов используем продвинутый интерактивный инструмент `htop`.

Сортировка по PID: \
![screen_9.2](images/part_9.2.png)

Сортировка по PERCENT_CPU: \
![screen_9.3](images/part_9.3.png)

Сортировка по PERCENT_MEM: \
![screen_9.4](images/part_9.4.png)

Сортировка по TIME: \
![screen_9.5](images/part_9.5.png)

Отфильтрованный для процесса sshd: \
![screen_9.6](images/part_9.6.png)

Процесс syslog, найденный при помощи поиска: \
![screen_9.7](images/part_9.7.png)

Вывод hostname, clock и uptime: \
![screen_9.7](images/part_9.8.png)


## Part 10. Использование утилиты fdisk

Для вывода информации о жестком диске воспользуемся командой `fdisk -l`: \
![screen_10](images/part_10.png)

- Название жесткого диска: `VBOX HARDDISK`;
- Размер: `10 GiB, 10737418240`;
- Количество секторов: `20971520`;
- Размер swap: 0.

## Part 11. Использование утилиты df

Выводим информацию о дисковом пространстве командой `df`: \
![screen_11.1](images/part_11.1.png)

**Информация о корневом разделе**:
- Размер раздела - `8408452`;
- Размер занятого пространства - `4761104`;
- Размер свободного пространства - `3198632`;
- Процент использования - `60%`;
- Единица измерения: КБ (килобайт).

Выводим информацию о дисковом пространстве с типом файловой системы и удобочитаемым выводом помяти командой `df -Th`: \
![screen_11.2](images/part_11.2.png)

**Информация о корневом разделе**:
- Размер раздела - `8.1G`;
- Размер занятого пространства - `4.6G`;
- Размер свободного пространства - `3.1G`;
- Процент использования - `60%`;
- Тип файловой системы раздела - `ext4`.


## Part 12. Использование утилиты du

Выводим информацию о дисковом пространстве командой `du`: \
![screen_12.1](images/part_12.1.png)

По умолчанию команда выводит размер в килобайтах.

Выводим размер папок `/home`, `/var` и `/var/log` в байтах командой `sudo du -sb /home /var/log /var`: \
![screen_12.2](images/part_12.2.png)

Выводим размер папок `/home`, `/var` и `/var/log` в человекочитаемом виде командой `sudo du -sh /home /var/log /var`: \
![screen_12.3](images/part_12.3.png)

**Флаги**:
- `-s` - вывод нужных директорий;
- `-h` - вывод в человекочитаемом стиле;
- `-b` - вывод в нужном размере.

Выводим содержимое каждого вложенного элемента в `/var/log` командой `sudo du -s /var/log/*`: \
![screen_12.4](images/part_12.4.png)

## Part 13. Установка и использование утилиты ncdu

Устанавливаем ncdu командой `sudo apt install ncdu`. Провеяем работоспособность запуском утилиты командой `ncdu`: \
![screen_13.1](images/part_13.1.png)

Выводим размер папки `/home` командой `ncdu /home`: \
![screen_13.2](images/part_13.2.png)

Выводим размер папки `/var` командой `ncdu /var`: \
![screen_13.3](images/part_13.3.png)

Выводим размер папки `/var/home` командой `ncdu /var/home`: \
![screen_13.4](images/part_13.4.png)


## Part 14. Работа с системными журналами

Для удобного просмотра логов открываем файлы в редакторе `vim` с флагом `-R` (только чтение).

**Файлы с логами**: `/var/log/dmesg`, `/var/log/syslog`, `/var/log/auth.log`.

Просматриваем файл логов, связаннный с аунтефикацией, командой `nano -R /var/log/auth.log` и находим последнюю авторизацию пользователя: \
![screen_14.1](images/part_14.1.png)

- Время последней авторизации: `20:34:42`;
- Имя авторизовавшегося пользователя: `collenep`;
- Метод входа в систему `TTY=tty1`.

Перезапускаем SSHD командой `sudo systemctl restart sshd`, открываем `/var/log/auth.log` и ищем логи перезагрузки утилиты: \
![screen_14.2](images/part_14.2.png)


## Part 15. Использование планировщика заданий CRON

Cron — это планировщик задач, используемый для выполнения задач (в фоновом режиме) в указанное время.

Открываем планировщика задач для редактирования командой `crontab -e` и ставим запуск команды `uptime` каждые 2 минуты: \
![screen_15.1](images/part_15.1.png)

Проверяем файл `/var/log/syslog` на работу CRON: \
![screen_15.2](images/part_15.2.png)

Выводим содержимое файла командой `crontab -l`: \
![screen_15.3](images/part_15.3.png)

Открываем планировщика задач для редактирования командой `crontab -e` удаляем задание. После выводим содержимое планировщика командой `crontab -l`: \
![screen_15.4](images/part_15.4.png)
