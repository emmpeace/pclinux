commands notes 


```
sudo apt install qemu-kvm virt-manager libvirt-daemon-system libvirt-clients virtinst libosinfo-bin genisoimage cpu-checker


sudo virt-install \
--name debian03 \
--memory 2048 \
--vcpus 2 \
--cdrom /var/lib/libvirt/images/debian-13.1.0-amd64-netinst.iso \
--disk path=/var/lib/libvirt/images/my-debian-vm.qcow2,size=10 \
--network network=default \
--os-variant debian13 \
--graphics none \
--console pty,target.type=serial \
--location /var/lib/libvirt/images/debian-13.1.0-amd64-netinst.iso


sudo virt-install \
--name ubuntu01 \
--memory 2048 \
--vcpus 2 \
--disk path=/var/lib/libvirt/images/ubuntu01.qcow2,size=10 \
--network network=default \
--os-variant ubuntu24.04 \
--graphics none \
--console pty,target.type=serial\
--cdrom /var/lib/libvirt/images/ubuntu-24.04.3-live-server-amd64.iso \
--extra-args 'console=ttyS0,115200n8 serial'


sudo virt-install \
--name debian03 \
--memory 2048 \
--vcpus 2 \
--disk path=/var/lib/libvirt/images/debian03.qcow2,size=10 \
--network network=default \
--os-variant debian13 \
--graphics none \
--console pty,target.type=serial \
--location /var/lib/libvirt/images/debian-13.1.0-amd64-netinst.iso \
--extra-args 'console=ttyS0,115200n8 serial']
```