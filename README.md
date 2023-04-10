# Домашнее задание к занятию «Система мониторинга Zabbix» Семикова Т.В. FOPS-9

### Задание 1 

Установите Zabbix Server с веб-интерфейсом.

#### Процесс выполнения
1. Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
2. Установите PostgreSQL. Для установки достаточна та версия что есть в системном репозитороии Debian 11
3. Пользуясь конфигуратором комманд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache
4. Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server

#### Требования к результаты 
1. Прикрепите в файл README.md скриншот авторизации в админке
2. Приложите в файл README.md текст использованных команд в GitHub

#### Команды:
1. sudo apt update
2. wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4+debian11_all.deb
3. sudo dpkg -i zabbix-release_6.0-4+debian11_all.deb
4. sudo apt update
5. sudo apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent
6. sudo -u postgres createuser --pwprompt zabbix
7. sudo -u postgres createdb -O zabbix zabbix
8. zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
9. nano /etc/zabbix/zabbix_server.conf параметр DBPassword=***
10. sudo systemctl restart zabbix-server zabbix-agent apache2
11. sudo systemctl enable zabbix-server zabbix-agent apache2

#### Ответ:
![alt text](https://github.com/SemikovaTV/hw_zabbix/blob/main/1.jpg)

### Задание 2 

Установите Zabbix Agent на два хоста.

#### Процесс выполнения
1. Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
2. Установите Zabbix Agent на 2 виртмашины, одной из них может быть ваш Zabbix Server
3. Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов
4. Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera
5. Проверьте что в разделе Latest Data начали появляться данные с добавленных агентов

#### Требования к результаты 
1. Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу
![alt text](https://github.com/SemikovaTV/hw_zabbix/blob/main/2.jpg)
2. Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером
![alt text](https://github.com/SemikovaTV/hw_zabbix/blob/main/3.jpg)
3. Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.
![alt text](https://github.com/SemikovaTV/hw_zabbix/blob/main/4.jpg)
4. Приложите в файл README.md текст использованных команд в GitHub

#### Команды:
1. sudo apt update
2. wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4+debian11_all.deb
3. sudo dpkg -i zabbix-release_6.0-4+debian11_all.deb
4. sudo apt update
5. apt install zabbix-agent
6. systemctl restart zabbix-agent
7. systemctl enable zabbix-agent
8. sudo nano /etc/zabbix/zabbix_agentd.conf редактировала параметр Server=127.0.0.1/Server=192.168.0.106
9. systemctl restart zabbix-agent
