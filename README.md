# orangepizero2

## OS Flash

1. Download ubuntu/debian server image from http://www.orangepi.org/downloadresources/
2. Use Rufus/Balena etcher to burn the image.

## Docker installation - issue

`curl -fSL https://get.docker.com -o get-docker.sh` - I carefully omitted silent flag -s since I wanted to know what was happening inside the script. And as I suspected docker installation failed.

`journalctl -u docker` revealed more info on what was causing the issue.

failed to start daemon: Error initializing network controller: error obtaining controller instance: failed to create NAT chain DOCKER: iptables failed - was the issue.

https://forums.docker.com/t/failing-to-start-dockerd-failed-to-create-nat-chain-docker/78269/2 - suggested replacing iptable references.

`sudo update-alternatives --set iptables /usr/sbin/iptables-legacy`

`sudo update-alternatives --set ip6tables /usr/sbin/ip6tables-legacy`

## Assign static ip

1. `ip -c addr show eth0` - Note down private ip assigned by local dhcp server and netmask.
2. Update /etc/network/interfaces as below - `iface eth0 inet dhcp` needs to be changed to `iface eth0 inet static`.
3. And update the private ip and dns info as below.
`address 10.1.1.125`
`netmask 255.0.0.0`
`gateway 10.1.1.1`
`dns-nameservers 1.1.1.1 8.8.8.8`

