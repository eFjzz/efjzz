# Users and groups management Linux on (Terminal);
---
## Основные понятия

+ **user** — учётная запись в системе;  
+ **group** — объединение пользователей для управления правами; 

> Каждый пользователь имеет: UID (идентификатор) ; основную группу (GID) ; дополнительные группы ;
---
# Управление пользователями
## Просмотр пользователей
`cat /etc/passwd`
+ Через системную базу (предпочтительно):
`getent passwd username`
+ Текущий пользователь:
`whoami`
+ Информация о пользователе:
`id username`
+ Коротко про getent
`getent` 
> команда для получения данных о пользователях и группах из системной базы (включая LDAP).
---
## Cоздание и редактирование пользователя:
+ Создание пользователя
`sudo useradd username`
+ Создать с домашней директорией:
`sudo useradd -m username`
+ Создать с указанием оболочки:
`sudo useradd -m -s /bin/bash username`
+ Установка пароля
`sudo passwd username`
---
+ Переименовать пользователя:
`sudo usermod -l newname oldname`
+ Переименовать домашнюю папку:
`sudo usermod -d /home/newname -m newname`
+ Добавить в группу:
`sudo usermod -g groupname username`
> используй -aG, иначе удалятся другие группы.
---
+ Удаление пользователя
`sudo userdel username`
+ Удалить вместе с домашней папкой:
`sudo userdel -r username`
---
## Управление группами
+ Просмотр групп
`cat /etc/group`
+ Через системную базу:
`getent group`
+ Группы текущего пользователя:
`groups`
+ Создание группы:
`sudo groupadd groupname`
+ Переименование группы
`sudo groupmod -n newname oldname`
+ Удаление группы:
`sudo groupdel groupname`
---
+ Изменение владельца
`sudo chown username file.txt`
+ Изменить владельца и группу:
`sudo chown username:groupname file.txt`
+ Изменить группу файла:
`sudo chgrp groupname file.txt`
+ Проверить пользователя:
`getent passwd username`
+ Проверить группу:
`getent group groupname`
> Если запись существует — команда выведет строку.
---
## Конфигурация пользователей:
+ Основные системные файлы:
| Файл           | Назначение                                               |
|----------------|----------------------------------------------------------|
| /etc/passwd    | список пользователей                                     |
| /etc/shadow    | зашифрованные пароли                                     |
| /etc/group     | список групп                                             |
| /etc/login.defs| настройки по умолчанию (UID, срок действия пароля)       |
| /etc/skel/     | шаблон файлов для новых пользователей                    |
---
+ Структура записи в /etc/passwd
+ Пример:
> user:x:1001:1001:User Name:/home/user:/bin/bash
+ Поля:
> имя пользователя : пароль (x — хранится в /etc/shadow) : UID : GID : описание : домашняя директория : оболочка (shell) ;
---
### Домашняя директория:
+ Создаётся при использовании -m:
`sudo useradd -m username`
+ Шаблон файлов копируется из:
`/etc/skel/`
---
### Смена оболочки (shell):
+ Посмотреть доступные оболочки:
`cat /etc/shells`
+ Изменить оболочку:
`sudo usermod -s /bin/bash username`
---
### Настройка срока действия пароля:
+ Посмотреть параметры:
`chage -l username`
+Изменить срок действия:
`sudo chage username`
---
## Права доступа:
Просмотр прав:
`ls -l`
+ Пример:
`-rw-r--r-- 1 user group 1234 file.txt`
+ Где:
> user — владелец; group — группа; rwx — права (read, write, execute)
