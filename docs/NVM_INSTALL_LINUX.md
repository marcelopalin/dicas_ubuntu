# 1. INSTALAÇÃO DO NVM PARA LINUX

https://github.com/nvm-sh/nvm


## Instalação Manual

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
```

Recarregue o shell:

```
source ~/.bashrc
```

Verifique:

```
nvm ls-remote
```

Instale o Node:

```

```

## Instalação por Ansible

Podemos usar o [Ansible](docs/ANSIBLE_AUTOMACAO.md)

```
You can use a task:

- name: nvm
  shell: >
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
  args:
    creates: "{{ ansible_env.HOME }}/.nvm/nvm.sh"
```


# 2. Arquivo .nvmrc

A intenção de usar o NVM é poder ter uma versão do Node.js para cada projeto, mas é muito difícil conseguir lembrar qual a versão foi usada em cada um.

Para isso, basta criar na raiz do projeto um arquivo com o nome **.nvmrc** e colocar dentro dele o número da versão do Node.js que está sendo utilizada nesse projeto, como:

v12.18.3

Com isso, ao abrir o terminal dentro do projeto e executar o comando no linux

```
nvm use
``` 
 
E no Windows (no Bash) use:

```
nvm use `cat .nvmrc`
nvm install `cat .nvmrc`
```

o NVM vai automaticamente encontrar o arquivo .nvmrc e utilizar a versão indicada para este projeto.


## 2.1. LISTAGEM NODEJS

Abra um novo terminal novo:

Arquitetura que estamos trabalhando:

```
nvm arch
System Default: 64-bit.
Currently Configured: -bit.
```
```
C:\Users\marce\Downloads\Documents>nvm list available

| CURRENT | LTS     | OLD STABLE | OLD UNSTABLE |
| ------- | ------- | ---------- | ------------ |
| 13.11.0 | 12.16.1 | 0.12.18    | 0.11.16      |
| 13.10.1 | 12.16.0 | 0.12.17    | 0.11.15      |
| 13.10.0 | 12.15.0 | 0.12.16    | 0.11.14      |
| 13.9.0  | 12.14.1 | 0.12.15    | 0.11.13      |
| 13.8.0  | 12.14.0 | 0.12.14    | 0.11.12      |
| 13.7.0  | 12.13.1 | 0.12.13    | 0.11.11      |
| 13.6.0  | 12.13.0 | 0.12.12    | 0.11.10      |
| 13.5.0  | 10.19.0 | 0.12.11    | 0.11.9       |
| 13.4.0  | 10.18.1 | 0.12.10    | 0.11.8       |
| 13.3.0  | 10.18.0 | 0.12.9     | 0.11.7       |
| 13.2.0  | 10.17.0 | 0.12.8     | 0.11.6       |
| 13.1.0  | 10.16.3 | 0.12.7     | 0.11.5       |
| 13.0.1  | 10.16.2 | 0.12.6     | 0.11.4       |
| 13.0.0  | 10.16.1 | 0.12.5     | 0.11.3       |
| 12.12.0 | 10.16.0 | 0.12.4     | 0.11.2       |
| 12.11.1 | 10.15.3 | 0.12.3     | 0.11.1       |
| 12.11.0 | 10.15.2 | 0.12.2     | 0.11.0       |
| 12.10.0 | 10.15.1 | 0.12.1     | 0.9.12       |
| 12.9.1  | 10.15.0 | 0.12.0     | 0.9.11       |
| 12.9.0  | 10.14.2 | 0.10.48    | 0.9.10       |
```

```
C:\wamp64\www\_2020\GESTAO_CLIENTES>nvm install 12.18.3
Downloading node.js version 12.16.1 (64-bit)...
Complete
Creating C:\Users\marce\AppData\Roaming\nvm\temp

Downloading npm version 6.13.4... Complete
Installing npm v6.13.4...

Installation complete. If you want to use this version, type

nvm use 12.18.3
```

## 2.2. EXECUTE O QUE ELE PEDIU

```
nvm use 12.18.3
node --version
v12.18.3
```

## 2.3. DEIXE DEFINITIVO

```
nvm alias default v12.18.3
default -> v12.18.3
```