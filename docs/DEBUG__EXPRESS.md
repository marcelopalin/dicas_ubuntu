# 1. DEBUG DO PROJETO QUE UTILIZA EXPRESS COM GRAPHQL

- No projeto de refatoração estamos utilizando o Express que gerou um setup

Para depurá-lo é preciso configurar o **launch.json** como:

```json
{
  "version": "0.2.0",
  "configurations": [
      {
          "type": "node", 
          "request": "launch",
          "name": "Node: bin/www",
          "program": "${workspaceFolder}/back/bin/www",
          "restart": true,
          "console": "integratedTerminal",
          "internalConsoleOptions": "neverOpen",
          "env": {
            "NODE_ENV": "development",
            "JWT_SECRET": "JinvDYTjC8IuCbdIeaR8uJR+AaXbrXfp",
            "MONGO_URI": "mongodb://127.0.0.1:27017/gestao_clientes",
          },
          "args": [
            "--debug=true"
          ]
      }     
  ]
}
```

Passando as variáveis de ambiente dentro da tag **env**.

Depois, basta clicar no botão de Debug do VSCode e então utilizar o playground
para testar métodos.


# 2. DEBUG PARA ESTE PROJETO QUE NÃO USA O EXPRESS

```json
{
  // Use IntelliSense to learn about possible attributes.
  // Hover to view descriptions of existing attributes.
  // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "launch",
      "name": "Launch Program",
      "skipFiles": [
        "<node_internals>/**"
      ],
      "program": "${workspaceFolder}\\index.js"
    }
  ]
}
```


# 3. JWT TOKEN NO PLAYGROUND

Lembrando que para utilizarmos os métodos que exigem que o usuário esteja logado
você pode executar o método de Login no Playground primeiro, pegar o Token gerado
e colocar na seção HTTP HEADERS

```graphql
{
  "Authorization": "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjVmNzNmZGExOGRhYzI3NTBiODQ2MzMzYyIsInByb2ZpbGVzIjpbInVzZXIiXSwiaWF0IjoxNjAxNDQxNDIxLCJleHAiOjE2MDE3MDA2MjF9.Qlh7tovw5EO3KGJ1Z0qWQKs6S6FjlyXANgMP2ZsB65g"
}
```

