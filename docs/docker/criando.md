Compilações Docker reproduzíveis rapidamente com pipenv
pipenv é outra ferramenta que permite manter dependências lógicas (em a Pipfile) e dependências fixas (em a Pipfile.lock). Ele também faz muito mais, por exemplo, gerenciamento virtualenv.

Muito do que ele faz não é relevante para a construção de imagens do Docker, portanto, a maneira fácil de usá-lo em sua construção do Docker é exportar um requirements.txtarquivo. Você pode fazer isso fora da sua compilação do Docker e apenas enviar o arquivo resultante para o controle de versão e usar o Dockerfileacima:

```
pipenv lock --requirements > requirements.txt
```


A vantagem é que você Dockerfilenão precisa saber nada sobre pipenv. Isso exige que você se lembre de regenerar requirements.txttoda vez que atualizar Pipfile.lock.

Como alternativa, você pode fazer a exportação na própria construção:

```yml
FROM python:3.7
RUN pip install pipenv
COPY Pipfile* /tmp
RUN cd /tmp && pipenv lock --requirements > requirements.txt
RUN pip install -r /tmp/requirements.txt
COPY . /tmp/myapp
RUN pip install /tmp/myapp
CMD flask run exampleapp:app

```
Observe que uma configuração melhor, omitida para fins de clareza, faria com que você instalasse de pipenvforma que suas dependências não afetassem seu código, por exemplo, usando um virtualenv para seu código. Se você quiser um Dockerfile de práticas recomendadas e um sistema de construção, dê uma olhada em meu produto Python Containers pronto para produção .
