Tutorial Avançado de Docker: Criando uma Aplicação Web com Banco de Dados e Rede Virtualizada

Este tutorial irá guiá-lo através do processo de criação de uma aplicação web simples em Python usando o Docker Compose. A aplicação usará o framework Flask e manterá um contador de acessos no Redis. Além disso, vamos criar uma rede virtualizada para nossos serviços.

Pré-requisitos

Você precisa ter o Docker Engine e o Docker Compose instalados em sua máquina. Você não precisa instalar Python ou Redis, pois ambos são fornecidos por imagens Docker.

Passo 1: Definindo as Dependências da Aplicação

Crie um diretório para o projeto e dentro dele, crie um arquivo chamado app.py com o seguinte código:

```python
import time
import redis
from flask import Flask

app = Flask(__name__)
cache = redis.Redis(host='redis', port=6379)

def get_hit_count():
    retries = 5
    while True:
        try:
            return cache.incr('hits')
        except redis.exceptions.ConnectionError as exc:
            if retries == 0:
                raise exc
            retries -= 1
            time.sleep(0.5)

@app.route('/')
def hello():
    count = get_hit_count()
    return 'Hello World! I have been seen {} times.\n'.format(count)
```

Crie outro arquivo chamado requirements.txt com o seguinte conteúdo:

```
flask
redis
```


Passo 2: Criando um Dockerfile

O Dockerfile é usado para construir uma imagem Docker. A imagem contém todas as dependências que a aplicação Python requer, incluindo o próprio Python. Crie um arquivo chamado Dockerfile com o seguinte conteúdo:

```Dockerfile
Copy code
# syntax=docker/dockerfile:1
FROM python:3.7-alpine
WORKDIR /code
ENV FLASK_APP=app.py
ENV FLASK_RUN_HOST=0.0.0.0
RUN apk add --no-cache gcc musl-dev linux-headers
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
EXPOSE 5000
COPY . .
CMD ["flask", "run
```


Neste Dockerfile:

-  FROM python:3.7-alpine: Esta linha indica que a imagem base será a imagem Python 3.7 que usa Alpine Linux, uma versão minimalista do Linux.

- WORKDIR /code: Define o diretório de trabalho dentro do container.

- ENV FLASK_APP=app.py e ENV FLASK_RUN_HOST=0.0.0.0: Define variáveis de ambiente usadas pelo comando flask.

- RUN apk add --no-cache gcc musl-dev linux-headers: Instala as dependências necessárias para compilar as dependências Python no Alpine Linux.

- COPY requirements.txt requirements.txt: Copia o arquivo requirements.txt do host para o container.

- RUN pip install -r requirements.txt: Instala as dependências Python listadas no arquivo requirements.txt.

- EXPOSE 5000: Informa ao Docker que o container estará ouvindo na porta 5000.

- COPY . .: Copia o diretório atual (.) do host para o diretório de trabalho atual (.) no container.

- CMD ["flask", "run"]: Define o comando padrão para o container.

Passo 3: Definindo Serviços em um Arquivo Compose

Crie um arquivo chamado docker-compose.yml com o seguinte conteúdo:

```yaml
version: '3'
services:
  web:
    build: .
    ports:
      - "8000:5000"
    networks:
      - webnet
  redis:
    image: "redis:alpine"
    networks:
      - webnet

networks:
  webnet:
```

Neste arquivo:

- version: '3': Especifica a versão do arquivo Compose.

- services:: Define os serviços que compõem a aplicação.

- web: e redis:: São os nomes dos serviços.

- build: .: Instrui o Compose a construir a imagem do serviço web a partir do Dockerfile no diretório atual.

- ports: - "8000:5000": Mapeia a porta 8000 do host para a porta 5000 do container.

- networks: - webnet: Adiciona o serviço à rede webnet.

- image: "redis:alpine": Instrui o Compose a usar a imagem redis:alpine para o serviço redis.

- networks: webnet:: Define a rede webnet.

Passo 4: Construindo e Executando sua Aplicação com Compose

A partir do diretório do seu projeto, inicie sua aplicação executando 
```
docker compose up.
```

Passo 5: Editando o Arquivo Compose para Adicionar uma Montagem de Volume

Edite o arquivo docker-compose.yml para adicionar uma montagem de volume para o serviço web:

```yaml
version: '3'
services:
  web:
    build: .
    ports:
      - "8000:5000"
    volumes:
      - .:/code
    environment:
      FLASK_DEBUG: "true"
    networks:
      - webnet
  redis:
    image: "redis:alpine"
    networks:
      - webnet

networks:
  webnet:
```


Passo 6: Reconstruindo e Executando a Aplicação com Compose

A partir do diretório do seu projeto, execute docker compose up para construir a aplicação com o arquivo Compose atualizado e executá-la.

Passo 7: Atualizando a Aplicação

Como o código da aplicação agora é montado no container usando um volume, você pode fazer alterações no código e ver as alterações instantaneamente, sem ter que reconstruir a imagem.

Passo 8: Experimentando com Alguns Outros Comandos

Se você quiser executar seus serviços em segundo plano, você pode passar a flag -d (para "modo desanexado") para docker compose up e usar docker compose ps para ver o que está atualmente em execução.

Conclusão

Neste tutorial, você aprendeu como criar uma aplicação web com banco de dados usando Docker e Docker Compose, e como configurar uma rede virtualizada para seus serviços. 
