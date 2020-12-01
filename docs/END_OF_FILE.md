# Solução

\r\n is a Windows Style
\n is a POSIX Style

\r is a old pre-OS X Macs Style, Modern Mac's using POSIX Style.
\r is a carrige return and \n is a line feed.

A intenção aqui (permitir a edição de arquivos com ferramentas do Windows somente CRLF e garantir que apenas arquivos LF sejam 
confirmados) é mais do que razoável. Na prática, porém, isso é um tanto equivocado e desnecessário.

# Conversão automática leva a casos extremos estranhos

Com a conversão habilitada, os arquivos retirados estão em um estado diferente do repositório de origem. Isso pode levar a erros estranhos em que os artefatos de construção ou arquivos transferidos para outros sistemas são sutilmente diferentes daqueles gerados a partir da fonte não modificada.


# GIT DESATIVE A CONVERSÃO AUTOMÁTICA

**Editores modernos não precisam da conversão**
Pode-se argumentar que casos raros de conversão são aceitáveis ​​para evitar arquivos CRLF acidentalmente confirmados. Isso não é mais válido dado o suporte dos editores modernos para arquivos LF.

Por exemplo, os projetos do Visual Studio podem usar .**editorconfig** para garantir configurações de arquivo consistentes:

#  EditorConfig  é  incrível:  https://EditorConfig.org

Dica:

Utilize minha configuração, basta criar o arquivo .editorconfig na raiz do seu projeto e colar o seguinte conteúdo.

```ini
# EditorConfig is awesome: https://EditorConfig.org

# top-most EditorConfig file
root = true

# Unix-style newlines with a newline ending every file
[*]
end_of_line = lf
insert_final_newline = true

# Matches multiple files with brace expansion notation
# Set default charset
[*.{js,py}]
charset = utf-8

# 4 space indentation
[*.py]
indent_style = space
indent_size = 4

# Tab indentation (no size specified)
[Makefile]
indent_style = tab

# Indentation override for all JS under lib directory
[lib/**.js]
indent_style = space
indent_size = 2

# Matches the exact files either package.json or .travis.yml
[{package.json,.travis.yml}]
indent_style = space
indent_size = 2

[*.yml]
indent_size = 2
```

# Desativando a conversão do final da linha no Git

Execute git config --global core.autocrlf falsep ara desabilitar qualquer conversão automática. Isso coloca o seguinte em sua configuração global do git:

~/.gitconfig:

[core] 
    autocrlf  =  false


[Voltar](README.md)    