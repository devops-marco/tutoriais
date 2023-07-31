Abaixo vou te fornecer cinco arquivos YAML distintos. Você deve seguir as referências de pesquisa e explicar em detalhes a sintaxe do que cada arquivo faz.

## Exercício 1: Fluxo de trabalho para implantar arquivo Node

  1. **Arquivo YAML**

  ```yaml
  name: CI para Node.js

  on:
    push:
      branches: [ master ]
    pull_request:
      branches: [ master ]

  jobs:
    construir:

      runs-on: ubuntu-latest

      strategy:
        matrix:
          node-version: [14.x]

      steps:
      - uses: actions/checkout@v2
      - name: Usar Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v2
        with:
          node-version: ${{ matrix.node-version }}
      - run: npm ci
      - run: npm run build --if-present
      - run: npm test
  ```

  1. **Pesquisa**

  Pesquise o que cada parte deste arquivo YAML faz. Use a documentação oficial do GitHub Actions (https://docs.github.com/pt/actions) como referência.

  ## Exercício 2: Fluxo de trabalho para implantar no Heroku

  1. **Arquivo YAML**

  ```yaml
  name: Implantar no Heroku

  on:
    push:
      branches:
        - master

  jobs:
    implantar:
      runs-on: ubuntu-latest

      steps:
      - uses: actions/checkout@v2

      - name: Implantar no Heroku
        uses: akhileshns/heroku-deploy@v3.12.12
        with:
          heroku_api_key: ${{secrets.HEROKU_API_KEY}}
          heroku_app_name: "nome-do-seu-app"
          heroku_email: "seu-email@example.com"
  ```

  1. **Pesquisa**

  Pesquise o que cada parte deste arquivo YAML faz. Use a documentação oficial do GitHub Actions (https://docs.github.com/pt/actions) e a documentação do Heroku Deploy Action (https://github.com/AkhileshNS/heroku-deploy) como referência.

  ## Exercício 3: Fluxo de trabalho para implantar no Azure

  1. **Arquivo YAML**

  ```yaml
  name: Implantar no Azure

  on:
    push:
      branches:
        - master

  jobs:
    construir-e-implantar:
      runs-on: ubuntu-latest

      steps:
      - uses: actions/checkout@v2

      - name: Login via módulo Az
        run: |
          az login --service-principal -u ${{ secrets.AZURE_SERVICE_APP_ID }} -p ${{ secrets.AZURE_SERVICE_PASSWORD }} --tenant ${{ secrets.AZURE_SERVICE_TENANT_ID }}

      - name: Implantar no Azure
        run: |
          az webapp up --name <nome-do-app> --location <localização> --sku <sku>
  ```

  1. **Pesquisa**

  Pesquise o que cada parte deste arquivo YAML faz. Use a documentação oficial do GitHub Actions (https://docs.github.com/pt/actions) e a documentação do Azure CLI (https://docs.microsoft.com/pt-br/cli/azure/) como referência.

  ## Exercício 4: Fluxo de trabalho para implantar no AWS

  1. **Arquivo YAML**

  ```yaml
  name: Implantar no AWS

  on:
    push:
      branches:
        - master

  jobs:
    implantar:
      runs-on: ubuntu-latest

      steps:
      - name: Fazer checkout do código
        uses: actions/checkout@v2

      - name: Configurar credenciais da AWS
        uses: aws-actions/configure-aws-credentials@v1
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-west-2

      - name: Implantar no AWS
        run: |
          aws s3 sync . s3://meu-bucket
  ```

  1. **Pesquisa**

  Pesquise o que cada parte deste arquivo YAML faz. Use a documentação oficial do GitHub Actions (https://docs.github.com/pt/actions) e a documentação da AWS CLI (https://aws.amazon.com/pt/cli/) como referência.

  ## Exercício 5: Fluxo de trabalho de Integração Contínua (CI) para Python

  1. **Arquivo YAML**

  ```yaml
  name: Aplicação Python

  on: [push]

  jobs:
    construir:

      runs-on: ubuntu-latest

      steps:
      - uses: actions/checkout@v2
      - name: Configurar Python 3.8
        uses: actions/setup-python@v2
        with:
          python-version: 3.8
      - name: Instalar dependências
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt
      - name: Testar com pytest
        run: |
          pytest
  ```

  1. **Pesquisa**

  Pesquise o que cada parte deste arquivo YAML faz. Use a documentação oficial do GitHub Actions (https://docs.github.com/pt/actions) como referência.
- ## Gabaritos

  1. **Exercício 1: Fluxo de trabalho de Integração Contínua (CI) para Node.js**

     Este fluxo de trabalho é acionado a cada push ou pull request para a branch master. Ele define um trabalho chamado "construir" que é executado em um ambiente Ubuntu. O trabalho usa a versão 14.x do Node.js, instala as dependências do projeto com `npm ci`, executa o script de build (se presente) com `npm run build --if-present`, e executa os testes com `npm test`.
  2. **Exercício 2: Fluxo de trabalho para implantar no Heroku**

     Este fluxo de trabalho é acionado a cada push para a branch master. Ele define um trabalho chamado "implantar" que é executado em um ambiente Ubuntu. O trabalho faz checkout do código do repositório e, em seguida, usa a ação Heroku Deploy para implantar o aplicativo no Heroku. A ação Heroku Deploy usa a chave da API do Heroku, o nome do aplicativo e o e-mail que são fornecidos como variáveis de ambiente.
  3. **Exercício 3: Fluxo de trabalho para implantar no Azure**

     Este fluxo de trabalho é acionado a cada push para a branch master. Ele define um trabalho chamado "construir-e-implantar" que é executado em um ambiente Ubuntu. O trabalho faz checkout do código do repositório, faz login no Azure usando o módulo Az e, em seguida, usa o comando `az webapp up` para implantar o aplicativo no Azure.
  4. **Exercício 4: Fluxo de trabalho para implantar no AWS**

     Este fluxo de trabalho é acionado a cada push para a branch master. Ele define um trabalho chamado "implantar" que é executado em um ambiente Ubuntu. O trabalho faz checkout do código do repositório, configura as credenciais da AWS e, em seguida, usa o comando `aws s3 sync` para sincronizar o código do repositório com um bucket do S3.
  5. **Exercício 5: Fluxo de trabalho de Integração Contínua (CI) para Python**

     Este fluxo de trabalho é acionado a cada push para o repositório. Ele define um trabalho chamado "construir" que é executado em um ambiente Ubuntu. O trabalho faz checkout do código do repositório, configura o Python 3.8, instala as dependências do projeto listadas no arquivo `requirements.txt` e, em seguida, executa os testes usando pytest.
