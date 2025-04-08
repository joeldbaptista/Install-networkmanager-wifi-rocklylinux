# Install Network Manager Wifi in Rocky Linux

At the time, if we install Rock Linux using the minimal ISO, we end up with a system without Wifi. This is how to install it.

0. Become root
1. Mount Minimal USB:

```bash
mkdir /mnt/usb && mount /dev/sda /mnt/usb
```

2. Create a temp repo (this must be removed afterwards):

```bash
cat > /etc/yum.repos.d/usb.repo <<EOF
[usb]
name=Rocky Linux Installation USB
baseurl=file:///mnt/usb/minimal
enabled=1
gpgcheck=0
EOF
```
**Note** check if NetworkManager is in `/minimal` by running:

```bash
find /mnt/usb -name "Network*"
```

If not, correct `baseurl` in the repo file.

3. Install NetworkManager-wifi:

```bash
dnf --disablerepo=\* --enablerepo=usb install NetworkManager-wifi
```

4. Test

Restart the NetworkManager service (it should be running by now), and then:

```
nmcli d w l
```
It should list the available wifi nets.

5. Connect to wifi.
6. Remove `/etc/yum.repo.d/usb.repo` and umount `/mnt/usb`


