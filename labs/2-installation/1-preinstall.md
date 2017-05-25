* Check `vm.swappiness` on all your nodes
	```
	$ cat /proc/sys/vm/swappiness
	30
	```
    
	* Set the value to `1` if necessary
		```
		$ sudo sysctl vm.swappiness=1
		vm.swappiness = 1
		```

* Show the mount attributes of all volumes
	```
	$ cat /etc/fstab
	
	#
	# /etc/fstab
	# Created by anaconda on Thu May 25 14:33:26 2017
	#
	# Accessible filesystems, by reference, are maintained under '/dev/disk'
	# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
	#
	/dev/mapper/centos_localhost1-root /                       ext3    defaults,noatime        1 1
	UUID=01385446-d881-4504-8b34-13e0e5ebf5ad /boot                   ext3    defaults        1 2
	/dev/mapper/centos_localhost1-home /home                   ext3    defaults,noatime        1 2
	/dev/mapper/centos_localhost1-swap swap                    swap    defaults        0 0
	```

* Show the reserve space of any non-root, `ext`-based volumes
    * XFS volumes do not maintain reserve space
		```
		$ df -hTl -x xfs
		
		Filesystem                         Type      Size  Used Avail Use% Mounted on
		/dev/mapper/centos_localhost1-root ext3       41G  5.3G   34G  14% /
		devtmpfs                           devtmpfs  1.5G     0  1.5G   0% /dev
		tmpfs                              tmpfs     1.5G  152K  1.5G   1% /dev/shm
		tmpfs                              tmpfs     1.5G  9.0M  1.5G   1% /run
		tmpfs                              tmpfs     1.5G     0  1.5G   0% /sys/fs/cgroup
		/dev/sda1                          ext3      488M  116M  348M  25% /boot
		/dev/mapper/centos_localhost1-home ext3      9.8G   27M  9.2G   1% /home
		tmpfs                              tmpfs     301M   28K  301M   1% /run/user/1000
		```

* Disable transparent hugepage support
	```
	$ echo $'
	#!/bin/bash
	### BEGIN INIT INFO
	# Provides:          disable-transparent-hugepages
	# Required-Start:    $local_fs
	# Required-Stop:
	# Default-Start:     2 3 4 5
	# Default-Stop:      0 1 6
	# Short-Description: Disable Linux transparent huge pages
	# Description:       Disable Linux transparent huge pages, to improve
	#                    database performance.
	### END INIT INFO
	case $1 in
	start)
		if [ -d /sys/kernel/mm/transparent_hugepage ]; then
		thp_path=/sys/kernel/mm/transparent_hugepage
		elif [ -d /sys/kernel/mm/redhat_transparent_hugepage ]; then
		thp_path=/sys/kernel/mm/redhat_transparent_hugepage
		else
		return 0
		fi
	
		echo \'never\' > ${thp_path}/enabled
		echo \'never\' > ${thp_path}/defrag
	
		re=\'^[0-1]+$\'
		if [[ $(cat ${thp_path}/khugepaged/defrag) =~ $re ]]
		then
		# RHEL 7
		echo 0  > ${thp_path}/khugepaged/defrag
		else
		# RHEL 6
		echo \'no\' > ${thp_path}/khugepaged/defrag
		fi
	
		unset re
		unset thp_path
		;;
	esac' | sudo tee /etc/init.d/disable-transparent-hugepages > /dev/null
	```
	
	```
	$ sudo chmod 755 /etc/init.d/disable-transparent-hugepages
	$ sudo chkconfig --add disable-transparent-hugepages
	```
	
	```
	$ sudo mkdir /etc/tuned/no-thp
	
	$ echo '
	[main]
	include=virtual-guest
	
	[vm]
	transparent_hugepages=never' | sudo tee /etc/tuned/no-thp/tuned.conf > /dev/null
	
	$ sudo tuned-adm profile no-thp
	```
	
	```
	$ cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
		always madvise [never]
	$ cat /sys/kernel/mm/redhat_transparent_hugepage/defrag
		always madvise [never]
	```
	
* List your network interface configuration
	```
	$ nmcli device status
	DEVICE       TYPE      STATE      CONNECTION  
	virbr0       bridge    connected  virbr0      
	eno16777736  ethernet  connected  eno16777736 
	virbr0-nic   tap       connected  virbr0-nic  
	lo           loopback  unmanaged  --         
	```
	
	```
	$ ifconfig
	eno16777736: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
			inet 192.168.121.131  netmask 255.255.255.0  broadcast 192.168.121.255
			inet6 fe80::20c:29ff:fe9f:d66c  prefixlen 64  scopeid 0x20<link>
			ether 00:0c:29:9f:d6:6c  txqueuelen 1000  (Ethernet)
			RX packets 625  bytes 330661 (322.9 KiB)
			RX errors 0  dropped 0  overruns 0  frame 0
			TX packets 314  bytes 27954 (27.2 KiB)
			TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
	
	lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
			inet 127.0.0.1  netmask 255.0.0.0
			inet6 ::1  prefixlen 128  scopeid 0x10<host>
			loop  txqueuelen 0  (Local Loopback)
			RX packets 4  bytes 340 (340.0 B)
			RX errors 0  dropped 0  overruns 0  frame 0
			TX packets 4  bytes 340 (340.0 B)
			TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
	
	virbr0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
			inet 192.168.122.1  netmask 255.255.255.0  broadcast 192.168.122.255
			ether 52:54:00:6d:3f:3d  txqueuelen 0  (Ethernet)
			RX packets 0  bytes 0 (0.0 B)
			RX errors 0  dropped 0  overruns 0  frame 0
			TX packets 0  bytes 0 (0.0 B)
			TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
	```
	
