# /etc/sshd_config options
PermitRootLogin no  
AllowUsers user1 user2  

# List permissions granted by sudo
sudo -l  

# Enumerate files with setuid and setgid bits
find / -user root -perm /4000 -print 2>/dev/null  
find / -type f -perm /04000 -ls 2>/dev/null  
find / -user root -perm /2000 -print 2>/dev/null  
find / -type f -perm /02000 -ls 2>/dev/null  

# Remove setuid bit
chmod u-s /path/to/my/file  

# Remove setgid bit
chmod g-s /path/to/my/file  

# IPTables
sudo iptables -L				# List rules  
sudo iptables -S				# List rules in CLI format (can copy/paste after iptables command)  
sudo iptables -F				# Flush all rules (reverts to default policy)  
sudo iptables -P INPUT ACCEPT	# Set default input policy to ACCEPT  
sudo iptables -P OUTPUT ACCEPT	# Set default output policy to ACCEPT  

# Sane rules for a webserver (change ports for other services)
sudo iptables -I INPUT 1 -i lo -j ACCEPT									# allow all incoming traffic on loopback  
sudo iptables -I OUTPUT 1 -o lo -j ACCEPT									# allow all outgoing traffic on loopback  
sudo iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT	# allow incoming for existing connections  
sudo iptables -A OUTPUT -m conntrack --ctstate ESTABLISHED -j ACCEPT		# allow outgoing for existing connections  
sudo iptables -A INPUT -i eth0 -p tcp -s 10.1.1.0/24 --dport 22 -j ACCEPT	# allow SSH on eth0 from subnet 10.1.1.0/24  
sudo iptables -A INPUT -i eth0 -p tcp --dport 80 -j ACCEPT					# allow HTTP on eth0  
sudo iptables -A INPUT -i eth0 -p tcp --dport 443 -j ACCEPT					# allow HTTPS on eth0  
sudo iptables -A INPUT -j DROP												# default deny to incoming traffic  
sudo iptables -A OUTPUT -j DROP												# default deny to outgoing traffic  

# crontab format: minute hour day-of-month month day-of-week
*/5 * * * * /home/user1/script.sh		# run script.sh every 5 minutes  
