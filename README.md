http://archlinuxarm.org/platforms/armv7/broadcom/raspberry-pi-2


PI 2 Cluster with docker/fleet
=============

http://archlinuxarm.org/platforms/armv7/broadcom/raspberry-pi-2#qt-platform_tabs-ui-tabs2
```bash
hostnamectl set-hostname <hostname>
passwd
```
```bash
pacman -Sy
pacman -S git gcc
pacman -S htop vim ranger
```

# build go
```bash
cd /usr/src
git clone https://go.googlesource.com/go
cd go
git checkout go1.4.1
cd src
./make.bash
```

Create a new file /etc/profile.d/go.sh
```bash
#!/bin/sh
export PATH=$PATH:/usr/src/go/bin/
export GOPATH=/usr/src/spouse
```
now
```bash
chmod +x /etc/profile.d/go.sh
mkdir /usr/src/spouse
```
# Install docker
```bash
pacman -S docker btrfs-progs lxc
systemctl enable docker.service
systemctl enable docker.socket
systemctl start docker.service
systemctl start docker.socket
docker ps  # should be header only (but not returning any error like "dail failed" or "file not found")
```

# Install fleet
```bash
cd /usr/src/
go get golang.org/x/tools/cmd/cover
git clone https://github.com/coreos/fleet.git
cd fleet
./build
./test
ln -s /usr/src/fleet/bin/* /usr/bin/
```

# Create RPI2 arch docker base image
pacman -S extra/arch-install-scripts # pacstrap


# Archlinux docker base image for ARM

https://registry.hub.docker.com/u/jimho/archlinux-arm



