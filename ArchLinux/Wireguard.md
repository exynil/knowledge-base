## 1. Установка WireGuard

```
apt update
```

```
apt install wireguard wireguard-tools
```

## 2. Генерация приватных и публичных ключей

Сгенерируйте пару приватных и публичных ключей на сервере в папке `/etc/wireguard/` 

```
wg genkey | sudo tee /etc/wireguard/server_private.key | wg pubkey | sudo tee /etc/wireguard/server_public.key
```

Сгенерируйте пару приватных и публичных ключей на клиенте в папке `/etc/wireguard/` 
```
wg genkey | sudo tee /etc/wireguard/client_private.key | wg pubkey | sudo tee /etc/wireguard/client_public.key
```

## 3. Настройка сервера

Включаем переадресацию IP в файле `/etc/sysctl.conf`

```
net.ipv4.ip_forward = 1
```

Применяем изменения

```
sysctl -p
```

Разрешаем входящий UDP-трафик для VPN-соединения

```
ufw allow 51820/udp
```

Find the name of your server’s main network interface. Save it for later use.

Найдите имя основного сетевого интерфейся вашего сервера. Сохраните его для дальнейшего использования

```
ip -c a
```

Создайте файл конфигурации WireGuard на сервере `/etc/wireguard/wg0.conf`

Скопируйте и вставьте приведенный ниже код в файл конфигурации.
Измените значения `PrivateKey` и `PublicKey` своими значениями.
Замените `eth0` на имя своего сетевого интерфейса.

```
# Server configuration
[Interface]
Address = 172.26.3.155/16 # Internal IP address of the VPN server.
ListenPort = 51820
SaveConfig = true
PrivateKey = uE6i2Hdas/mJDN1BaMckKjqDl1E8YNe/MKNyNPIAB1o= # The server_private.key value.

# IP Forwarding. Modify network interface name "eth0"
PostUp = iptables -A FORWARD -i wg0 -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i wg0 -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE

# Client configuration
[Peer]
PublicKey = PMOp3o6JAOnKd6Vjd/220ft1KijsNUVVluXHhWrUpkQ= # The client_public.key value.
AllowedIPs = 172.26.5.67/32
```

Start WireGuard service on the server machine.
Запустите службу WireGuard на сервере

```
systemctl enable --now wg-quick@wg0
```

Проверьте статус службы

```
systemctl status wg-quick@wg0
```

## 4. Настройка клиента

Установите `systemd-resolvconf` на клиент

```
yay -S systemd-resolvconf
```

Запустите службу

```
systemctl enable --now systemd-resolved
```

Создайте конфигурационный файл на машине клиента

```
vim /etc/wireguard/wg-client.conf
```

Скопируйте и вставьте приведенный ниже код в конфигурационный файл.
Измените значения `PrivateKey` и `PublicKey` на свои значения.
Измените Endpoint.

```
# Client configuration    
[Interface]
Address = 172.26.5.67/16 # private IP address of the VPN client.
DNS = 1.1.1.1
PrivateKey = mCyPWpLw5OjepZTjnrTdjYuaRPpIFspbxU6orz5Np3g= # The client_private.key value.

# Server configuration    
[Peer]
PublicKey = Q96urAY8bv6orRwaRWvMpg2GqraYSKr6fZgucmwZFgk= # The server_public.key value.
AllowedIPs = 0.0.0.0/0
Endpoint = 18.116.19.235:51820 # Public IP address of our VPN server and port number (ListenPort in the server configuration).
PersistentKeepalive = 25
```

Запустите службу WireGuard на машине клиента

```
systemctl enable --now wg-quick@wg-client
```

Проверьте статус службы

```
systemctl status wg-quick@wg-client
```


