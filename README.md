# curso-quarkus-devtalk

## Cronograma do curso

### Módulo 1

1. O que é o Quarkus, e qual problema ele veio resolver?
2. Configuração do ambiente - Instalando o IntelliJ
3. Configuração do ambiente - Instalando o Java através do IntelliJ
5. Criando uma aplicação Quarkus (Usando code.quarkus.io)
6. Criando uma aplicação Quarkus (Usando o Quarkus CLI)
7. Criando uma aplicação Quarkus usando Maven
8. Explorando um projeto Quarkus
9. Onde está o método main?
10. Executando nossa aplicação Quarkus com o Quarkus CLI e Maven
11. Subindo nossa aplicação para o Github
12. Configurando o CI para a aplicação no Github

### Módulo 2

1. Entendendo o que vamos criar (Um sistema para call for papers) e apresentando a arquitetura do sistema com o C4 Model (Diagrama de Contexto e de Contêineres)
2. Criando a entidade `Event`
3. Criando os testes de unidade para a classe `Event`
4. Criando nosso primeiro endpoint REST com JAX-RS para cadastro de `Events` em memória
    1. Versionamento de APIs
    2. Conheça sobre o padrão DTO
    3. Adicionando a extensão `quarkus-rest-jackson` para o Quarkus saber lidar com a serialização/deserialização de JSON
    4. Adicionando a extensão `quarkus-smallrye-openapi` para a documentação da nossa API e para consumirmos de forma amigável os nossos recursos REST em tempo de desenvolvimento
5. Instalando o driver JDBC e o Hibernate em nossa aplicação
6. Persistindo um `Event` no banco de dados com `EntitityManager`
7. Realizando testes de integração POST `/v1/events`
8. Atualizando nossa aplicação para utilizar o Panache ORM
9. Implementando a paginação de `Events` com Panache ORM 
10. Implementando a  busca por ID de `Events` com Panache ORM
11. Implementando a deleção de um `Event` com Panache ORM
12. Implementando a edição de um `Event` com Panache ORM

### Módulo 3 

