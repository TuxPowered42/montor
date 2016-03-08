# Description
This program gets list of checks for current host from nagios, puts it into a temp CONFIG_FILE and then runs checks on host directly.  
It will display it colorful in term of exit code of plugin  
- exit 0 - Green background  
- exit 1 - Yellow background  
- exit 2 - Red background  

Confuration file (montor_config) must me located under /etc

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
![](https://raw.githubusercontent.com/leoleovich/images/master/montor.png)

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
![](https://raw.githubusercontent.com/leoleovich/images/master/montors.png)
