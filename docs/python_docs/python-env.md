# Variáveis ​​de ambiente com Dotenv em Python

Aconteceu com todos nós que, ao criar um script Python simples para importar dados em nosso banco de dados, precisamos definir os parâmetros de conexão. Normalmente, os parâmetros são diferentes no banco de dados de desenvolvimento e no banco de dados de produção.

De acordo com a metodologia do Twelve-Factor (https://www.12factor.net/config) App, muito ruim se salvar a configuração diretamente no código-fonte. Entre outras coisas, porque você pode estar postando informações confidenciais para olhos curiosos.
É melhor colocá-lo em um arquivo de configuração, mas CUIDADO!… Não inclua este arquivo no repositório. Então, como fazemos isso?

Os aplicativos que dependem de fontes de terceiros para dados, em algum momento, precisarão incluir coisas como tokens OAuth, chaves SSH ou credenciais de API. Isso se torna um problema quando o código do aplicativo é enviado para um controle de origem público, como o GitHub. Uma vez que o código está lá, ele fica acessível a qualquer pessoa que o veja. E assim são suas chaves.


O arquivo .env(Dotenv) vem para auxiliar, em quase todos os idiomas, pode encontrar uma biblioteca ou pacote que torna a sua vida mais fácil. Em Python, o pacote em questão é python-dotenv.

# Como é um arquivo .env?

Pois bem, é um arquivo de texto simples onde, a cada linha, definimos uma variável de ambiente e atribuímos seu valor através do operador =.

```ini
PG_USER = postgres 
PG_PASSWORD = mykey 
supersecret PG_DBNAME = banco de dados 
PG_HOST = servidor 
API_KEY = the_key_supersecret

```

Para não guardar estes dados sensíveis no nosso repositório, é importante adicionar ao .gitignore a entrada do .env, para não perder de vista as variáveis ​​de ambiente que podemos configurar, duplicar o arquivo como .env.sample, sim, sem colocar os valores reais é claro. 

Desta forma, ao baixarmos nosso projeto, bastará copiar o arquivo .env.sample e renomear para .env.

# Muito bom, mas como o usamos?

A primeira coisa será instalar o pacote usando pip

```
pip install python-dotenv
```

No código ficará assim:

``` python
import os
from dotenv import load_dotenv
load_dotenv()
# para usar o valor faça
API_KEY = os.getenv('API_KEY')
```