* List forward and reverse host lookups using `getent` or `nslookup`
	```
	$ nslookup localhost
	Server:		192.168.121.2
	Address:	192.168.121.2#53
	
	Name:	localhost.localdomain
	Address: 127.0.0.1
	```
	
	```
	$ nslookup 127.0.0.1
	Server:		192.168.121.2
	Address:	192.168.121.2#53
	
	Non-authoritative answer:
	1.0.0.127.in-addr.arpa	name = localhost.
	
	Authoritative answers can be found from:
	127.in-addr.arpa	nameserver = localhost.
	localhost	internet address = 127.0.0.1
	localhost	has AAAA address ::1
	```
	
* Show the `nscd` service is running
	```
	$ sudo yum install nscd
	$ sudo service nscd status
	Redirecting to /bin/systemctl status  nscd.service
	● nscd.service - Name Service Cache Daemon
	Loaded: loaded (/usr/lib/systemd/system/nscd.service; disabled; vendor preset: disabled)
	Active: active (running) since Thu 2017-05-25 17:41:40 CEST; 5s ago
	Process: 5978 ExecStart=/usr/sbin/nscd $NSCD_OPTIONS (code=exited, status=0/SUCCESS)
	Main PID: 5980 (nscd)
	CGroup: /system.slice/nscd.service
			└─5980 /usr/sbin/nscd
	
	May 25 17:41:40 localhost1.localdomain nscd[5980]: 5980 monitoring file `/etc...
	May 25 17:41:40 localhost1.localdomain nscd[5980]: 5980 monitoring directory ...
	May 25 17:41:40 localhost1.localdomain nscd[5980]: 5980 monitoring file `/etc...
	May 25 17:41:40 localhost1.localdomain nscd[5980]: 5980 monitoring directory ...
	May 25 17:41:40 localhost1.localdomain nscd[5980]: 5980 monitoring file `/etc...
	May 25 17:41:40 localhost1.localdomain nscd[5980]: 5980 monitoring directory ...
	May 25 17:41:40 localhost1.localdomain nscd[5980]: 5980 disabled inotify-base...
	May 25 17:41:40 localhost1.localdomain nscd[5980]: 5980 stat failed for file ...
	May 25 17:41:40 localhost1.localdomain nscd[5980]: 5980 Access Vector Cache (...
	May 25 17:41:40 localhost1.localdomain systemd[1]: Started Name Service Cache...
	Hint: Some lines were ellipsized, use -l to show in full.
	```
	
* Show the `ntpd` service is running
	```
	$ sudo systemctl start ntpd
	$ service ntpd status
	Redirecting to /bin/systemctl status  ntpd.service
	● ntpd.service - Network Time Service
	Loaded: loaded (/usr/lib/systemd/system/ntpd.service; disabled; vendor preset: disabled)
	Active: active (running) since Thu 2017-05-25 17:32:20 CEST; 3s ago
	Process: 4964 ExecStart=/usr/sbin/ntpd -u ntp:ntp $OPTIONS (code=exited, status=0/SUCCESS)
	Main PID: 4966 (ntpd)
	CGroup: /system.slice/ntpd.service
			└─4966 /usr/sbin/ntpd -u ntp:ntp -g
	
	May 25 17:32:22 localhost1.localdomain ntpd[4966]: Listen and drop on 1 v6wil...
	May 25 17:32:22 localhost1.localdomain ntpd[4966]: Listen normally on 2 lo 12...
	May 25 17:32:22 localhost1.localdomain ntpd[4966]: Listen normally on 3 eno16...
	May 25 17:32:22 localhost1.localdomain ntpd[4966]: Listen normally on 4 virbr...
	May 25 17:32:22 localhost1.localdomain ntpd[4966]: Listen normally on 5 lo ::...
	May 25 17:32:22 localhost1.localdomain ntpd[4966]: Listen normally on 6 eno16...
	May 25 17:32:22 localhost1.localdomain ntpd[4966]: Listening on routing socke...
	May 25 17:32:23 localhost1.localdomain ntpd[4966]: 0.0.0.0 c016 06 restart
	May 25 17:32:23 localhost1.localdomain ntpd[4966]: 0.0.0.0 c012 02 freq_set k...
	May 25 17:32:23 localhost1.localdomain ntpd[4966]: 0.0.0.0 c011 01 freq_not_set
	Hint: Some lines were ellipsized, use -l to show in full.
	```