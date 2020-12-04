# PRE COMMIT

https://pre-commit.com/

https://ljvmiranda921.github.io/notebook/2018/06/21/precommits-using-black-and-flake8/

# Automate Python workflow using pre-commits: black and flake8

Antes de enviar meus arquivos Python testados, formate meu código com black e verifique minha conformidade com o PEP8 usando Flake8. Se tudo passar, o commit é feito. Caso contrário, realizo as edições necessárias e executo commit novamente. Menos tempo é gasto na formatação do código para que eu possa me concentrar mais na lógica do código.

Eu gosto de fazer revisões de código. Eles me permitem aprender com o código de outras pessoas ao mesmo tempo em que oferecem a oportunidade de ensinar o que sei. No entanto, ainda há algumas coisas que desejo melhorar ao facilitar as revisões em meus projetos de código:

- Menos tempo comentando sobre o formato do código e mais tempo discutindo a lógica do código
- Menos incômodo identificando erros de formato ("você pode realmente ver aquele espaço em branco à direita na linha 76?")
Pare de soar minucioso (“Por favor, coloque duas linhas em branco entre as definições de função”)
- Se eu pudesse automatizar os processos acima e remover o humano no loop, poderíamos nos concentrar mais na lógica e na implementação do código.

Uma boa prática, eu aprendi sobre Git Hooks https://git-scm.com/book/gr/v2, especificamente ganchos pré-commit. Ele permite que você execute automaticamente um pequeno script antes de iniciar commit. Este script pode ser uma ferramenta de verificação ou um formatador. Se o script for aprovado, o commit é feito, caso contrário, o commit é negado.

![Pipeline](precommit_pipeline.png)


Discutiremos primeiro a pre-commit estrutura e, em seguida, adicionarei os componentes um por um: primeiro é black e depois flake8. Vou mostrar os dotfiles presentes em meu projeto, então fique à vontade para adotá-los no seu!

## Pré-commit

Podemos executar arquivos shell tudo o que quisermos para ditar como nosso processo de pré-confirmação será, mas esta estrutura de pré-confirmação escrita em Python nos ajudou. Ele ainda vem com um conjunto de ganchos pré-consolidados fora da caixa (baterias incluídas!). Para adotar pre-commit em nosso sistema, simplesmente realizamos as seguintes ações:

(Serão feitos no arquivo pipenv.md quando criamos o ambiente virtual)

1) Instale o pré-commit: pip install pre-commit

2) Adicionar pre-commit a requirements.txt (ou requirements-dev.txt)

3) Defina **.pre-commit-config.yaml** com os ganchos que deseja incluir.

4) Execute **pre-commit install** para instalar git hooks em seu .git/ diretório.

O arquivo YAML configura as fontes de onde os ganchos serão retirados. No nosso caso, o flake8 já foi incluído neste projeto, então só precisamos especificar seu id. Por outro lado, precisamos definir onde obter a fonte black usando algumas linhas de código. Abaixo está um .pre-commit-config.yaml arquivo de amostra que uso em meu projeto:

Tudo isto também é explicado em https://pre-commit.com/

E as configurações do pre-commit também estão explicadas nos sites:
https://github.com/psf/black

.pre-commit-config.yaml de exemplo, mas que será alterado no arquivo
pipenv.md.

```yml
repos:
-   repo: https://github.com/ambv/black
    rev: stable
    hooks:
    - id: black
      language_version: python3
-   repo: https://gitlab.com/pycqa/flake8
    rev: 3.7.9
    hooks:
    - id: flake8
```

# O formatador de código Black

O formatador de código Black em Python é uma ferramenta opinativa que formata seu código da melhor maneira possível. Você pode verificar suas decisões de design no próprio repositório. Algumas decisões de formatação notáveis, em minha opinião:

- Ao contrário do PEP8, o comprimento do código é de 88 caracteres, não 79.
- Uso de aspas duplas em vez de aspas simples em strings.
- Se houver muitos argumentos de função, cada argumento será quebrado por linha.

