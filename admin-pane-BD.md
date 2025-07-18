# 🟢 Установка PostgreSQL

[LINUX TERMINAL]

sudo apt update

sudo apt install postgresql postgresql-contrib -y

---

# 🟢 Создание пользователя 

[LINUX TERMINAL]

sudo -u postgres createuser desollatecore --superuser

sudo -u postgres createdb desollatecore

---

# 🟢 Задаём пароль:

[LINUX TERMINAL]

sudo -u postgres psql

\password desollatecore (ваш uname)

\q

---

# 🟢 Установка pgAdmin 4 (веб-интерфейс):

[УСТАНАВЛИВАЕМ ЗАВИСИМОСТИ, LINUX TERMINAL]

sudo apt install curl ca-certificates gnupg -y

curl https://www.pgadmin.org/static/packages_pgadmin_org.pub | gpg --dearmor | sudo tee /usr/share/keyrings/pgadmin.gpg >/dev/null

[ДОБАВЛЯЕМ РЕПОЗИТОРИЙ]

echo "deb [signed-by=/usr/share/keyrings/pgadmin.gpg] https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/jammy pgadmin4 main" | sudo tee /etc/apt/sources.list.d/pgadmin4.list

sudo apt update

[УСТАНАВЛИВАЕМ pgAdmin Web]

sudo apt install pgadmin4-web -y

[НАСТРАИВАЕМ]

sudo /usr/pgadmin4/bin/setup-web.sh











