# openmaint_docker

'''bash
sudo apt update
'''

# install docker
'''bash
sudo apt -y install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
sudo apt update
apt-cache policy docker-ce
sudo apt -y install docker-ce
'''

# install docker compose
'''bash
sudo curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
'''

# install openmaint
'''bash
git clone https://github.com/mrhavens/openmaint_docker.git
cd openmaint_docker
docker-compose up -d
'''