Prefiro manter o comprimento recomendado de 79 caracteres. Que bom, eles têm uma opção para fazer isso. Só preciso configurar meu pyproject.toml para line-length=79 e está tudo pronto. Este é meu .toml arquivo para configuração black:

pyproject.toml

```toml
[tool.black]
line-length = 79
include = '\.pyi?$'
exclude = '''
/(
    \.git
  | \.hg
  | \.mypy_cache
  | \.tox
  | \.venv
  | _build
  | buck-out
  | build
  | dist
)/
'''
```

Se você não é fã do preto, sempre existe autopep8 - um formatador mais fiel ao PEP8. Boa coisa, o framework de pré-commit já tem um gancho nesta ferramenta, então não há necessidade de fonte de outro repositório.


# Flake8 Checker

Flake8 é uma ferramenta poderosa que verifica a conformidade do nosso código com PEP8. Para que o preto funcione bem com o flake8 (ou evite que ele emita vários erros e avisos), precisamos listar alguns códigos de erro a serem ignorados. Você pode verificar minha .flake8 configuração abaixo:


```ini
[flake8]
ignore = E203, E266, E501, W503, F403, F401
max-line-length = 79
max-complexity = 18
select = B,C,E,F,W,T4,B9
```

Pronto!

Agora siga as instruções descritas em pipenv.md para criarmos o arquivo
.pre-commit-config.yaml.


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
    rev: 20.8b1
    hooks:
    - id: black
      language_version: python3.8

-   repo: https://github.com/pycqa/isort
    rev: 5.6.4
    hooks:
    -  id: isort

-   repo: https://gitlab.com/pycqa/flake8
    rev: 3.8.4
    hooks:
    - id: flake8

-   repo: https://github.com/pre-commit/mirrors-autopep8
    rev: v1.5.4
    hooks:
    - id: autopep8
      name: autopep8-default
      entry: autopep8
      language: python
      'types': [python]
      args: ["-i"]
      require_serial: false
      additional_dependencies: []
      exclude: .*/tests/.*

-   repo: https://github.com/pre-commit/mirrors-autopep8
    rev: v1.5.4
    hooks:
    - id: autopep8
      name: autopep8-unit-tests
      entry: autopep8
      language: python
      'types': [python]
      args: ["-i", "--ignore=E226,E24,W50,W690,E402"]

-   repo: git://github.com/pre-commit/pre-commit-hooks
    rev: v3.3.0
    hooks:
    -   id: trailing-whitespace
    # ensures files are either empty or end with a blank line
    -   id: end-of-file-fixer
    -   id: mixed-line-ending
        args: ['--fix=lf']
        description: Forces to replace line ending by the UNIX 'lf' character.
    # valid python file
    -   id: check-ast
    # Add # -*- coding: utf-8 -*- to the top of python files.
    -   id: fix-encoding-pragma
        args: ['--remove']
    # fix requirements.txt
    # Sorts entries in requirements.txt and removes incorrect pkg-resources==0.0.0
    -   id: requirements-txt-fixer
    # Limitando o tamanho de arquivos
    - id: check-added-large-files
      args: ['--maxkb=1024']
    - id: check-yaml
    # Check for debugger imports and py37+ `breakpoint()` calls in python source
    - id: debug-statements
    # Check for files that contain merge conflict strings.
    - id: check-merge-conflict
    # Checks a common error of defining a docstring after code.
    - id: check-docstring-first

- repo: https://github.com/myint/docformatter
  rev: v1.3.1
  hooks:
    - id: docformatter
      args: [--in-place]

# -   repo: local
#     hooks:
#       - id: pytest
#         name: Check pytest unit tests pass
#         entry: pipenv run pytest
#         pass_filenames: false
#         language: system
#         types: [python]
#       - id: mypy
#         name: Check mypy static types match
#         entry: pipenv run mypy python_starter --ignore-missing-imports
#         pass_filenames: false
#         language: system
#         types: [python]

```