# Tutorial VS Code, Node e Express

- # Atividade - Tutorial de VS Code, Node.js, Express, GitHub e GitHub Actions

  - ## Parte 1: VS Code com Node.js e Express

    1. **Instalação do Node.js**: Para rodar uma aplicação Node.js, você precisará instalar o Node.js em sua máquina. Você pode verificar se o Node.js está instalado corretamente em seu computador abrindo um novo terminal e digitando `node --version`. Você deverá ver a versão atual do Node.js instalada.
    2. **Criando uma aplicação Node.js 'Hello World'**: Crie uma pasta vazia chamada 'hello', navegue até ela e abra o VS Code:

    ```
    mkdir hello
    cd hello
    code .
    ```

    1. **Criando um arquivo JavaScript**: No VS Code, pressione o botão 'New File' e nomeie o arquivo como 'app.js'. Crie uma variável de string simples em 'app.js' e envie o conteúdo da string para o console:

    ```
    var msg = 'Hello World';
    console.log(msg);
    ```

    1. **Executando a aplicação**: Para executar 'app.js' com Node.js, digite `node app.js` em um terminal. Você deverá ver 'Hello World' exibido no terminal.
    2. **Criando uma aplicação Express**: Express é um framework muito popular para construir e executar aplicações Node.js. Você pode criar uma nova aplicação Express usando a ferramenta Express Generator. Instale o Express Generator executando `npm install -g express-generator` em um terminal. Em seguida, crie uma nova aplicação Express chamada 'myExpressApp' executando `express myExpressApp --view pug`. Isso criará uma nova pasta chamada 'myExpressApp' com o conteúdo da sua aplicação.
    3. **Instalando as dependências da aplicação**: Para instalar todas as dependências da aplicação, vá para a nova pasta e execute `npm install`. Para testar se a aplicação está funcionando, execute `npm start` em um terminal na pasta da aplicação Express. O servidor web Node.js será iniciado e você poderá navegar até 'http\://localhost:3000' para ver a aplicação em execução.

    ##
  - # Tutorial de VS Code, Node.js, Express e GitHub

    ## Parte 1: VS Code com Node.js e Express

    Siga as etapas descritas anteriormente para criar e testar sua aplicação Node.js e Express no VS Code.

    ## Parte 2: Git e GitHub

    1. **Inicializando um Repositório Git**

       No VS Code, abra o terminal integrado (View -> Terminal).

       Navegue até a pasta do seu projeto (se ainda não estiver lá) usando o comando `cd`.

       Inicialize um novo repositório Git com o comando:

       ```
       git init
       ```
    2. **Adicionando Arquivos ao Repositório Git**

       Adicione todos os arquivos do seu projeto ao novo repositório Git com o comando:

       ```
       git add .
       ```
    3. **Commitando as Alterações**

       Faça um commit das alterações com o comando:

       ```
       git commit -m "Initial commit"
       ```
    4. **Conectando com o GitHub**

       Crie um novo repositório no GitHub. Não inicialize o repositório com um README, .gitignore ou License. Isso será adicionado do seu projeto existente.

       No terminal do VS Code, adicione o URL do repositório GitHub como o "origin" remoto:

       ```
       git remote add origin your-github-repo-url
       ```

       Substitua "your-github-repo-url" pelo URL do seu repositório GitHub.
    5. **Pushing para o GitHub**

       Faça um push do seu commit para o repositório GitHub com o comando:

       ```
       git push -u origin master
       ```

    Agora, seu código deve estar disponível no GitHub. Seus colegas de equipe podem clonar o repositório, fazer alterações e fazer push de suas próprias alterações, e você pode fazer pull dessas alterações de volta para o seu repositório local.
  - # Tutorial de GitHub Actions

    ## Parte 1: Configurando um Fluxo de Trabalho

    1. **Criar um arquivo de fluxo de trabalho**

       No seu repositório, crie um diretório chamado `.github/workflows/`. Dentro deste diretório, você pode criar um arquivo YAML para o seu fluxo de trabalho. Por exemplo, você pode criar um arquivo chamado `main.yml`.
    2. **Definir o fluxo de trabalho**

       Dentro do arquivo YAML, você pode definir o seu fluxo de trabalho. Aqui está um exemplo de um fluxo de trabalho básico que é acionado a cada push para o repositório:

       ```
       name: CI

       on: [push]

       jobs:
         build:
           runs-on: ubuntu-latest

           steps:
           - uses: actions/checkout@v3

           - name: Use Node.js
             uses: actions/setup-node@v1
             with:
               node-version: '18.x'

           - name: Install Dependencies
             run: npm install

           - name: Run Tests
             run: npm test

           - name: Build
             run: npm run build
       ```

       Este fluxo de trabalho realiza as seguintes ações:
       - Faz checkout do código do repositório.
       - Configura o Node.js.
       - Instala as dependências do projeto (assumindo que você tem um arquivo `package.json`).
       - Executa os testes do projeto (assumindo que você tem um script de teste definido no seu `package.json`).
       - Constrói o projeto (assumindo que você tem um script de build definido no seu `package.json`).
    3. **Commitar e Pushar o arquivo de fluxo de trabalho**

       Faça commit do arquivo de fluxo de trabalho e faça push para o seu repositório. O GitHub Actions começará a executar o fluxo de trabalho a cada push para o repositório.

    ## Parte 2: Disparando Manualmente um Fluxo de Trabalho

    Para disparar manualmente um fluxo de trabalho, você pode usar o evento `workflow_dispatch` no seu arquivo de fluxo de trabalho. Aqui está um exemplo:

    ```
    name: CI

    on: 
      workflow_dispatch:
      push:

    jobs:
      build:
        runs-on: ubuntu-latest

        steps:
        - uses: actions/checkout@v3

        - name: Use Node.js
          uses: actions/setup-node@v1
          with:
            node-version: '18.x'

        - name: Install Dependencies
          run: npm install

        - name: Run Tests
          run: npm test

        - name: Build
          run: npm run build
    ```

    Neste exemplo, adicionamos `workflow_dispatch:` sob o `on:`. Isso permite que o fluxo de trabalho seja disparado manualmente a partir da interface do GitHub.

    Para disparar o fluxo de trabalho manualmente, vá para a guia "Actions" no seu repositório GitHub, selecione o fluxo de trabalho que você deseja disparar, e clique no botão "Run workflow".

    ## Parte 3: Examinando os Resultados do Fluxo de Trabalho

    Você pode verificar os resultados do seu fluxo de trabalho indo para a guia "Actions" no seu repositório GitHub. Aqui, você pode ver uma lista de todas as execuções do fluxo de trabalho.

    Para ver os detalhes de uma execução do fluxo de trabalho:
    1. Clique no nome da execução do fluxo de trabalho na lista. Isso abrirá uma página de resumo da execução do fluxo de trabalho.
    2. Na página de resumo, você pode ver o progresso da execução do fluxo de trabalho e o resultado de cada trabalho no fluxo de trabalho.
    3. Para ver os detalhes de um trabalho, clique no nome do trabalho na barra lateral esquerda ou no gráfico de visualização. Isso abrirá uma página com os detalhes do trabalho, incluindo cada passo do trabalho e o resultado de cada passo.
    4. Para ver os resultados de uma etapa, clique no nome da etapa. Isso abrirá uma janela com os detalhes da etapa, incluindo o log de saída da etapa.

