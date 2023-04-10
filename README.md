# OSWP cheat sheets

## WEP attack






















## Connect to AP

### Open
```
sudo iw <interface> connect <ESSID>
sudo dhclient <interface>
```

### WEP
```
sudo iw <interface> connect <ESSID> key 0:<key>
sudo dhclient <interface>
```

### WPA2

Dependencies: wpasupplicant
```
sudo dhclient <interface>
wpa_passphrase <ESSID> <key> | sudo tee /etc/wpa_supplicant.conf
sudo wpa_supplicant -B -c /etc/wpa_supplicant.conf -i <interface>
sudo dhclient <interface>
```

### WPA enterprise

```

sudo dhclient <interface>
```
