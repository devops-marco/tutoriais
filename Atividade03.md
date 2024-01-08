## 1. Obtenha a aplicação
Antes de poder executar a aplicação, você precisa obter o código fonte da aplicação em sua máquina. Clone o repositório getting-started usando o seguinte comando:

```bash
Copy code
git clone https://github.com/docker/getting-started.git
```

Dentro do diretório getting-started/app, você deve ver package.json e dois subdiretórios (src e spec).

## 2. Construa a imagem do container da aplicação
Para construir a imagem do container, você precisará usar um Dockerfile. Um Dockerfile é simplesmente um arquivo baseado em texto sem extensão de arquivo que contém um script de instruções. O Docker usa este script para construir uma imagem de container.

No diretório app, no mesmo local que o arquivo package.json, crie um arquivo chamado Dockerfile. Você pode usar os seguintes comandos abaixo para criar um Dockerfile com base em seu sistema operacional.

```bash
cd /path/to/app
touch Dockerfile
```


Adicione o seguinte conteúdo ao Dockerfile:

```Dockerfile
Copy code
# syntax=docker/dockerfile:1

FROM node:18-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
EXPOSE 3000
```


Aqui está uma explicação detalhada dos comandos usados no Dockerfile:
- **syntax=docker/dockerfile:1**: Esta linha define a versão da sintaxe do Dockerfile que estamos usando. É uma boa prática especificar a versão da sintaxe para garantir a compatibilidade.

- **FROM node:18-alpine**: Este comando FROM inicia uma nova etapa de construção e define a imagem base para instruções subsequentes. Neste caso, estamos usando a imagem node:18-alpine, que é uma imagem leve do Node.js baseada no Alpine Linux.

- **WORKDIR /app**: O comando WORKDIR define o diretório de trabalho para qualquer instrução RUN, CMD, ENTRYPOINT, COPY e ADD que se segue no Dockerfile. Neste caso, estamos definindo /app como nosso diretório de trabalho.

- **COPY . .**: O comando COPY copia novos arquivos ou diretórios do <src> e adiciona-os ao sistema de arquivos do container no caminho <dest>. Neste caso, estamos copiando tudo do diretório atual (indicado pelo primeiro .) para o diretório de trabalho no container (indicado pelo segundo .).

- **RUN yarn install --production**: O comando RUN executa qualquer comando em uma nova camada em cima da imagem atual e faz commit da imagem resultante. A imagem resultante será usada para o próximo passo no Dockerfile. Neste caso, estamos usando yarn install --production para instalar as dependências do nosso aplicativo.

- **CMD ["node", "src/index.js"]**: O comando CMD fornece padrões para um container em execução. Esses padrões podem incluir um executável, ou eles podem omitir o executável, caso em que você deve especificar um ENTRYPOINT de comando. Neste caso, estamos definindo o comando padrão para iniciar nosso aplicativo como node src/index.js.

- **EXPOSE 3000**: O comando EXPOSE informa ao Docker que o container escuta nas portas de rede especificadas no tempo de execução. Neste caso, estamos expondo a porta 3000.


## 3. Construa a imagem do container
Construa a imagem do container usando os seguintes comandos:

```bash
Copy code
cd /path/to/app
docker build -t getting-started .
```
O comando docker build usa o Dockerfile para construir uma nova imagem de container. A flag -t marca sua imagem. Pense nisso simplesmente como um nome legível por humanos para a imagem final. Como você nomeou a imagem getting-started, você pode se referir a essa imagem quando executar um container.

## 4. Inicie um container da aplicação
Agora que você tem uma imagem, você pode executar a aplicação em um container. Para fazer isso, você usará o comando docker run.

```bash
Copy code
docker run -dp 127.0.0.1:3000:3000 getting-started
```

A flag -d (abreviação de --detach) executa o container em segundo plano. A flag -p (abreviação de --publish) cria um mapeamento de porta entre o host e o container. O comando mostrado aqui publica a porta 3000 do container para 127.0.0.1:3000 (localhost:3000) no host.

Depois de alguns segundos, abra seu navegador da web para http://localhost:3000. Você deve ver sua aplicação.
