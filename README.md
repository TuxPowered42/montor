# Description
This program gets list of checks for current host from nagios, puts it into a temp CONFIG_FILE and then runs checks on host directly
It will display it colorful in term of exit code of plugin
exit 0 - Green background
exit 1 - Yellow background
exit 2 - Red background

# Usage
- -s
        Prints nrpe configs which are used for execution of check locally

# Examples
- mon  
check_disk - DISK OK - free space: / 5939 MB (29% inode=99%); /dev 10 MB (100% inode=99%); /run 6140 MB (89% inode=99%);   /dev/shm 14917 MB (100% inode=99%); /run/lock 5 MB (100% inode=99%); /sys/fs/cgroup 14917 MB (100% inode=99%);  
check_load - OK - load average: 7.44, 7.56, 7.41  
check_nofile_limit - OK  
check_ntp_peer - NTP OK: Offset 0 secs  
check_swapping - OK - No swap activity  
...  
![](https://3.downloader.disk.yandex.ru/disk/f423241fa113227243b06d0442e27bd97391bc6309e6f5139abf1739ab673705/56d9ed48/33-bZQkAwxR3vD43Wn86qYVRhGcYkSU5g8WGi2Xq0s-IO9dqVo_okBXajdg-QiCRSdCxIzpNcfhwDeFhp0xfuQ%3D%3D?uid=0&filename=montor.png&disposition=inline&hash=&limit=0&content_type=image%2Fpng&fsize=47770&hid=673f84c5158eb284661b01a7e674503c&media_type=image&tknv=v2&etag=1a287d8d1d61bbb4ee2aeb7ce7d5c274)

- mon -s  
/etc/nagios/nrpe.d/igbase_debian.cfg:command[check_disk] = /usr/lib/nagios/plugins/check_disk -w 15% -c 5% -W 50% -K 5%  
check_disk - DISK OK - free space: / 5938 MB (29% inode=99%); /dev 10 MB (100% inode=99%); /run 6140 MB (89% inode=99%);   /dev/shm 14917 MB (100% inode=99%); /run/lock 5 MB (100% inode=99%); /sys/fs/cgroup 14917 MB (100% inode=99%);  
/etc/nagios/nrpe.d/igbase_debian.cfg:command[check_load] = /usr/lib/nagios/plugins/check_load -w 30,20,15 -c 100,80,50  
check_load - OK - load average: 10.07, 8.34, 7.69  
/etc/nagios/nrpe.d/igbase_debian.cfg:command[check_nofile_limit] = sudo /usr/lib/nagios/igmonplugins/limitcheck.py  
check_nofile_limit - OK  
/etc/nagios/nrpe.d/igsoftware_ntp.cfg:command[check_ntp_peer] = /usr/lib/nagios/plugins/check_ntp_peer -H 127.0.0.1 -w 1 -c 3  
check_ntp_peer - NTP OK: Offset 0 secs  
/etc/nagios/nrpe.d/igbase_debian.cfg:command[check_swapping] = /usr/lib/nagios/igmonplugins/check_linux_swapping.sh  
check_swapping - OK - No swap activity  
...  
![](https://4.downloader.disk.yandex.ru/disk/a34165fd8104c26132572b4c36c3bc621dc892bc7ad05767b4d50710697f9fcd/56d9edec/33-bZQkAwxR3vD43Wn86qa08n28iEWy1oBlI6sTOekrhtVL82sCe-1knurOs90nOA-4XVK3pis4mD5eiRjpWyA%3D%3D?uid=0&filename=montors.png&disposition=inline&hash=&limit=0&content_type=image%2Fpng&fsize=81398&hid=f468e600be4ebc859a69cae6285b2112&media_type=image&tknv=v2&etag=080e5997daf690ce51b89c487e61f8eb)
