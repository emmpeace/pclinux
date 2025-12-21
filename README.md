# pclinux
my journey from Windows to Linux

So this June 2025 and Windows 10 is coming to its end ... <br>
Like Pewdiepie, My 8 years desktop PC is going to Linux <br><br>

## Notes for this playbook:
1. you will have to set your other partitions in group_vars/all<br>
2. This playbook edit /etc/fstab so please check yours disks settings

## Problems I ran into:
1. Deactivate Bitlocker on my other disk

I had to deactivate bilocker
```
manage-bde -status
manage-bde D: off
```
   
2. EFI is full

I had to get into the bios and delete some secure boot keys that were taking a lot of space.<br>
https://askubuntu.com/questions/1401737/couldnt-create-moklist-volume-full-grub-doesnt-start-at-all<br>


---

## Choices: 
- OS: Lubuntu 24.04<br>

## what i did<br>
- install ansible<br>
https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html#installing-ansible-on-ubuntu<br>
```
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
ansible-galaxy collection install community.docker
```

```
git clone https://github.com/emmpeace/pclinux.git
cd pclinux
ansible-playbook site.yml -K

```
## Note for dvd playing
```
sudo apt install vlc
sudo apt install libdvd-pkg
sudo dpkg-reconfigure libdvd-pkg
```
## Note for bluray playing

```
## install required packages
sudo apt install libaacs0 libbluray-bdj libbluray2

## Download KEYDB.CFG from site below
http://fvonline-db.bplaced.net/fv_download.php?lang=eng
http://fvonline-db.bplaced.net/

## Copy to designated repository
mkdir ~/.config/aacs
cp Downloads/keydb_jpn/keydb.cfg /home/emm/.config/aacs/KEYDB.cfg

```
