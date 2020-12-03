# INSTALL GOLANG

https://golang.org/dl/

Descompacte no diretório /usr/local

```
sudo tar -C /usr/local -xzf go1.15.5.linux-amd64.tar.gz
```

Edite o arquivo .profile acrescentando a linha:

```
export PATH=$PATH:/usr/local/go/bin
```

Execute o comando:

```
source ~/.profile
```

E verifique a versão:

```
go version
```