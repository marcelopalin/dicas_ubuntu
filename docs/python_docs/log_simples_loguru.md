

[loguru](https://github.com/Delgan/loguru)


Interessante utilizar ele como middleware

https://stackoverflow.com/questions/63400683/python-logging-with-loguru-log-request-params-on-fastapi-app


# Aplicando o Loguru nas Rotas

Tirado de: https://stackoverflow.com/questions/63400683/python-logging-with-loguru-log-request-params-on-fastapi-app

Para aplicarmos o loguru como um middleware de debug
para cada requisição basta alterar o main.py da seguinte maneira:

```python
from starlette.middleware.cors import CORSMiddleware
from fastapi import FastAPI, Request, Depends

import sys
from loguru import logger

logger.remove()
logger.add(sys.stdout, colorize=True, format="<green>{time:HH:mm:ss}</green> | {level} | <level>{message}</level>")

async def logging_dependency(request: Request):
    logger.debug(f"{request.method} {request.url}")
    logger.debug("Params:")
    for name, value in request.path_params.items():
        logger.debug(f"\t{name}: {value}")
    logger.debug("Headers:")
    for name, value in request.headers.items():
        logger.debug(f"\t{name}: {value}")

def create_app():
  
  app = FastAPI()
  # Set all CORS enabled origins
  app.add_middleware(
      CORSMiddleware,
      allow_origins=["*"],
      allow_credentials=True,
      allow_methods=["*"],
      allow_headers=["*"],
  )  
  
  setup_routes(app)
  return app

def setup_routes(app):
    """Register routes."""
    from app.api.routes import views
    from app.core import auth
    
    app.include_router(auth.router, dependencies=[Depends(logging_dependency)])
    app.include_router(views.router, dependencies=[Depends(logging_dependency)])

```

Após acessar qualquer uma das rotas 
a saída será por exemplo uma chamada na rota http://localhost:8000/api/15 passando o parâmetro 15.

```ini
INFO:     127.0.0.1:41580 - "GET /service-worker.js HTTP/1.1" 404 Not Found
15:04:24 | DEBUG | GET http://localhost:8000/api/15
15:04:24 | DEBUG | Params:
15:04:24 | DEBUG |      num: 15
15:04:24 | DEBUG | Headers:
15:04:24 | DEBUG |      host: localhost:8000
15:04:24 | DEBUG |      connection: keep-alive
15:04:24 | DEBUG |      accept: application/json
15:04:24 | DEBUG |      authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1YnVudHUiLCJleHAiOjY4NjQwNTU0MjZ9.Ljz3NvNx_5ZO4DMi3GiOTDEK4MiRGW-fX1huU8TXG58
15:04:24 | DEBUG |      user-agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.88 Safari/537.36
15:04:24 | DEBUG |      sec-fetch-site: same-origin
15:04:24 | DEBUG |      sec-fetch-mode: cors
15:04:24 | DEBUG |      sec-fetch-dest: empty
15:04:24 | DEBUG |      referer: http://localhost:8000/docs
15:04:24 | DEBUG |      accept-encoding: gzip, deflate, br
15:04:24 | DEBUG |      accept-language: pt-BR,pt;q=0.9,en-US;q=0.8,en;q=0.7,da;q=0.6
15:04:24 | DEBUG |      cookie: session=335f15b8fed948fbbb7697bfaae6b7fd
INFO:     127.0.0.1:41582 - "GET /api/15 HTTP/1.1" 200 OK
INFO:     127.0.0.1:41584 - "GET /service-worker.js HTTP/1.1" 404 Not Found
```
