# INSTALAÇÃO DO NVM PARA WINDOWS

# 1. Arquivo .nvmrc

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


# 2. REQUISITOS

Você tenha instalado o GERENCIADOR NVM

## 2.1. NVM NO WINDOWS

Recomendo a instalação do NVM para windows:

https://github.com/coreybutler/nvm-windows

No Linux
https://github.com/nvm-sh/nvm

Na documentação tem o link para os instaladores:
https://github.com/coreybutler/nvm-windows/releases


# 3. ANTES DE INSTALAR O NVM REMOVA O NODE

How to remove Node.js from Windows:
Take a deep breath.

Run npm cache clean --force

Uninstall from Programs & Features with the uninstaller.

Reboot (or you probably can get away with killing all node-related processes from Task Manager).

Look for these folders and remove them (and their contents) if any still exist. Depending on the version you installed, UAC settings, and CPU architecture, these may or may not exist:

C:\Program Files (x86)\Nodejs
C:\Program Files\Nodejs
C:\Users\{User}\AppData\Roaming\npm (or %appdata%\npm)
C:\Users\{User}\AppData\Roaming\npm-cache (or %appdata%\npm-cache)
C:\Users\{User}\.npmrc (and possibly check for that without the . prefix too)
C:\Users\{User}\AppData\Local\Temp\npm-*
Check your %PATH% environment variable to ensure no references to Nodejs or npm exist.

If it's still not uninstalled, type where node at the command prompt and you'll see where it resides -- delete that (and probably the parent directory) too.

Reboot, for good measure.


Cleanup directories
After the uninstall, look for the following folders and delete them if exists
* Nodejs installed directory
  
Abra o Windows Explorer e cole %appdata% e você verá os diretórios npm e npm-cache
* npm and npm-cache directories from %appdata% directory
* npmrc directory from user home directory ( C:\Users\{User} )

## 3.1. INSTALANDO NVM no Windows

Vou instalar a versão 1.1.7 - baixe o .zip e você terá o instalador.

Se o Node estiver instalado na sua máquina ele perguntará várias vezes se
você quer que o NVM controle ele agora.

Foi criado as variáveis de ambiente na área do seu usuário:

NVM_HOME C:\Users\marce\AppData\Roaming\nvm
e
NVM_SYMLINK C:\Program Files\nodejs

## 3.2. LISTAGEM NODEJS

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

## 3.3. EXECUTE O QUE ELE PEDIU

```
nvm use 12.18.3
node --version
v12.18.3
```

## 3.4. DEIXE DEFINITIVO

```
nvm alias default v12.18.3
default -> v12.18.3
```