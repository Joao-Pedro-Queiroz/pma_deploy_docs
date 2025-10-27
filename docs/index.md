# Documentação do Deploy dos Microserviços

## Equipe de desenvolvedores

- João Pedro Queiroz Viana
- Pedro Ricardo Fardin

## Documentação detalhada dos Microserviços, Jenkins, Kubernets e Bottlenecks

[Documentação dos Microserviços](https://joao-pedro-queiroz.github.io/pma_apis_docs/)

## Estrutura atual dos microserviços

``` mermaid
flowchart LR
    subgraph api [Subnet API]
        direction TB
        gateway --> account
        gateway --> auth:::red
        gateway --> order
        gateway --> product
        auth --> account
        order --> product
        order --- product        %% linha adicional que sugere proximidade
        account --> db[(PostgreSQL)]
        product --> db
        order --> db
        product --> re[(Redis Cache)]
        re --> |HIT| product
        re --> |MISS| db
        db --> re
    end
    internet --> |request| gateway:::orange

    classDef orange fill:#FCBE3E
    classDef red fill:#f8d7da,stroke:#c43a3a
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