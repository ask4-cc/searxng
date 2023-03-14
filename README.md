# ask4.cc searxng-docker

Create a new a SearXNG instance for ask4.cc using Docker

1. Update upstream sources
2. Update nameservers

## Deploy Code template

  ```sh
  
  #!/bin/bash
 
  apt-get -y install ufw docker.io docker-compose
  apt-get -y install build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev libsqlite3-dev wget libbz2-dev
  
  wget https://www.python.org/ftp/python/3.10.0/Python-3.10.0.tgz
  tar -xvf Python-3.10.0.tgz
  
  cd Python-3.10.0
   ./configure --enable-optimizations
   make -j 2
   
  
  ufw allow ssh
  ufw enable
  cd /usr/local
  git clone https://github.com/ask4-cc/searxng-docker.git
  cd searxng-docker
  sed -i "s|ultrasecretkey|$(openssl rand -hex 32)|g" searxng/settings.yml
  docker-compose up
  ufw allow https
  docker-compose down
  cp searxng-docker.service.template searxng-docker.service
  systemctl enable $(pwd)/searxng-docker.service
  systemctl start searxng-docker.service
  
  ```
Upgrade
```sh
docker-compose pull
docker-compose down
docker-compose up
```
This is not meant to be used by the general public... 
