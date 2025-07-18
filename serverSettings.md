# marIDE

mar-ide/PLUGIN-FOR-LZT

---
# Создание FILEBROWSER для управление файлами на сервере.

[LINUX TERMINAL]

1.sudo apt update && sudo apt install curl -y

2.curl -fsSL https://raw.githubusercontent.com/filebrowser/get/master/get.sh | bash

3.sudo mkdir -p /srv/files

4.filebrowser -r /srv/files -p 8080 --address 0.0.0.0

---
# Как узнать какое айпи в АДМИН-МЕНЮ файловой директории 

[LINUX TERMINAL]

curl ifconfig.me

---
# Запуск админ панели 

[LINUX TERMINAL]

filebrowser -r /srv/files -p 8080 --address 0.0.0.0

---

# Автозапуск Admin-панели Директории 

[LINUX TERMINAL]

which filebrowser - покажет путь, где находиться.

Почти всегда путь будет - /usr/local/bin/filebrowser

sudo nano /etc/systemd/system/filebrowser.service

sudo mkdir -p /srv/filebrowser

sudo chown -R desollatecore /srv/filebrowser

P.S Вместо desollatecore ваш uname

---

[ТЕКСТОВЫЙ РЕДАЕКТОР NANO]

[Unit]

Description=FileBrowser Admin Panel

After=network.target

[Service]

User=desollatecore (Вместо desollatecore ваш uname)

WorkingDirectory=/srv/filebrowser

ExecStart=/usr/local/bin/filebrowser -r /srv/files -p 8080 --address 0.0.0.0

Restart=always

[Install]

WantedBy=multi-user.target


---
Активируем и запускаем:

[LINUX TERMINAL]

sudo systemctl daemon-reload

sudo systemctl enable filebrowser

sudo systemctl start filebrowser

---
Проверяем 

sudo systemctl status filebrowser

# КАК УЗНАТЬ ЛОГИН И ПАРОЛЬ ОТ АДМИН-ПАНЕЛИ ДИРЕКТОРИИ?

journalctl -u filebrowser.service --no-pager | grep "User 'admin' initialized"

