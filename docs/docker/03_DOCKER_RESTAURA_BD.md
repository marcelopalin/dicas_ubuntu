Restaurando as Collections de CNPJ e Agentes dentro do Container

winpty docker exec -it mongodb bash

Entre em qualquer pasta e crie a pasta onde copiará os arquivos do host (windows) para o Linux do Docker
Ex: /home/restaurar
2.  Supondo que os arquivos com os backups estão em c:/dev/backups, entre na pasta c:/dev e digite:
docker cp backup/ mongodb:/home/restaurar
Entre novamente no terminal winpty docker exec -it mongodb bash
e veja que os arquivos estão lá, agora basta executar os comandos de restauração:
mongorestore --gzip --nsFrom gestao_db.agentes --nsTo gestao_db.agentes --archive=agentes.gz
mongorestore --gzip --nsFrom gestao_db.cnpjs --nsTo gestao_db.cnpjs --archive=cnpjs.gz