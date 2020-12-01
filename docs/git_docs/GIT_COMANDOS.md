# GIT

Livro: https://git-scm.com/book/pt-br/v2


## Para verificar as configurações locais podemos usar o comando:

```
git config --list
```

## Para mostrar o nome de usuário

```
git config --global user.name
```

## Para mostra o email do usuário configurado

```
git config --global user.email
```

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

# Arquivos não monitorados

Se o arquivo foi modificado mas você ainda **não executou** git add, um simples git checkout removerá as alterações, deixando o arquivo como ele estava no último commit.

Passe o nome do arquivo a ter as alterações desfeitas ou . para desfazer as alterações em todos os arquivos modificados. Muito útil se você está apenas experimentando um código mas não quer que ele seja salvo.

```
git checkout .
```

Esse comando não apaga novos arquivos. Para apagar novos arquivos que ainda não foram adicionados ao Stage, execute:

```
git clean -df
```

# Removendo arquivos do Stage

Se você executou git add e quer desfazer, use o reset.

```
git reset
```


# Renomear a mensagem do último Commit

Escreveu algo errado no último commit? Esse comando te permite renomear a mensagem do último commit feito:

```
git commit --amend
```

# Referências

https://woliveiras.com.br/posts/facilitando-os-merges-no-git-com-o-visual-studio-code-como-merge-tool-e-editor-padr%C3%A3o/
