# marIDE

mar-ide/PLUGIN-FOR-LZT

---
# Создание FILEBROWSER для управление файлами на сервере.

Вставляем в linux-terminal

1.sudo apt update && sudo apt install curl -y

2.curl -fsSL https://raw.githubusercontent.com/filebrowser/get/master/get.sh | bash

3.sudo mkdir -p /srv/files

4.filebrowser -r /srv/files -p 8080 --address 0.0.0.0

---
# Как узнать какое айпи в АДМИН-МЕНЮ файловой директории 

Вставляем в linux-terminal

curl ifconfig.me

---
# Запуск админ панели 

Вставляем в linux-terminal

filebrowser -r /srv/files -p 8080 --address 0.0.0.0

---

# Автозапуск Admin-панели Директории 

Вставляем в linux-terminal

which filebrowser - покажет путь, где находиться.

Почти всегда путь будет - /usr/local/bin/filebrowser

sudo nano /etc/systemd/system/filebrowser.service

---

Вставляем в текстовом редакторе nano/vim:

[Unit]

Description=FileBrowser Admin Panel

After=network.target

[Service]

User=desollatecore

ExecStart=/usr/local/bin/filebrowser -r /srv/files -p 8080 --address 0.0.0.0

Restart=always

[Install]

WantedBy=multi-user.target

---
Активируем и запускаем:

sudo systemctl daemon-reload

sudo systemctl enable filebrowser

sudo systemctl start filebrowser

---
Проверяем 

sudo systemctl status filebrowser
