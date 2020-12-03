# Passo 1 — Instalando o MySQL
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

# Passo 2 — Configurando o MySQL

Se quiser novas instalações do MySQL, execute o script de segurança incluído do DBMS. Esse script modifica algumas das opções padrão menos seguras referentes, por exemplo, a logins root remotos e usuários de exemplo.

Execute o script de segurança com o sudo:

```
sudo mysql_secure_installation
```

Isso levará você através de uma série de prompts onde é possível fazer algumas alterações nas opções de segurança de sua instalação do MySQL. O primeiro prompt perguntará se você gostaria de definir o plug-in de validar senha, que pode ser usado para testar a força de sua senha do MySQL.

Caso você escolha configurar o plug-in de validar senha, o script solicitará que você escolha um nível de validação de senha. O nível mais forte — que você seleciona ao digitar 2 — exigirá que sua senha tenha pelo menos oito caracteres de tamanho e inclua uma mistura de caracteres em maiúsculo, minúsculo, numérico e especial:

# Login como Root

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
