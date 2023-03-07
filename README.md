## Microserviços Controle financeiro
- Desenvolvimento de um Saas multitenancy de um sistema de controle financeiro
- Cada cliente terá seu subdominio e poderá fazer o controle de suas finanças
- Cada cliente será capaz de gerar relatórios a partir de um filtro de data
- Teremos um dasboard para acompanhar as métricas e transações
- usando tudo com docker

## Desafio 1
Serviço de identidade e autentticação que seja capaz de identificar qual empresa (tenant)
cada usuário pertence e que possa realizar o processo de autenticação.

## Solução 1
Usar o Keycloack, Uma plataforma Open Source para gerenciamento de acessos e identidade que 
atualmente é mantida pela RedHat.

## Desafio 2
Pelo fato de todo processo de autenticação estar centralizado no Keycloak, precisamos evitar
que cada requisição no backend, ele precise consultar o keycloack para validar o JWT informado.

## Solução 2
Usamos o formato de chaves públicas e privadas emitidas pelo Keycloak. O nosso backend terá uma 
chave pública que será capaz de validar o JWT enviado pelo frontend, não haverá necessidade do backend
se conectar com o keycload a cada requisição.

## Desafio 3
O processo de emissão de relatório acontecerá de forma assíncrona através de um microserviço específico
para isso. Como garantir resiliência entre a solitação do relatório, bem como a confirmação de um relatório
foi gerado ?

## Solução 3
Usamos para esse processamento de forma assíoncrona e para isso utilizaremos o poderoso Apache Kafka

## Desafio 4
O Microserviço de geração de relatórios terá um espelhamento das transações realizadas em banco de dados
Elasticsearch. Como garantir a sincronização entre as duas bases ?

## Solução 4
Usamos o Kafka Connect para fazer a ingestão dos dados de forma automatizada no ElasticSearch.

## Desafio 5
Precisamos extrair métricas gerenciais do sistema como um todo incluindo a geração de gráficos e dashboards.

## Solução 5
Usamos o Kibana para gerar de forma simples e intuitiva todas as informações necessárias através de 
gráficos e dashboards.

!.[Dinamica do sistema].(https://cdn.discordapp.com/attachments/1008571086411145308/1082730875789258783/dinamica.png)

## Ordem recomendada de execução
* Apache Kafka
* Keycloak
* Back-end Nest.js
* Front-end Next.js

# Imersão Fullcycle 4
Essa imersão foi realizada com o time fullcycle: https://imersao.fullcycle.com.br/