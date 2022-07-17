#Free5GC 
#update apt-get
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install git curl

#install gtp5g
git clone https://github.com/free5gc/gtp5g.git
cd gtp5g
make
sudo make install

#install correct version - docker compose
curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
docker-compose --version

# install free5gc docker
git clone https://github.com/free5gc/free5gc-compose.git
cd free5gc-compose
make base
docker-compose build
sudo docker-compose up # Recommend use with tmux to run in frontground
sudo docker-compose up -d # Run in backbround if needed

#drop database
docker exec -it mongodb mongo
> use free5gc
> db.subscribers.drop()
> exit # (Or Ctrl-D)
