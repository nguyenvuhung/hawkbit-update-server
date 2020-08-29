# hawkbit-update-server
1. Prerequsite
* Install docker\
sudo apt-get install docker.io -y \
sudo groupadd docker\
sudo usermod -aG docker $USER
- Reset machine \
newgrp docker 

* Install docker-compose \
sudo curl -L "https://github.com/docker/compose/releases/download/1.25.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose \
sudo chmod +x /usr/local/bin/docker-compose \
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose 
2. Build compose container  \
docker-compose up -d 
