# Após instalar o Ubuntu 20.10 será necessário instalarmos o pip3.

Antes de você começar


Python vem em dois sabores; Python 2 e Python 3. A partir do Ubuntu 20.04, Python 3 está incluído na instalação do sistema básico e Python 2 está disponível para instalação no repositório Universe. Os usuários são incentivados a mudar para o Python 3.

Ao instalar um módulo Python globalmente, é altamente recomendável instalar o pacote deb do módulo com a apt ferramenta, pois eles são testados para funcionar corretamente em sistemas Ubuntu. Os pacotes Python 3 são prefixados com python3- e os pacotes Python 2 são prefixados com python2-.

Use pip3 para instalar um módulo globalmente apenas se não houver pacote deb para esse módulo.


Prefira usar pip apenas em um ambiente virtual . Ambientes virtuais Python permitem que você instale módulos Python em um local isolado para um projeto específico, em vez de serem instalados globalmente. Dessa forma, você não precisa se preocupar em afetar outros projetos Python.

```
sudo apt update
sudo apt install python3-pip
```

Como usar o Pip


Nesta seção, mostramos alguns comandos básicos úteis do pip. Com o pip, você pode instalar pacotes do PyPI, controle de versão, projetos locais e de arquivos de distribuição. Geralmente, você instalará pacotes do PyPI.

Para visualizar a lista de todos os comandos e opções do pip, digite:

```
pip3 --help
```


Você pode obter mais informações sobre um comando específico usando pip <command> --help. Por exemplo, para obter mais informações sobre o comando de instalação, digite:

```
pip3 install --help
```
