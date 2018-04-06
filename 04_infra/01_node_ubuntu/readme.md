
docker run -it ubuntu:18.04 bash

> check node version. should be higher than 8.0.2

node -v

> check if installed via apt

apt list --installed | grep nodejs

> check npm, node path

> install n package

sudo npm cache clean
sudo npm install n -g

> install npm

sudo n stable

> check installed node

/usr/local/bin/node -v

> remove nodejs npm installed via apt

sudo apt remove nodejs npm

