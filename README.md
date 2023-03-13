# ask4.cc searxng-docker

Create a new a SearXNG instance for ask4.cc using Docker

## Deploy Code template

  ```sh
  
  #!/bin/bash
 
  apt-get -y install ufw docker.io docker-compose
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
