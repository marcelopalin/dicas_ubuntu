# COMO GERENCIAR DUAS CONTAS GITLAB NO UBUNTU 20.x

Referência:

https://medium.com/uncaught-exception/setting-up-multiple-github-accounts-the-nicer-way-5ab732078a7e

Para conseguir trabalhar com duas ou mais contas do Gitlab no seu S.O é preciso fazer uma configuração.

No diretório docs/git_docs/configs_gitlab_duas_contas
temos os arquivos que devemos copiar para a raíz da pasta do seu usuário linux.

No arquivo docs/git_docs/configs_gitlab_duas_contas/.gitconfig temos a configuração global.

Que determina que o VSCode será utilizado como editor principal e também como ferramenta de diff local e global.

Veja que defini o diretório **work** para conter os projetos do trabalho. E as configurações específicas de chave ficam dentro do arquivo docs/git_docs/configs_gitlab_duas_contas/.gituser-ampere.

No arquivo também contém algumas personalizações de comandos para facilitar a visualização.

Lembrando que você deve utilizar o terminal do Git for Windows para gerar
duas chaves com o comando:

Detalhes em: https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent

```
ssh-keygen -t rsa -b 4096 -C "email@work.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/mpi/.ssh/id_rsa): work_ubuntu_key
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in work_ubuntu_key
Your public key has been saved in work_ubuntu_key.pub
The key fingerprint is:
SHA256:EKorsgJYvEX0jrM/e//FowyH+0VT0Rhoykoplkr0gXE email@work.com
The key's randomart image is:
+---[RSA 4096]----+
|   .ooE      ..+.|
|    ++..    o . o|
| . o..oo o o    .|
|  o.oo=.o o    . |
|...+oo.oS.    o  |
|o ...o  .  . o . |
|+ . .     o . =  |
|oo   .. .  = + . |
|o     o+ .oo=    |
+----[SHA256]-----+
```

As duas chaves, uma com o e-mail pessoal e outra com o e-mail da empresa devem estar salvas
na pasta /home/userfulano/.ssh.

# Atenção:

Não se esqueça de copiar a chave para sua conta no GitLab em configurações - SSH Keys.
Tanto para a conta pessoal quanto para a conta do trabalho.


# Alterando o editor de textos usados no commit e diffs

Quando fazemos um commit, devemos deixar uma mensagem, para isso podemos usar um editor de textos que facilite nossa vida.

Eu costumo utilizar o VSCode, por isso rodaria:

```
git config --global core.editor "code --wait"
```

## Visualizar o gitconfig Global

Para garantir que realmente houveram alterações, podemos rodar o comando que abre as configurações globais do Git no editor de textos e o VS Code irá abrir automágicamente:

```
git config --global -e
```


Neste caso temos as chaves id_rsa_pessoal conforme configurado

No linux, dentro do seu HOME crie o arquivo **.gituser-default**:

```ini
[user]
	name = Marcelo Palin
	email = email@pessoal.com (AQUI COLOQUE O EMAIL QUE GEROU CHAVE PUBLICA DA CONTA PESSOAL)
[core]
	sshCommand = "ssh -i ~/.ssh/id_rsa_pessoal" (AQUI COLOQUE O NOME DA CHAVE PUBLICA DA CONTA PESSOAL)
	editor = code --wait
[alias]
	c = !git add --all && git commit -m
	s = !git status -s
	l = log --graph --decorate --date-order --date=local --date=format:'%y-%M-%d %H:%M:%S' --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %Cgreen(%cd) %C(auto)%d %C(bold blue)<%an>%Creset'  --max-count=10 --abbrev-commit
```

e também o arquivo **.gituser-work**:

```ini
[user]
	name = Marcelo Palin
	email = email@work.com (AQUI COLOQUE O EMAIL QUE GEROU CHAVE PUBLICA DA CONTA PESSOAL)
[core]
	sshCommand = "ssh -i ~/.ssh/id_rsa_work" (AQUI COLOQUE O NOME DA CHAVE PUBLICA DA CONTA DE TRABALHO)
[alias]
	c = !git add --all && git commit -m
	s = !git status -s
	l = log --graph --decorate --date-order --date=local --date=format:'%y-%M-%d %H:%M:%S' --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %Cgreen(%cd) %C(auto)%d %C(bold blue)<%an>%Creset'  --max-count=10 --abbrev-commit
```

No arquivo .gitconfig (git config --global -e) coloque:


```ini
# This is Git's per-user configuration file.
[include]
  path = .gituser-default
[includeIf "gitdir:~/work/"]
  path = .gituser-work
[alias]
	c = !git add --all && git commit -m
	s = !git status -s
	l = log --graph --decorate --date-order --date=local --date=format:'%y-%M-%d %H:%M:%S' --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %Cgreen(%cd) %C(auto)%d %C(bold blue)<%an>%Creset'  --max-count=10 --abbrev-commit
	lall = log --graph --decorate --date-order --date=local --date=format:'%y-%M-%d %H:%M:%S' --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %Cgreen(%cd) %C(auto)%d %C(bold blue)<%an>%Creset' --abbrev-commit

[core]
	autocrlf = input
	editor = code --wait
[user]
	name = Marcelo Palin
	email = email@work.com (AQUI COLOQUE O EMAIL QUE GEROU CHAVE PUBLICA DA CONTA PESSOAL)
# Add this to you gitconfig
# Comment: Start of "Extra Block"
# Comment: This is to unlock VSCode as your git diff and git merge tool
[merge]
    tool = vscode
[mergetool "vscode"]
    cmd = code --wait $MERGED
[diff]
    tool = vscode
[difftool "vscode"]
    cmd = code --wait --diff $LOCAL $REMOTE
# VSCode Difftool
## End of extra block
```


# VERIFICAÇÃO

Entre no diretório ~/work e digite:

```

```

