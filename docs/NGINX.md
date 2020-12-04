
```
sudo apt update
sudo apt install nginx
sudo systemctl enable nginx
sudo /etc/init.d/nginx start
sudo /etc/init.d/nginx status
```


# Acessando o servidor WSL2

https://docs.microsoft.com/pt-br/windows/wsl/wsl-config#configure-per-distro-launch-settings-with-wslconf

Eu criei o arquivo **wsl.conf** dentro do diretório /etc do linux wsl2:

```ini
# Enable extra metadata options by default
[automount]
enabled = true
root = /windir/
options = "metadata,umask=22,fmask=11"
mountFsTab = false

# Enable DNS – even though these are turned on by default, we'll specify here just to be explicit.
[network]
generateHosts = true
generateResolvConf = true
```

# Permissões

Crie o usuário ubuntu:

```
sudo adduser ubuntu
```

Coloque ele no grupo www-data:

```
sudo usermod -aG www-data ubuntu
```

```
sudo chown -R ubuntu:www-data /var/www/html
```


Adicionando meu usuário ao grupo sudo:

```
sudo usermod -aG sudo mpi
```