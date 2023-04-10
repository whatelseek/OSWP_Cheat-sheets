# OSWP cheat sheets

This cheat sheet based on "WiFi Hacking Mind Map - v1.0 by Jérémy Brun-Nouvion (https://github.com/koutto)"

## Monitoring
```
airodump-ng <interface> --wps --manufacturer --uptime --band abg
```

## WEP attack







## Connect to AP

### Open
```
iw <interface> connect <ESSID>
dhclient <interface>
```

### WEP
```
iw <interface> connect <ESSID> key 0:<key>
dhclient <interface>
```

### WPA2

Dependencies: wpasupplicant
```

wpa_passphrase "<ESSID>" <key> | sudo tee /etc/wpa_supplicant.conf
wpa_supplicant -B -c /etc/wpa_supplicant.conf -i <interface>
dhclient <interface>
```

### WPA enterprise

```
sudo dhclient <interface>
```

## Other
### MAC-spoofing
```
ip link set dev <interface> down
ip link set dev <interface> address <XX:XX:XX:XX:XX:XX>
ip link set dev <interface> up
```
### Prepare Attacker PC (Monitor mode)
```
airmon-ng check kill
airmon-ng start <interface>
```
### Back to normal modee (Managed mode)
```
airmon-ng stop <Monitor interface>
systemctl start wpa_supplicant
systemctl start NetworkManager
```
