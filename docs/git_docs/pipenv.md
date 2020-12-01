# 1. Um projeto simples para iniciantes em Python

https://medium.com/@cgrinaldi/a-simple-python-starter-project-c71b0e57b929

Sinto-me frequentemente gastando maneira a criação de um projeto Python muito tempo.

Quero começar e codificar minha ideia mais recente - mas primeiro preciso refrescar minha memória sobre a melhor maneira de fazer isso.

Achei que era hora de criar um repositório inicial rápido para um projeto Python 3.7 para que eu pudesse parar de pesquisar no Google e começar a programar.

Nesta postagem dará uma visão geral das seguintes tecnologias usadas neste projeto inicial:
* Pipenv
* Pre-Commit Hooks
* Testing
* Code Formatting
* Type Checking

## 1.1. Pipenv

O Pipenv combina ambientes pip e virtuais em uma única ferramenta que gerencia as dependências do projeto de maneira determinística. Você pode instalar isso via pip.

Este projeto inicial vem com as seguintes dependências de desenvolvimento:

Pytest, pre-commit e mypy.

Instalando Pipenv é indicado usarmos o Pipx

```
python3 -m pip install --user pipx
```
```
pipenv shell
```

Então o arquivo Pipfile foi criado:

```ini
[[source]]
url = "https://pypi.org/simple"
verify_ssl = true
name = "pypi"

[packages]

[dev-packages]

[requires]
python_version = "3.8"
```

Agora você verá que ele criou e ativou o ambiente virtual e se der o comando **pip list**
você verá que o ambiente só possui 3 pacotes instalados:

```
Package    Version
---------- -------
pip        20.2.4
setuptools 50.3.2
wheel      0.35.1
```
Seu prompt indica que o ambiente virtual está ativado:

(fast_api_tutorial) mpi@DESKTOP-4DUQ19F:~/projs_python/tutoriais/fast_api_tutorial$


# 2. Adicionando os Pacotes com Pipenv

Instalando os pacotes apenas para desenvolvimento

```
pipenv install --dev pre-commit
pipenv install --dev pytest
pipenv install --dev mypy
```

Mypy é um verificador de tipo estático opcional para Python que visa combinar os benefícios da tipagem dinâmica (ou "pato") e da tipagem estática

Setup do pre-commit criando o arquivo .pre-commit-config.yaml

```yml
# pre-commit hooks require a user to have installed `pre-commit`:
#   $ pipenv install pre-commit --dev
# Then install the hooks within the repo:
#   $ cd /PATH/TO/base-python3 (or whatever your package is located)
#   $ pre-commit install
# You only need to run the `install` once per repo

# note that you can update the `sha` versions in this file automatically with the command
# `pre-commit autoupdate`
repos:
-   repo: https://github.com/ambv/black
    rev: stable
    hooks:
    - id: black
      language_version: python3.8

-   repo: https://gitlab.com/pycqa/flake8
    rev: 3.7.9
    hooks:
    - id: flake8

-   repo: git://github.com/pre-commit/pre-commit-hooks
    rev: v1.2.3
    hooks:
    -   id: trailing-whitespace
    # ensures files are either empty or end with a blank line
    -   id: end-of-file-fixer
    - id: mixed-line-ending
      args: ['--fix=lf']
      description: Forces to replace line ending by the UNIX 'lf' character.
    # valid python file
    -   id: check-ast
    # validates style (see setup.cfg for options)
    -   id: flake8
    # Add # -*- coding: utf-8 -*- to the top of python files.
    - id: fix-encoding-pragma
      args: ['--remove']
    # validates json
    -   id: pretty-format-json
    # fix requirements.txt
    # Sorts entries in requirements.txt and removes incorrect pkg-resources==0.0.0
    -   id: requirements-txt-fixer

-   repo: local
    hooks:
      - id: pytest
        name: Check pytest unit tests pass
        entry: pipenv run pytest
        pass_filenames: false
        language: system
        types: [python]
      - id: mypy
        name: Check mypy static types match
        entry: pipenv run mypy python_starter --ignore-missing-imports
        pass_filenames: false
        language: system
        types: [python]
```

Agora vamos instalar os ganchos no diretório .git com o comando:

```
pipenv run pre-commit install
```

# 3. O que foi configurado no pre-commit?

## 3.1. Testes

Este projeto inicial usa o Pytest para seus testes. Os ganchos de pré-confirmação executam os testes de unidade para cada confirmação, mas você pode executá-los manualmente com **make test** ou **pipenv run pytest**.

## 3.2.  Formatação de Código
Para a formatação do código, este projeto usa Black e flake8. Isso garante que você possa gastar seu tempo codificando em vez de se preocupar em seguir um guia de estilo específico.

Você não precisa se preocupar em fazer nada aqui - os ganchos de pré-confirmação cuidam da formatação do código.

## Verificação de tipo
Embora não seja obrigatório, este esqueleto do projeto suporta a verificação de tipos declarados. Por exemplo, podemos definir a seguinte função:

```
def greeting(name: int) -> str:
    return f'Hello {name}!'
```

Você notará que este código não funciona de fato porque o nome recebeu um tipo int . Podemos usar mypy para verificar os tipos:

pyenv execute mypy <my_file.py>

E veremos o seguinte erro:
<my_file.py>: 12: erro: Tipos de operando não suportados para + ("str" ​​e "int")

Um gancho de pré-confirmação mypy foi adicionado ao projeto, mas você não é forçado a usar os tipos do Python 3 se não quiser.


# MELHORANDO AS CONFIGURAÇÕES

https://benp44.github.io/blog/posts/pre-commit/
