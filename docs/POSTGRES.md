
O PostgreSQL, ou Postgres, é um sistema de gerenciamento de banco de dados RELACIONAL que fornece uma implementação da linguagem de consulta SQL. 
É uma escolha popular para muitos projetos pequenos e grandes e tem a vantagem de ser compatível com os padrões e ter muitos recursos avançados, 
como transações confiáveis ​​e simultaneidade **SEM BLOQUEIOS DE LEITURA**.

Resumo

```
sudo apt update
sudo apt install postgresql postgresql-contrib
sudo systemctl enable postgresql
sudo service postgresql status
sudo netstat -plunt | grep postgres

sudo -i -u postgres
postgres@DESKTOP-4DUQ19F:~$ (entrou no prompt do postgres com o usuário padrão chamado postgres)
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
