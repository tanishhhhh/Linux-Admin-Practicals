
# Practical 02
# Aim: Working with Users, Groups, and Permissions

1. **Adding a User:**
   ```bash
   sudo useradd john
   ```

2. **Setting a Password:**
   ```bash
   sudo passwd john
   ```

3. **Changing User Details (e.g., changing home directory):**
   ```bash
   sudo usermod -d /new/home/directory john
   ```

4. **Deleting a User:**
   ```bash
   sudo userdel john
   ```

5. **Adding a Group:**
   ```bash
   sudo groupadd developers
   ```

6. **Adding a User to a Group:**
   ```bash
   sudo usermod -aG developers john
   ```

7. **Changing Group Ownership:**
   ```bash
   sudo chgrp developers file_or_directory
   ```

8. **Changing File Permissions:**
   ```bash
   sudo chmod 644 file.txt
   ```

9. **Viewing File Permissions:**
   ```bash
   ls -l file.txt
   ```
   










# Practical 03
# Aim: Initial settings: 

1. **Add a User:**
   ```bash
   sudo useradd zoro
   ```

2. **Network Settings - Change to Static IP Address:**
   ```bash
   sudo nmcli connection modify eth0 ipv4.method manual ipv4.addresses 192.168.1.100/24 ipv4.gateway 192.168.1.1 ipv4.dns 8.8.8.8
   ```

3. **Disable IPv6 if not needed:**
   Edit the `/etc/sysctl.conf` file and add the following lines:
   ```bash
   sudo nano /etc/sysctl.conf
   net.ipv6.conf.all.disable_ipv6 = 1
   net.ipv6.conf.default.disable_ipv6 = 1
   sudo sysctl -p
   ```

4. **Configure Services:**
   Start a service (e.g., Apache HTTP Server):
```
 service httpd start
  service httpd stop
```

5. **Display the List of Services that are Running:**
   ```bash
   sudo systemctl list-units --type=service --state=running
   OR
   sudo chkconfig --list
   ```

6. **Stop and Turn OFF Auto-Start Setting for a Service if You Don’t Need It:**
   ```bash
   sudo systemctl stop httpd
   sudo systemctl disable httpd

   OR

   service http stop
   sudo chkconfig httpd off

   ```

7. **Sudo Settings:**
   ```bash
   sudo nano /etc/sudoers
   zoro ALL=(ALL:ALL) ALL
   ```









# Practical 0?
# Aim: Testing basic commands: 

```
ifconfig
vim /vi
hostname
chmod 
mkdir
ls 
ls -a
cat
```

# Practical 04
# Aim: SSH Server

```
sudo yum install openssh-server
sudo service sshd start
sudo chkconfig sshd on
sudo vi /etc/ssh/sshd_config
PasswordAuthentication yes
sudo service sshd restart
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
sudo service iptables save
ssh john@localhost
```

# Practical 05
# Aim: Vsftpd and FTP 
```
//Installation
Goto packages in RHEL disc (Most IMPORTANT)
#rpm –qa | grep vsftpd
#rpm – ivh vsftpd*
#rpm –ivh ftp*
#rpm –qa | grep ftp 
#rpm –qa | grep vsftpd
# chkconfig vsftpd on
# cd /var/ftp/pub/ 
#cat > ftpfile
#ifconfig 
#vi /etc/vsftpd/vsftpd.conf
Uncomment anonymous _enable = YES (line 12)
Uncomment local_enable = YES  (line 15)
Uncomment anonymous_upload_enable = YES  (line 27) 
Uncomment listen = YES (line 109)
#service vsftpd restart
ftp 192.168.1.3
username: anonymous
password: blank (not a word)
ftp> ls –a
bye

//Configuration
#getsebool –a | grep ftp
#setsebool –P allow_ftp_annon_write on or = 1
#getsebool –a | grep ftp
#getsebool –a | grep ftp
#setsebool –P ftp_home_dir on
#getsebool –a | grep ftp
#ls –ldZ /var/ftp/pub
#chgrp ftp /var/ftp/pub
#chown ftp /var/ftp/pub
#ls –ldz /var/ftp/pub
#cd /var/ftp/pub
#touch T1 T2 T3
#cat > ftptest
service vsftpd start
#service vsftpd restart
#chkconfig vsftpd on
#chkconfig –list | grep vsftpd
#vi /etc/vsftpd/vsftpd.conf

i) Go to directive anonymous _enable = YES and make it anonymous
_enable = NO.
ii) Go to directive anonymous_upload_enable = YES and make it
anonymous_upload_enable = NO.
#service vsftpd restart
#ftp 192.168.1.3
#useradd T1
#passwd T1
#useradd T2
#passwd T2
ftp>pwd
ftp>ls
ftp>bye
#service vsftpd restart.
#vi /etc/vsftpd/user_list
add T1
service vsftpd restart
#cd /home
#pwd
#cd T2
#pwd
#cat > test.txt
hi... this file is created by T2.
#ftp 192.168.1.1
ftp> get test.txt





```



