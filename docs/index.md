# Documentação do Deploy dos Microserviços

## Equipe de desenvolvedores

- João Pedro Queiroz Viana
- Pedro Ricardo Fardin

## Documentação detalhada dos Microserviços, Jenkins, Kubernets e Bottlenecks

[Documentação dos Microserviços](https://joao-pedro-queiroz.github.io/pma_apis_docs/)

## Estrutura atual dos microserviços

``` mermaid
flowchart LR
  %% camadas
  subgraph public["Cliente / Internet"]
    direction TB
    Internet[Internet]
  end

  subgraph edge["Borda / API Gateway"]
    direction TB
    Gateway[Gateway]
  end

  subgraph backend["Serviços (Subnet API)"]
    direction TB

    subgraph services["Services"]
      direction LR
      Auth[auth\n(authentication)]
      Account[account\n(profile/orders)]
      Order[order\n(orders)]
      Product[product\n(catalog)]
    end

    subgraph storage["Armazenamento"]
      direction LR
      Redis[(Redis Cache)]
      Postgres[(PostgreSQL)]
    end
  end

  %% fluxos principais
  Internet -->|HTTP request| Gateway
  Gateway -->|authn| Auth
  Gateway --> Account
  Gateway --> Order
  Gateway --> Product

  %% interações entre serviços
  Auth -->|tokens / introspect| Account
  Account -->|create/read/update| Postgres
  Order -->|create/read| Postgres
  Product -->|read| Redis
  Redis -->|HIT| Product
  Redis -->|MISS → fallback| Postgres
  Postgres -->|write / cache update| Redis

  %% estilos simples
  classDef gw fill:#FCBE3E,stroke:#333,stroke-width:1px
  classDef svcBox fill:#E8F0FF,stroke:#4b6cb7
  classDef authBox fill:#FFEDEE,stroke:#c43a3a
  classDef cyl fill:#FFF7E6,stroke:#b07b00

  class Gateway gw
  class Product,Account,Order svcBox
  class Auth authBox
  class Redis,Postgres cyl
```

## Repositórios

Principal: 
[https://github.com/Joao-Pedro-Queiroz/pma.25.2](https://github.com/Joao-Pedro-Queiroz/pma.25.2)

| Microservice | Interface | Implementation |
|-|-|-|
| Account | [account](https://github.com/Joao-Pedro-Queiroz/account) | [account-service](https://github.com/Joao-Pedro-Queiroz/account-service) |
| Auth | [auth](https://github.com/Joao-Pedro-Queiroz/auth) | [auth-service](https://github.com/Joao-Pedro-Queiroz/auth-service) |
| Gateway |  | [gateway-service](https://github.com/Joao-Pedro-Queiroz/gateway-service) |
| Product | [product](https://github.com/Joao-Pedro-Queiroz/product) | [product-service](https://github.com/Joao-Pedro-Queiroz/product-service) |
| Order | [order](https://github.com/Joao-Pedro-Queiroz/order) | [order-service](https://github.com/Joao-Pedro-Queiroz/order-service) |