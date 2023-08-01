# Introdução à Engenharia do Caos

A Engenharia do Caos é uma disciplina de engenharia que se concentra em melhorar a resiliência e a confiabilidade dos sistemas através da introdução proativa de falhas. A ideia é que, ao introduzir falhas de maneira controlada em um sistema, podemos descobrir e corrigir problemas antes que eles ocorram em um ambiente de produção, onde podem ter consequências muito mais graves.

## Introdução ao Gremlin

Gremlin é uma plataforma líder em Engenharia do Caos como serviço. Ele fornece uma maneira simples, segura e segura de realizar experimentos de Engenharia do Caos em uma variedade de sistemas, incluindo servidores físicos, máquinas virtuais, contêineres e orquestradores de contêineres.

O Gremlin fornece uma variedade de ataques que podem ser usados para introduzir diferentes tipos de falhas, incluindo atrasos de rede, falhas de CPU, falhas de disco e muito mais. Ele também fornece uma interface de usuário intuitiva e uma API poderosa, tornando-o fácil de usar para engenheiros de todos os níveis de experiência.

## Tipos de Ataques com Gremlin

O Gremlin fornece três categorias de experimentos:

- Experimentos de Recursos: Testam contra mudanças súbitas no consumo de recursos computacionais.
- Experimentos de Rede: Testam contra condições de rede não confiáveis.
- Experimentos de Estado: Testam contra mudanças inesperadas em seu ambiente, como quedas de energia, falhas de nós, deriva de relógio ou falhas de aplicativos.

Cada experimento testa sua resiliência de uma maneira diferente. Os experimentos de recursos são um ótimo ponto de partida - simples de executar e entender. Eles revelam como seu serviço se degrada quando é privado de CPU, memória, IO ou espaço em disco.

## Ataque a um servidor Nginx com Gremlin

Aqui está um exemplo de como você pode usar o Gremlin para realizar um ataque de Engenharia do Caos em um servidor Nginx rodando em um contêiner Docker:

Instale o Docker e o Gremlin: Primeiro, você precisará instalar o Docker e o Gremlin em sua máquina local. Você pode baixar o 
Docker a partir do site oficial do Docker e o Gremlin a partir do site oficial do Gremlin.

Inicie um contêiner Docker Nginx: Execute o seguinte comando para iniciar um contêiner Docker rodando o servidor Nginx:

```sh
docker run -d --name my-nginx -p 8080:80 nginx
```
Este comando inicia um contêiner chamado my-nginx rodando o servidor Nginx e mapeia a porta 8080 da sua máquina local para a porta 80 do contêiner.

Execute um ataque Gremlin: Agora você pode executar um ataque Gremlin no contêiner my-nginx. 

Por exemplo, você pode introduzir uma latência nas chamadas durante 10 segundos em todas as chamadas de rede feitas a partir do contêiner my-nginx com o seguinte comando:

```sh
docker exec -it my-gremlin gremlin attack delay --length 10 --target container my-nginx
```


Este comando introduz um atraso durante 10 segundos em todas as chamadas de rede feitas a partir do contêiner my-nginx.
Verifique o resultado do ataque: Você pode verificar o resultado do ataque Gremlin verificando os logs do contêiner my-gremlin:

```sh
docker logs my-gremlin
```

Você deve ver uma mensagem indicando que o ataque Gremlin foi executado com sucesso.
Observe o comportamento antes e depois do ataque: 

Antes do ataque, você deve ser capaz de acessar o servidor Nginx em http://localhost:8080 sem atrasos. Durante o ataque, você deve notar um atraso de 10 segundos ao tentar acessar o servidor. 

Depois que o ataque terminar, o acesso ao servidor deve voltar ao normal.

Este é apenas um exemplo básico de como você pode usar o Gremlin para realizar um ataque de Engenharia do Caos em um servidor Nginx rodando em um contêiner Docker. 

A complexidade dos ataques do Gremlin pode variar dependendo de suas necessidades. Para mais detalhes, consulte a documentação oficial do Gremlin.
