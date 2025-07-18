# 📚 Установка pgAdmin (Web-based GUI для PostgreSQL) без Docker

> Актуально для Linux (Debian/Ubuntu)

---

## 📦 Установка зависимостей

```bash
sudo apt update && sudo apt install curl ca-certificates gnupg -y
```

---

## 📥 Добавляем репозиторий pgAdmin

```bash
curl https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo gpg --dearmor -o /usr/share/keyrings/pgadmin-keyring.gpg
```

```bash
echo "deb [signed-by=/usr/share/keyrings/pgadmin-keyring.gpg] https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4" | sudo tee /etc/apt/sources.list.d/pgadmin4.list
```

---

## 🔁 Устанавливаем pgAdmin (веб-версия)

```bash
sudo apt update
sudo apt install pgadmin4-web -y
```

---

## ⚙️ Настройка и запуск pgAdmin

```bash
sudo /usr/pgadmin4/bin/setup-web.sh
```

> Тут нужно будет вручную ввести:
>
> - Email (например, `admin@admin.com`)
> - Пароль (например, `admin123`)
> - Повторить пароль

После успешной настройки будет выведен адрес панели — обычно это:
```
http://localhost/pgadmin4
```

---

## 🌐 Как открыть доступ извне (GCP, UFW и т.п.)

- Если используешь **Google Cloud VM**, добавь правило фаервола для порта `80` (HTTP) — если доступа ещё нет.
- Если используешь `ufw` (локальный фаервол):

```bash
sudo ufw allow 80
```

---

## 🔐 Где лежат данные pgAdmin

Конфиги, логины, сервера — всё в:

```bash
/var/lib/pgadmin/
```

---

## 🔁 Автозапуск

pgAdmin автоматически запускается как systemd-сервис:

```bash
sudo systemctl status apache2
```

(Он работает через Apache — pgAdmin4 интегрируется в него как Web App)
