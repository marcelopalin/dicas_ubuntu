# 1. DOCKER MONGODB

https://blog.jeremylikness.com/blog/2018-12-27_mongodb-on-windows-in-minutes-with-docker/

Em uma máquina nova caso não queira instalar o MongoDB você pode instalar o Docker e então criar um Container com o MongoDB.

# 2. PASSOS

Requisitos: docker instalado no seu sistema operacional.

Criaremos um volume para persistir os dados caso a máquina reinicie.

```
docker volume create --name=mongodata
```

```
docker run --name mongodb -v mongodata:/data/db -d -p 27017:27017 mongo
```

Acesse o container e crie o BD backteste01db

```
winpty docker exec -it mongodb bash
```

Depois é só chamar o **mongo**

use backteste01db

db.createCollection("info")
db.info.insert( { info: "BD criado para teste com o projeto de refatoração do Backend", date: new Date() } )

Teste:
 db.info.find()
{ "_id" : ObjectId("5f5ce0500c63061c73c0cc1b"), "info" : "BD criado para teste c
om o projeto de refatoração do Backend", "date" : ISODate("2020-09-12T14:50:56.1
98Z") }

E pronto!

# 3. Verificando se está rodando

```
docker ps -a
```

Inicializando:

```
docker start mongodb
```