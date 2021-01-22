# INSTALL GOLANG

https://golang.org/dl/

Baixe:

wget https://golang.org/dl/go1.15.7.linux-amd64.tar.gz


Descompacte no diretório /usr/local

```
sudo tar -C /usr/local -xzf go1.15.7.linux-amd64.tar.gz
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


# Instalando a IDE

Instalando via snap:

```
snap search goland
Name    Version   Publisher   Notes    Summary
goland  2020.3.1  jetbrains✓  classic  A Clever IDE to Go
```

Comando para instalar:

```
sudo snap install goland --classic
```