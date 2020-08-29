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

- If want to rebuild hawkbit, please git clone https://github.com/nguyenvuhung/hawkbit.git \
and rebuild with below command \
$: docker build . -t "vuhungkt18/hawkbit-update-server:latest-mysql"

3. Start Hawkbit server \
Start with command: \
$: ${Your_IP}:8080 \
Example: http://172.17.0.1:8080 \

4. List all image docker \
docker images -a \
docker rmi ID_Image