# Practical 07
# Aim: DHCP

```
#rpm –qa dhcp 
#cd /media/RHEL/Package
#rpm –ivh dhcp* 
#rpm –qa | grep dhcp
#hostname
#setup
//Then a dialog box will open up:
-> setup
-> network configuration
-> device configuration
-> eth0
-> Enter ip address, mask, remove *
-> ip:192.168.1.3, msk:255.255.255.0
-> save and quit 
#ifdown eth0
#ifup eth0
#vi /etc/dhcp/dhcpd.conf
#cp /usr/share/doc/dhcp/dhcpd.conf.sample /etc/dhcp/dhcpd.conf
y
#vi /etc/dhcp/dhcpd.conf
:se nu (for showing number line)
Uncomment line no. 18 # authoritative 
Comment Line No 27 and 28 
Also make changes to Line 32
-> Subnet 198.168.1.0 netmask 255.255.255.0 
      {
      Range 192.168.1.10 192.168.1.20; 
      routersrtr-239-0-1.example.org,rtr-239-0-2.example.org 
       }
:wq
#service dhcpd start
#service dhcpd restart
#chkconfig dhcp on
#chkconfig –list dhcp
#service iptables stop
#setenforce 0
```


# Practical 0?
# Aim: Shell Script

```
1] Reverse of a number 

echo "Enter a number:"
read num 

rev=0
rem=0

if [ $num -le 0 ]
then 
    echo "Invalid number" 
    exit 
fi

while [ $num -ne 0 ]
do 
    rem=$((num % 10))
    rev=$((rem + rev * 10))
    num=$((num / 10))
    echo "num = $num"
    echo "rev = $rev"
done 

echo "Reverse number is $rev"
 




2] Decimal to Binary 

echo "Accept number:"
read deci 

bin=0
p=1
rem=0

while [ $deci -gt 0 ]
do 
   rem=$((deci % 2))
   bin=$((bin + rem * p))
   p=$((p * 10))
   deci=$((deci / 2))
done

echo "Binary number is: $bin"


3] Binary to Decimal 

echo "Accept number:"
read deci 

bin=0
p=1
rem=0

while [ $deci -gt 0 ]
do 
   rem=$((deci % 10))
   bin=$((bin + rem * p))
   p=$((p * 2))
   deci=$((deci / 10))
done

echo "Decimal number is: $bin"


4] Decimal to Octal 

echo "Accept number:"
read deci 

if [ $deci -lt 1 ]
then 
    echo "Invalid number" 
    exit 
fi 

bin=0
p=1
rem=0

while [ $deci -gt 0 ]
do 
    rem=$((deci % 8))
    bin=$((bin + rem * p))
    p=$((p * 10))
    deci=$((deci / 8))
done 

echo "Octal number is $bin"



5] Octal to decimal 

 echo "Accept number:"
read deci 
if [ $deci -lt 1 ]
then 
         echo Invalid number 
         exit 
fi 
bin=0
p=1
rem=0
while [ $deci -gt 0 ]
do 
     rem=`expr $deci % 8`
     bin=`expr $bin + $rem \* $p`
     p=`expr $p \* 10`
     deci=`expr $deci \/ 8`
done 
echo "Decimal  number is $bin"
```

# Practical 10
# Aim: Install and configure NFS server.

```
#rpm -qa|grep nfs 
#cd /media/RHEL/disc/packages  (not actual path)
#rpm -ivh nfs*
#ifconfig
#su root
#cd /home 
#mkdir servernfs
#cd servernfs
#vi tanish 
#cat > tanish 
#vi /etc/exports
//In this file make following changes:
home/servernfs * (rw, sync)
#servernfs restart
#service iptables stop
#showmount -e 192.168.1.3
#service vsftpd stop
#service vsftpd status
#chmod -R 777 /home/servernfs/
#cd /home/
#ls
#mkdir clientnfs
#mount -t nfs 192.168.1.3:/homeservernfs/ /home/clientnfs/
#cd clientnfs/
#ls
```


