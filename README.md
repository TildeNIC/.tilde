# .tilde

The .tilde TLD project's BIND9 conf files.


# Setting up a .tilde DNS Server

## Debian
Execute the following:
```
sudo apt update
sudo apt -y upgrade
sudo apt -y install bind9 git dnsutils cron bind9utils
cd /var
sudo git clone https://github.com/tildenic/.tilde.git
sudo mv .tilde tilde
cd /var/tilde
sudo cp db.* /etc/bind/
sudo cp named.conf.* /etc/bind/
sudo cp update_dns_zones_ubuntu /etc/bind/
chmod +x /etc/bind/update_dns_zones_ubuntu
Follow the directions on this page: https://wiki.opennic.org/opennic/srvzone
nano /etc/bind/srvzone.conf    (check paths for all programs srvzone requires to function and correct them)
mkdir /etc/bind/opennic
mkdir /etc/bind/opennic/master
mkdir /etc/bind/opennic/slave
sudo systemctl restart bind9
sleep 3
sudo journalctl -xe
```

The last command should tell you if bind9 reloaded successfully, and if it did not.  If it didn't, you'll need to fix the errors it shows you.

To automatically keep zone files updated, execute:
```
crontab -e

```
put the following on a new line in the cron: 
```
*/5 * * * * /etc/bind/update_dns_zones_ubuntu

```

#### To be added to tildenic.org as a public .tilde resolver. Please submit an issue with your ip address information. 
