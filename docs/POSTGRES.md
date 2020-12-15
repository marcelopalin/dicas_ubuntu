
O PostgreSQL, ou Postgres, é um sistema de gerenciamento de banco de dados RELACIONAL que fornece uma implementação da linguagem de consulta SQL. 
É uma escolha popular para muitos projetos pequenos e grandes e tem a vantagem de ser compatível com os padrões e ter muitos recursos avançados, 
como transações confiáveis ​​e simultaneidade **SEM BLOQUEIOS DE LEITURA**.

## Resumo da Instalação do Postgresql 11

Before adding repository content to your Ubuntu 20.04/18.04/16.04 system, you need to import the repository signing key:

```
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
```
After importing GPG key, add repository contents to your Ubuntu 20.04/18.04/16.04 system:

```
RELEASE=$(lsb_release -cs)
echo "deb http://apt.postgresql.org/pub/repos/apt/ ${RELEASE}"-pgdg main | sudo tee  /etc/apt/sources.list.d/pgdg.list

```
sudo apt update
sudo apt -y install postgresql-11
sudo /etc/init.d/postgresql start
sudo netstat -plunt | grep postgres
sudo -u postgres psql

sudo locale-gen pt_BR.UTF-8
sudo dpkg-reconfigure locales
sudo update-locale LANG=pt_BR.UTF-8

postgres=# create user myuser with encrypted password '@myuserpass';
postgres=# grant all privileges on database myuser to myuser;

GRANT ALL ON ALL TABLES IN SCHEMA public TO myuser;
GRANT ALL ON ALL TABLES IN SCHEMA authentication TO myuser;

## Não funcionou

CREATE DATABASE "mydb" WITH OWNER "myuser" ENCODING 'UTF8' LC_COLLATE = 'pt_BR.UTF-8' LC_CTYPE = 'pt_BR.UTF-8' TEMPLATE template0;

## funcionou
CREATE DATABASE "site-sanic" WITH OWNER "ampere" ENCODING 'UTF8' TEMPLATE template0;

## Resumo da instalação do Postgresql 12

```
sudo apt update
sudo apt install postgresql postgresql-contrib
sudo systemctl enable postgresql
sudo service postgresql status
sudo netstat -plunt | grep postgres

sudo -u postgres psql
```



# 1. Etapa 1 - Instalação do PostgreSQL

Os repositórios padrão do Ubuntu contêm pacotes Postgres, então você pode instalá-los usando o apt sistema de empacotamento.

Se você não fez isso recentemente, atualize o índice de pacotes local do seu servidor:

```
sudo apt update
```

Em seguida, instale o pacote Postgres junto com um -contrib pacote que **adiciona alguns utilitários e funcionalidades** adicionais:

```
sudo apt install postgresql postgresql-contrib
```

Agora que o software está instalado, podemos ver como ele funciona e como pode ser diferente de outros sistemas de gerenciamento de banco de dados relacional que você possa ter usado.


# 2. Verificar se o Serviço está rodando e Habilitar para inicializar automaticamente

Para habilitar a inicialização do serviço do Postgres:

```
sudo systemctl enable postgresql
sudo /etc/init.d/postgresql start
```

Para verificar o status:

```
sudo service postgresql status
sudo netstat -plunt | grep postgres
```


# 3. Etapa 2 - Uso de funções (Roles) e bancos de dados PostgreSQL

Por padrão, o Postgres usa um conceito chamado "funções" "Roles" para lidar com a autenticação e autorização. Estas são, de certa forma, semelhantes às contas regulares do estilo Unix, mas o **Postgres não faz distinção entre usuários e grupos** e, em vez disso, prefere o termo mais flexível “função”.

Após a instalação, o Postgres é configurado para usar autenticação **ident**, o que significa que associa as funções do Postgres a uma conta de sistema Unix / Linux correspondente. Se houver uma função no Postgres, um nome de usuário Unix/Linux com o mesmo nome é capaz de entrar como essa função.

O procedimento de instalação criou uma conta de usuário chamada **postgres** que está associada à função Postgres padrão. Para usar o Postgres, **você pode entrar nessa conta**.

Existem algumas maneiras de utilizar essa conta para acessar o Postgres.

Mudando para a conta postgres
Alterne para a conta postgres em seu servidor digitando:

```
sudo service postgresql status
sudo -i -u postgres
```

Pronto, você está no prompt de comando do Postgres!

```
psql (12.5 (Ubuntu 12.5-0ubuntu0.20.04.1))
Type "help" for help.

postgres=#
```

A partir daí, você está livre para interagir com o sistema de gerenciamento de banco de dados conforme necessário.

# 4. Saia do prompt do PostgreSQL digitando:

```
\q
```
Isso o levará de volta ao postgres prompt de comando do Linux.

# 5. Acessando o prompt em um único comando

```
sudo -u postgres psql
```

Veja que isto exigirá sua senha de administrador do linux.


# 6. Criar usuario e senha

```
sudo -u postgres psql
postgres=# create database mydb;
postgres=# create user myuser with encrypted password 'mypass';
postgres=# grant all privileges on database mydb to myuser;
```


# 7. Criar um banco de dados pelo terminal

```
createdb -U username -E utf8 dbname -h localhost

```

# 8. Criar um banco de dados no console do PostgreSQL (psql)

```
create database dbname with owner=postgres encoding='utf8';
```

# 9. Renomear um banco de dados

```
alter database "old_name" rename to "new_name";
```

# 10. Apagar um banco de dados

```
drop database dbname;
```
# 11. Dump (backup) de um banco de dados

```
pg_dump dbname -h localhost -U postgres > backup.sql
```

# 12. Restauração de um banco de dados (a partir de um arquivo SQL)

```
psql dbname -h localhost -U postgres < backup.sql
```

# 13. Dump (backup) dos usuários de um banco de dados

```
pg_dumpall -g -U postgres -h localhost > users.sql
```

# 14. Comandos especiais em queries SQL

Data:

```
select (current_date + integer '7') as nome_campo;
```

# How to Uninstall Postgresql

You can use the apt-get command to completely remove PostgreSQL on a Debian-based distribution of Linux such as Linux Mint or Ubuntu:

```
sudo apt-get --purge remove postgresql
sudo apt-get purge postgresql*
sudo apt-get --purge remove postgresql postgresql-doc postgresql-common
```

Grep for all PostgreSQL packages in Debian Linux
You can use the dpkg command for managing Debian packages, in conjunction with grep, to search for all the package names installed that contain the sub-string postgres. An example of this command is shown below:

```
dpkg -l | grep postgres
```

Finally, make sure to use the APT-GET repository’s --purge remove command, followed by the postgres package name. This command will remove the package and purge all the data associated with it:


sudo apt-get --purge remove {POSTGRESS-PACKAGE NAME}

Remove all of the PostgreSQL data and directories
Use the rm command with the -rf options to recursively remove all of the directories and data for the postgresql packages:


```
sudo rm -rf /var/lib/postgresql/
sudo rm -rf /var/log/postgresql/
sudo rm -rf /etc/postgresql/
```

