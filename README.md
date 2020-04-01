# Автоматическое подключение VPN

Создать файл /etc/systemd/system/openvpn.service (имя файла не принципиально, оно будет соответствовать названию сервиса)
с содержимым

```
[Unit]
Description=Подключение к VPN
Wants=network-online.target
After=network-online.target

[Service]
ExecStart=/usr/sbin/openvpn --config <путь к файлу конфигурации>
Restart=always
KillSignal=SIGINT

[Install]
WantedBy=multi-user.target
```

В файле конфигурации для параметров

```
ca
cert
key
```

указать абсолютные пути

## Запуск

Выполнить команды 

```bash
systemctl enable openvpn.service
systemctl start openvpn.service
```

Проверить сервис командой

```bash
systemctl status openvpn.service
```

или посмотреть лог

```bash
journalctl -u openvpn.service
```

