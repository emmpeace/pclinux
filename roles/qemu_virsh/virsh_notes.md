
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


references:
https://documentation.ubuntu.com/public-images/public-images-how-to/launch-with-libvirt/
https://www.redhat.com/en/blog/build-VM-fast-ansible
https://www.redhat.com/en/blog/build-lab-quickly

---

This worked on ubuntu 24
Ref: https://documentation.ubuntu.com/public-images/public-images-how-to/launch-with-libvirt/

cp noble-server-cloudimg-amd64.img my_noble.img

cat > user-data.yaml <<EOF
#cloud-config
password: password
chpasswd:
  expire: False
ssh_pwauth: True
EOF

cat user-data.yaml

cloud-localds my_noble_seed.img user-data.yaml

qemu-system-x86_64  \
  -cpu host -machine type=q35,accel=kvm -m 2048 \
  -nographic \
  -netdev id=net00,type=user,hostfwd=tcp::2222-:22 \
  -device virtio-net-pci,netdev=net00 \
  -drive if=virtio,format=qcow2,file=my_noble.img \
  -drive if=virtio,format=raw,file=my_noble_seed.img

sudo cp my_noble.img /var/lib/libvirt/images/ub_01.qcow2

sudo virt-install --name ub_01 \
--memory 2048 \
--vcpus 2 \
--import \
--disk path=/var/lib/libvirt/images/ub_01.qcow2,size=10 \
--network network=default \
--osinfo generic \
--graphics none \
--console pty,target_type=serial
