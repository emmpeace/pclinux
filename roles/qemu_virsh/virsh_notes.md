
OK, trying to play with guestfs in a VM
1. create VM1 and play with it a lil bit
2. make an image of this VM1
3. create another VM2 
4. mount VM1 image  to VM2
4. check files in VM1 from VM2

commands notes 


```
sudo apt install qemu-kvm virt-manager libvirt-daemon-system libvirt-clients virtinst libosinfo-bin genisoimage cpu-checker guestfs-tools

sudo virt-install --name ubuntu01 \
--memory 2048 \
--vcpus 2 \
--disk path=/var/lib/libvirt/images/ubuntu01.qcow2,size=10 \
--network network=default \
--os-variant ubuntu24.04 \
--graphics none \
--console pty,target_type=serial \
--location /var/lib/libvirt/images/ubuntu-24.04.3-live-server-amd64.iso,kernel=casper/vmlinuz,initrd=/casper/initrd \
--extra-args 'console=ttyS0,115200n8 serial'

sudo virt-install \
--name debian01 \
--memory 2048 \
--vcpus 2 \
--disk path=/var/lib/libvirt/images/debian01.qcow2,size=10 \
--network network=default \
--os-variant debian13 \
--graphics none \
--console pty,target.type=serial \
--location /var/lib/libvirt/images/debian-13.1.0-amd64-netinst.iso \
--extra-args 'console=ttyS0,115200n8 serial'


virsh --connect qemu:///system console debian01

```

mount disk on host
```
virsh attach-disk --config ubuntu01 --source /var/lib/libvirt/images/debian01_cp.qcow2 --target vdb

```
mount disk on guest
```
mount /dev/vdb1 /mnt/vmtest/
```

unmount disk on guest
```
umount /dev/vdb1
```

unmount disk on host
```
virsh detach-disk ubuntu01 vdb
```


bonus 
- virt-sparsify: delete free space from vm disk
guestfs-tools is necessary


```
virt-sparsify --in-place /var/lib/libvirt/images/debian01_cp.qcow2
```

is the drive still usable ? 

it seems like we can use qemu-img with the -c otpion, this will compress the whole disk work only with qcow2
