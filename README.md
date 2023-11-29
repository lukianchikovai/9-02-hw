# Домашнее задание к занятию "Система мониторинга Zabbix" - Юлия Лукьянчикова


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw>   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя: done
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-home>   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.

Желаем успехов в выполнении домашнего задания!

### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1 

Установите Zabbix Server с веб-интерфейсом.

1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции. 
2. Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11 - **done**
3. Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache - **done**
4. Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server - **done**

#### Результаты: 

1. Скриншот авторизации в админке - [Общая ссылка на архив со скриншотами](https://drive.google.com/drive/folders/1d2AO__ptEc5QzBOBU-tTmOEiU0azO8ox?usp=sharing)
2. Текст использованных команд: 

```
sudo -i 
apt update
apt install postgresql
exit
wget https://repo.zabbix.com/zabbix/6.4/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.4-1+ubuntu22.04_all.deb
dpkg -i zabbix-release_6.4-1+ubuntu22.04_all.deb
apt update
apt install zabbix-server-pgsql zabbix-frontend-php php8.1-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent
sudo -u postgres createuser --pwprompt zabbix
sudo -u postgres createdb -O zabbix zabbix
zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
sudo nano /etc/zabbix/zabbix_server.conf
DBPassword=****
sudo systemctl restart zabbix-server zabbix-agent apache2
sudo systemctl enable zabbix-server zabbix-agent apache2
sudo systemctl status zabbix-server.service

```

### Задание 2

Установите Zabbix Agent на два хоста.

1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
2. Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server - **done**
3. Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов - **done**
4. Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera - **done**
5. Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов - **done**

#### Результаты:
1. Скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу
2. Скриншот лога zabbix agent, где видно, что он работает с сервером
3. Скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные

[Общая ссылка на архив со скриншотами](https://drive.google.com/drive/folders/1d2AO__ptEc5QzBOBU-tTmOEiU0azO8ox?usp=sharing)

4. Текст использованных команд:

```
sudo nano zabbix_agentd.conf
Server = Zabbix Server IP address
sudo systemctl restart zabbix-agent.service
tail -f /var/log/zabbix/zabbix_agentd.log

```
