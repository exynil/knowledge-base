# 🛡️ Собственный DNS-over-HTTPS (DoH) сервер через AdGuard Home

## 🧰 Что потребуется

1. Доменное имя (например: `dns.test.net`)
2. Простой VPS-сервер (Linux)
3. Открытые порты: `443`, `53`, `3000`
4. SSL-сертификат (через Certbot)

---

## 🔧 Шаг 1. Установка AdGuard Home

~~~~bash
curl -s -S -L https://static.adguard.com/adguardhome/release/AdGuardHome_linux_amd64.tar.gz | tar -xz
cd AdGuardHome
./AdGuardHome -s install
~~~~

---

## 🔓 Шаг 2. Открытие порта 3000

~~~~bash
sudo ufw status
sudo ufw allow 3000/tcp
~~~~

---

## 🌐 Шаг 3. Первичная настройка

Откройте в браузере:

~~~~
http://<IP-адрес сервера>:3000
~~~~

Следуйте мастеру настройки.

---

## 🔐 Шаг 4. Получение SSL-сертификатов

~~~~bash
sudo apt install certbot
sudo certbot certonly --standalone -d dns.test.net
~~~~

Файлы сертификатов будут в:

- `/etc/letsencrypt/live/dns.test.net/fullchain.pem`
- `/etc/letsencrypt/live/dns.test.net/privkey.pem`

---

## ⚙️ Шаг 5. Настройка шифрования в AdGuard Home

1. Перейдите: **Настройки → Настройки шифрования**
2. Включите:
   - HTTPS
   - DNS-over-HTTPS (DoH)
   - DNS-over-TLS (DoT)
3. Укажите имя сервера: `dns.test.net`
4. Укажите пути к сертификатам:
   - Сертификат: `/etc/letsencrypt/live/dns.test.net/fullchain.pem`
   - Ключ: `/etc/letsencrypt/live/dns.test.net/privkey.pem`

---

## 👤 Шаг 6. Добавление клиента в AdGuard

1. Перейдите: **Настройки → Клиенты**
2. Добавьте нового клиента с ID, например: `bob-iphone`

---

## 📄 Шаг 7. Создание профиля для iPhone

Создайте файл `dns-profile.mobileconfig` со следующим содержимым:

~~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN"
   "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
  <key>PayloadContent</key>
  <array>
    <dict>
      <key>DNSSettings</key>
      <dict>
        <key>DNSProtocol</key>
        <string>HTTPS</string>
        <key>ServerURL</key>
        <string>https://dns.test.net/dns-query/bob-iphone</string>
        <key>ServerName</key>
        <string>dns.test.net</string>
      </dict>
      <key>PayloadDescription</key>
      <string>Custom DNS via DoH</string>
      <key>PayloadDisplayName</key>
      <string>DNS: Secure Custom</string>
      <key>PayloadIdentifier</key>
      <string>com.custom.dnsprofile</string>
      <key>PayloadOrganization</key>
      <string>PrivateDNS</string>
      <key>PayloadType</key>
      <string>com.apple.dnsSettings.managed</string>
      <key>PayloadUUID</key>
      <string>D33DDEAD-BEEF-BEEF-BEEF-ABCDEF123456</string>
      <key>PayloadVersion</key>
      <integer>1</integer>
    </dict>
  </array>
  <key>PayloadDisplayName</key>
  <string>Secure DNS Profile</string>
  <key>PayloadIdentifier</key>
  <string>com.custom.dnsprofile.master</string>
  <key>PayloadType</key>
  <string>Configuration</string>
  <key>PayloadUUID</key>
  <string>ABCDEF12-3456-7890-ABCD-EF1234567890</string>
  <key>PayloadVersion</key>
  <integer>1</integer>
</dict>
</plist>
~~~~

> ⚠️ Убедитесь, что путь `dns-query/bob-iphone` совпадает с ID клиента в AdGuard Home.

---

## 📲 Шаг 8. Установка профиля на iPhone

1. Отправьте `.mobileconfig` файл на iPhone (через AirDrop, почту и т.д.)
2. Откройте файл на устройстве — появится предложение установить профиль
3. Перейдите в:
   **Настройки → Профиль загружен** → нажмите **Установить**
4. Подтвердите установку и перезагрузите iPhone (желательно)

---

## ✅ Проверка

1. Зайдите в AdGuard Home → **Журнал DNS-запросов**
2. Убедитесь, что в логах видны запросы от клиента `bob-iphone`
3. Можно фильтровать по клиенту, смотреть статистику, применять блокировки и т.п.