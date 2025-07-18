
# 🔥 Настройка фаерволов для сервера с pgAdmin и FileBrowser (GCP)

## 📍 Входящие порты, которые нужно открыть

| Назначение              | Порт | Протокол |
|-------------------------|------|----------|
| FileBrowser             | 8080 | TCP      |
| pgAdmin (если не Apache)| 5050 | TCP      |
| Apache (pgAdmin через веб) | 80, 443 | TCP  |

---

## 🧱 1. Настройка фаервола в Google Cloud

### Перейди в Google Cloud Console:

**VPC Network → Firewall Rules → CREATE FIREWALL RULE**

### Заполни так:

- **Name**: `allow-admin-panels`
- **Targets**: `All instances in the network` *(или метки/теги для конкретного инстанса)*
- **Source IP ranges**: `0.0.0.0/0` *(можно указать свой IP для безопасности)*
- **Protocols and ports**:
  - ✅ Выбрать `Specified protocols and ports`
  - Включить `tcp`
  - Указать порты:

    ```
    8080,5050,80,443
    ```

- **Нажать**: `Create`

---

## 🧱 2. Настройка фаервола внутри сервера (UFW)

Проверь, активен ли UFW:

```bash
sudo ufw status
```

Если он **не активен**, то ничего не нужно делать.  
Если **активен**, разреши нужные порты:

```bash
# Разрешаем FileBrowser
sudo ufw allow 8080/tcp

# Разрешаем pgAdmin, если работает не через Apache
sudo ufw allow 5050/tcp

# Разрешаем Apache (если pgAdmin через /pgadmin4)
sudo ufw allow 'Apache Full'

# Перезапускаем UFW
sudo ufw reload
```

---

## ✅ Проверка открытых портов

Проверь, слушаются ли нужные порты:

```bash
sudo ss -tuln | grep -E '8080|5050|:80|:443'
```

---

## 🌍 Проверка из браузера

Открой в браузере:

```
http://<IP-СЕРВЕРА>:8080     # FileBrowser
http://<IP-СЕРВЕРА>:5050     # pgAdmin (если не через Apache)
http://<IP-СЕРВЕРА>/pgadmin4 # pgAdmin через Apache
```

Если страница открывается — всё работает.

