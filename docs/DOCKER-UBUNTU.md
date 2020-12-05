# INSTALAÇÃO DO DOCKER NO UBUNTU

https://www.digitalocean.com/community/tutorials/how-to-install-docker-compose-on-ubuntu-20-04-quickstart

Atenção:

Se estiver utilizando o Ubuntu dentro do Windows com WSL2 o docker não precisará ser instalado.


Mais informações em:

[Leia](docs/WSL2.md)


# Resumo

https://linuxhint.com/install_configure_docker_ubuntu/

sudo apt update

sudo apt install docker.io

sudo systemctl enable --now docker

sudo usermod -aG docker <seu_user>
ou
sudo usermod -aG docker ${USER}

https://www.linuxbabe.com/docker/install-docker-ubuntu

systemctl status containerd

docker --version

Docker version 19.03.13, build 4484c46

sudo docker run hello-world


