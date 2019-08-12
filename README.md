## Install Docker

sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y  
sudo reboot  
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -  
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"  
sudo apt-get install -y docker-ce  
sudo usermod -aG docker $USER  
  
## Install Docker Compose  
  
sudo curl -L https://github.com/docker/compose/releases/download/1.18.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose  
sudo chmod +x /usr/local/bin/docker-compose  
docker-compose --version  
  
## Make working directory  
  
mkdir ~/sip && cd $_  
  
## extension.conf  
  
vim ~/sip/var/conf/asterisk/extensions.conf  
    
[from-internal]  
exten = 100,1,Answer()  
same = n,Wait(1)  
same = n, Playback(hello-world)  
same = n,Hangup()    
  
### sip.conf  
  
---
[general]  
context=default  
  
[6001]  
type=friend  
context=from-internal  
host=dynamic  
secret=rahasia  
disallow=all  
allow=ulaw  


