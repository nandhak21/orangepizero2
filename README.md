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
