# 1. Passo 1 — Instalando o MySQL
No Ubuntu 20.04, é possível instalar o MySQL usando o repositório de pacotes APT. No momento em que este artigo foi escrito, a versão do MySQL disponível no repositório padrão do Ubuntu era a versão 8.0.19.

Para instalar o MySQL, atualize o índice de pacotes em seu servidor se ainda não tiver feito isso:

```
sudo apt update
```

Depois disso, instale o pacote mysql-server:

```
sudo apt install mysql-server
```
Isso instalará o MySQL, mas não solicitará que você defina uma senha ou que faça outras alterações de configuração. Como isso deixa sua instalação do MySQL não segura, abordaremos isso a seguir.

# 2. Passo 2 — Configurando o MySQL

Se quiser novas instalações do MySQL, execute o script de segurança incluído do DBMS. Esse script modifica algumas das opções padrão menos seguras referentes, por exemplo, a logins root remotos e usuários de exemplo.

Antes garanta que o serviço está inicializado:
```
sudo /etc/init.d/mysql start
sudo /etc/init.d/mysql status
```

Agora sim:

```
sudo mysql_secure_installation
```

Isso levará você através de uma série de prompts onde é possível fazer algumas alterações nas opções de segurança de sua instalação do MySQL. O primeiro prompt perguntará se você gostaria de definir o plug-in de validar senha, que pode ser usado para testar a força de sua senha do MySQL.

Caso você escolha configurar o plug-in de validar senha, o script solicitará que você escolha um nível de validação de senha. O nível mais forte — que você seleciona ao digitar 2 — exigirá que sua senha tenha pelo menos oito caracteres de tamanho e inclua uma mistura de caracteres em maiúsculo, minúsculo, numérico e especial:

# 3. Login como Root

Caso não consiga logar com o comando: mysql -u root -p faça:

Para interagir com o servidor MySQL a partir da linha de comando, use o utilitário cliente MySQL que é instalado como uma dependência do pacote do servidor MySQL.

No MySQL 8.0, o usuário root é autenticado pelo auth_socket plug-in por padrão.

O auth_socketplugin autentica usuários que se conectam a partir do localhost arquivo de socket Unix. Isso significa que você não pode se autenticar como root fornecendo uma senha.


Para fazer login no servidor MySQL como o tipo de usuário root:

```
sudo /etc/init.d/mysql start
sudo /etc/init.d/mysql status
```

```
sudo mysql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'senhadobd';
flush privileges;
```

```
Agora você conseguirá logar com: mysql -u root -p
```


# MySQL com WSL2

https://dev.to/hymanzhan/setting-up-wsl-2-for-web-development-3202

O WSL2 funciona como uma máquina virtual e portanto tem seu IP. Abra
o terminal do Windows (não é o CMD - prompt é o terminal novo 2020)
e digite:

```
ip addr | grep eth0
5: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    inet 172.30.125.207/20 brd 172.30.127.255 scope global eth0
```

Veremos que o IP do WSL2 é: 172.30.125.207.

Porém no WSL2 o IP ficou fixo e podemos acessá-lo pelo **localhost**


Como faço para acessar o BD MySQL que está no Linux do WSL2 utilizando minhas IDEs favoritas
no Windows?


## Permitir que seu Banco de Dados MySQL seja acessado de qualquer máquina

**OBS:** um exemplo de utilização é na sua máquina virtual linux para poder ser acessada pelo Windows. Não faça isso nos seus servidores de produção nunca! É totalmente inseguro!

Altere o arquivo:

```bash
/etc/mysql/mysql.conf.d
```

Alterando a linha bind-address para:

```bash
# Instead of skip-networking the default is now to listen only on
# localhost which is more compatible and is not less secure.
bind-address            = 0.0.0.0
```



# 4. Criando Usuário e Banco de Dados


Para criarmos o BD **mydatabase** com o usário **myadmin** e senha: **123456** faça:


CREATE DATABASE mydatabase CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
CREATE USER 'myadmin'@'localhost' IDENTIFIED BY '123456';
GRANT ALL PRIVILEGES ON *.* TO 'myadmin'@'localhost';
CREATE USER 'myadmin'@'%' IDENTIFIED BY '123456';
GRANT ALL PRIVILEGES ON *.* TO 'myadmin'@'%';
flush privileges;
quit;

# Verificando a Porta do Servidor no WSL2

Com o comando: 

```
sudo netstat -plunt
```

Temos a saída:

```
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 127.0.0.1:33060         0.0.0.0:*               LISTEN      7025/mysqld
tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN      7025/mysqld
tcp6       0      0 :::43749                :::*                    LISTEN      584/node
```

ou filtrando temos:

```
sudo netstat -plunt | grep mysql
```

```
mpi@DESKTOP-4DUQ19F:~$ sudo netstat -plunt | grep mysql
tcp        0      0 127.0.0.1:33060         0.0.0.0:*               LISTEN      7025/mysqld
tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN      7025/mysqld
```

# Habilitando o serviço do MySQL para iniciar automaticamente

```
sudo systemctl enable mysql
```


# 5. Formato utf8mb4

Universalmente o conjunto de caracteres chamado utf8 usa o máximo de três bytes por caractere, limitado apenas a caracteres BMP, ou seja, Basic Multilingual Plane.

A partir do MySQL 5.5.3 e MariaDB 10.1.0, o conjunto de utf8mb4 utiliza no máximo quatro bytes por caractere (um byte a mais na codificação), suportando assim os famosos caracteres suplementares (do nosso idioma), e também emojis.

O que se declara no MySQL/MariaDB como utf8 na verdade não o é, e sim apenas parte dele

Para consertar este erro, a partir da versão MySQL 5.5.+ foi implementado o padrão completo (indo de 1 até 4 bytes) e como a equipe já havia usado o nome utf8, optou-se por chamar a nova implementação de utf8mb4.

Resumindo o utf8 do MySQL não é UTF-8, e, o utf8mb4 sim segue totalmente o padrão UTF-8.

# 6. Como fazer um Dump (Backup com Dados) do BD no MySQL


Para quem não está familiarizado o Dump é um backup do BD naquele momento.
Que caso aconteça algum problema no banco ele poderá ser restaurado.

```
mysqldump -uroot -p --default-character-set=utf8mb4 mydatabase > mydatabase.sql
```


# 7. RESTAURANDO BD 

Como restaurar o Dump (backup).


```
mysql -u root -p --default-character-set=utf8mb4 mydatabase < mydatabase.sql

ou 

mysql -u myadmin -p --default-character-set=utf8mb4 mydatabase < mydatabase.sql
```

# 8. Sintaxes para iniciantes

Como executar um Update

```sql
UPDATE voluntarios
SET voluntarios.recrutamento_id = 1
WHERE voluntarios.cod_cpm = "00033085742";
```

```sql
UPDATE mydatabase.voluntarios SET cidadbho_2020db.voluntarios.recrutamento_id = 1 WHERE (cidadbho_2020db.voluntarios.id = 1) 
```


## 8.1. Como remover completamente a instalação do MYSQL do Linux

```bash
sudo apt-get remove --purge mysql*
```

Ou, mais completo:

```bash
sudo apt-get remove --purge mysql-server mysql-client mysql-common -y
sudo apt-get autoremove -y
sudo apt-get autoclean
```