1. Validando dados de entrada com Bean Validation (`@NotNull`, `@Size`, etc.)
2. Melhorando os erros da nossa API para os nossos clientes
    1. Utilizando [`ExceptionMapper`](https://pt.quarkus.io/guides/rest#exception-mapping)
    2. Utilizando [Problem Details](https://datatracker.ietf.org/doc/html/rfc7807) para melhorar e padronizar nossas respostas de erro
3. Revisitando os princípios REST e o modelo de maturidade de Richardson aplicados ao nosso domínio de Call4Papers
4. Organizando nossa aplicação em camadas com CDI
    1. Injeção de dependência, escopos (`@ApplicationScoped`, `@RequestScoped`) e qualifiers
    2. Separando Resource, Service e Repository
5. Protegendo nossos endpoints: autenticação em memória com Quarkus Security
6. Protegendo nossos endpoints: autenticação com usuários armazenados em banco de dados
7. Implementando autorização com RBAC e JSR-250 (`@RolesAllowed`, `@PermitAll`, `@DenyAll`)

### Módulo 4

1. Por que quebrar nosso sistema em microsserviços? Revisitando a arquitetura C4 apresentada no início do curso e o domínio do Call4Papers (`proposal`, `email` e `event`)
2. Reestruturando o projeto em um monorepo multi-módulo Maven: criando os módulos `proposal-service`, `email-service` e `event-service`
3. Configurando um banco de dados dedicado (Database per Service) para cada microsserviço com Docker Compose
4. Modelando as entidades `Event` e `Local` no `event-service` com Panache
5. Modelando a entidade `Slot` e o seu relacionamento com `Event` e `Local`
6. Criando os endpoints REST para o `ORGANIZADOR` cadastrar um `Event` e o seu `Local`
7. Criando o endpoint REST para o `ORGANIZADOR` cadastrar os `Slots` de um `Event`
8. Comunicação síncrona entre microsserviços: comparando REST Clients (Java HttpClient, RestEasy Classic e Quarkus REST)
9. Consumindo o `proposal-service` a partir do `event-service` com o MicroProfile Rest Client
10. Explorando o MicroProfile Config e Health Checks
11. Explorando o MicroProfile Fault Tolerance
12. Compilando nossos microsserviços como imagem nativa com o GraalVM

### Módulo 5

1. Entendendo transações e o modelo ACID
2. Criando o endpoint de avaliação de propostas no `event-service` (aprovar ou rejeitar)
3. Implementando a busca pelo próximo `Slot` compatível e disponível para a proposta aprovada
4. Alocando automaticamente o `Slot` na aprovação, dentro da mesma transação, com `@Transactional`
5. Tratando o caso de não haver `Slot` disponível (rollback e status "aprovada aguardando slot")
6. Propagação de transações: entendendo `REQUIRED`, `REQUIRES_NEW` e `NESTED`
7. Criando um filtro para logar as requisições entre os microsserviços
8. Criando um interceptador para uma regra de rate limit no `proposal-service`

### Módulo 6

1. Entendendo tokens JWT: estrutura, claims e assinatura
2. Gerando e validando tokens JWT no `event-service`
3. Introduzindo SSO, OpenID Connect e OAuth2
4. Subindo o Keycloak com Docker Compose
5. Configurando o Realm e os papéis `SPEAKER`, `REVISOR` e `ORGANIZADOR` no Keycloak
6. Protegendo o `proposal-service` como Resource Server com `quarkus-oidc`
7. Protegendo o `email-service` e o `event-service` como Resource Servers com `quarkus-oidc`
8. Restringindo o cadastro de `Event`, `Local` e `Slot` apenas ao papel `ORGANIZADOR`
9. Liberando a avaliação de propostas para os papéis `REVISOR` e `ORGANIZADOR`

### Módulo 7

1. Otimizando consultas com cache usando Redis no `proposal-service`
2. Configurando o cliente Redis com a extensão `quarkus-redis-client`
3. Entendendo o MicroProfile Reactive Messaging: canais, `@Incoming`/`@Outgoing` e o conceito de conectores
4. Configurando o conector Kafka (`smallrye-kafka`) com a extensão `quarkus-messaging-kafka`
5. Publicando eventos de mudança de status de proposta em um tópico Kafka
6. Consumindo eventos do Kafka no `email-service` para notificar o `SPEAKER`
7. Consumindo eventos do Kafka no `event-service` para sincronizar as propostas submetidas
8. Conhecendo o RabbitMQ: filas, exchanges e bindings (laboratório isolado, comparando mensageria tradicional com streaming de eventos)

### Módulo 8

1. Orquestrando todo o sistema Call4Papers com Docker Compose (Postgres x3, Kafka, Redis, Keycloak)
2. Cadastrando um `Event`, um `Local` e seus `Slots` como `ORGANIZADOR`
3. Submetendo uma proposta como `SPEAKER`
4. Aprovando a proposta como `REVISOR` e acompanhando a alocação automática do `Slot`
5. Conferindo a notificação por e-mail recebida pelo `SPEAKER`
6. Revisão geral do curso e próximos passos

### Módulo 9

1. Por que usar Flyway em vez do `hibernate.hbm2ddl.auto` em produção?
2. Adicionando a extensão `quarkus-flyway` e criando a primeira migration (`V1__create_table.sql`)
3. Versionando as migrations do `proposal-service`, `event-service` e `email-service`
4. Rodando as migrations automaticamente na inicialização de cada microsserviço

### Módulo 10

1. Configurando profiles para produção (`%prod`) e variáveis de ambiente
2. Gerenciando segredos (senhas de banco, client secrets do Keycloak) fora do código-fonte
3. Preparando health checks, métricas e logs estruturados para produção
4. Empacotando nossos microsserviços como imagem de contêiner com a extensão `quarkus-container-image-jib`
5. Rodando as migrations do Flyway como parte do processo de build e deploy da imagem de contêiner
6. Criando uma conta gratuita no Red Hat OpenShift (Developer Sandbox)
7. Fazendo o deploy do `proposal-service` no OpenShift com a extensão `quarkus-openshift`
8. Fazendo o deploy do `event-service` e do `email-service` no OpenShift
9. Testando o fluxo completo do Call4Papers rodando em produção