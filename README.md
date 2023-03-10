# Домашнее задание к занятию "`9.2. Zabbix. Часть 1`" - `Барановский Станислав`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

## Задание 1

Установите Zabbix Server с веб-интерфейсом.

*Приложите скриншот авторизации в админке. Приложите текст использованных команд в GitHub.*
```
sudo apt update
sudo apt install -y postgresql
wget https://repo.zabbix.com/zabbix/6.2/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.2-4%2Bubuntu22.04_all.deb
sudo dpkg -i zabbix-release_6.2-4+ubuntu22.04_all.deb
sudo apt update
sudo apt install -y zabbix-server-pgsql zabbix-frontend-php php8.1-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent
sudo -u postgres createuser --pwprompt zabbix
sudo -u postgres createdb -O zabbix zabbix
zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
sudo nano /etc/zabbix/zabbix_server.conf # DBPassword=password
sudo systemctl restart zabbix-server zabbix-agent apache2
sudo systemctl enable zabbix-server zabbix-agent apache2

http://localhost/zabbix/  login:Admin passwd:zabbix
```
![Скриншот веб-интерфейса](https://github.com/StanislavBaranovskii/9-2-hw-zabbix-1/blob/main/img/9-2-1.png "Скриншот веб-интерфейса")

---

## Задание 2

Установите Zabbix Agent на два хоста.

*Приложите скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу. Приложите скриншот лога zabbix agent, где видно, что он работает с сервером. Приложите скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные. Приложите текст использованных команд в GitHub.*
```
wget https://repo.zabbix.com/zabbix/6.2/debian/pool/main/z/zabbix-release/zabbix-release_6.2-4%2Bdebian11_all.deb
sudo dpkg -i zabbix-release_6.2-4+debian11_all.deb
sudo apt update
sudo apt install -y zabbix-agent
sudo nano /etc/zabbix/zabbix_agentd.conf # Server=192.168.32.211 # LogFileSize=64
sudo systemctl restart zabbix-agent
sudo systemctl enable zabbix-agent
```
![Скриншот раздела Configuration > Hosts](https://github.com/StanislavBaranovskii/9-2-hw-zabbix-1/blob/main/img/9-2-2-1.png "Скриншот раздела Configuration > Hosts")
![Скриншот лога zabbix agent](https://github.com/StanislavBaranovskii/9-2-hw-zabbix-1/blob/main/img/9-2-2-2.png "Скриншот лога zabbix agent")
![Скриншот лога zabbix agent](https://github.com/StanislavBaranovskii/9-2-hw-zabbix-1/blob/main/img/9-2-2-3.png "Скриншот лога zabbix agent")
![Скриншот лога zabbix agent](https://github.com/StanislavBaranovskii/9-2-hw-zabbix-1/blob/main/img/9-2-2-4.png "Скриншот лога zabbix agent")
![Скриншот раздела Monitoring > Latest data](https://github.com/StanislavBaranovskii/9-2-hw-zabbix-1/blob/main/img/9-2-2-5.png "Скриншот раздела Monitoring > Latest data для debian-1")
![Скриншот раздела Monitoring > Latest data](https://github.com/StanislavBaranovskii/9-2-hw-zabbix-1/blob/main/img/9-2-2-6.png "Скриншот раздела Monitoring > Latest data для debian-2")

---

## Задание 3*

Установите Zabbix Agent на Windows (компьютер) и подключите его к серверу Zabbix.

*Приложите скриншот раздела Latest Data, где видно свободное место на диске C:*
```
```
![Скриншот раздела Latest Data](https://github.com/StanislavBaranovskii/9-2-hw-zabbix-1/blob/main/img/9.2.3.png "Скриншот раздела Latest Data")
![Скриншот раздела Configuration > Hosts](https://github.com/StanislavBaranovskii/9-2-hw-zabbix-1/blob/main/img/9.2.3.1.png "Скриншот раздела Configuration > Hosts")
