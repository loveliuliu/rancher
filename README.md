# rancher
rancher scripts to setup an atlassian stack (bitbucket, bamboo, jira, ...) on some vps

## rancher worker nodes setup:
-----------------------------

```bash

curl https://releases.rancher.com/install-docker/17.12.sh | sh

rpm -q container-selinux
sudo yum install selinux-policy-devel
vi virtpatch.te
make -f /usr/share/selinux/devel/Makefile
sudo semodule -i virtpatch.pp
sudo semodule -l


sudo firewall-cmd --state
sudo firewall-cmd --get-active-zones

sudo firewall-cmd --permanent --zone=trusted --add-interface=docker0
sudo firewall-cmd --permanent --zone=trusted --change-interface=docker0

sudo firewall-cmd --zone=trusted --add-port=80/tcp
sudo firewall-cmd --permanent --zone=trusted --add-port=8080/tcp

sudo firewall-cmd --zone=public --permanent --add-rich-rule='rule protocol value="esp" accept'
sudo firewall-cmd --zone=public --permanent --add-rich-rule='rule protocol value="ah" accept'
sudo firewall-cmd --zone=public --permanent --add-port=500/udp
sudo firewall-cmd --zone=public --permanent --add-port=4500/udp

sudo firewall-cmd --permanent --zone=trusted --add-port=500/udp
sudo firewall-cmd --permanent --zone=trusted --add-port=4500/udp
sudo firewall-cmd --permanent --add-service="ipsec"
sudo firewall-cmd --reload

``` 

