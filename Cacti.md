# Monitoring with cacti
### Install packages yang diperlukan cacti
```bash
apt install snmp snmpd librrds-perl rrdtool
```
### Install cacti dan cacti spine
```bash
apt install cacti cacti-spine
```
> pada bagian db-common pilih yes
> dan pada bagian mysql masukkan password mariadb
### config pada snmpd nya
```bash
nano /etc/snmp/snmpd.conf
```
> ubah pada bagian agentaddress dan dibawah rocommunity
```bash
agentaddress udp:192.168.2.2:161
rocommunity Nama_bebas 192.168.2.2
```
> Keluar dari file dan restart snmpdnya
```bash
systemctl restart snmpd
```
> Lakukan test dengan cara berikut
```bash
snmpwalk -v2c -c Nama_bebas 192.168.2.2 | head -10
```
### buka cacti di chrome, ip/cacti
> create newa
