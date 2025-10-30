# Projeto - AWS + EKS

## Configuração AWS CLI

Baixar o AWS CLI e utilizar o aws configure com as chaves de acesso.

[AWS CLI - Instalação](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

## Criação do Cluster na AWS

Criação do Cluster EKS:
![Cluster Funcionando](../img/cluster_running.png)

Ao final, teremos um cluster que, por padrão, tera duas instancias de subnets publicas e privadas, onde no meio delas existe um load balancer para controlar o tráfego de rede, enquanto as aplicações ficam na subnet privada. Deste modo, temos um sistema seguro onde o ususario comum é incapaz de ter acesso à nossa rede após o load balancer:  
![Arquitetura do Load Balancer](../img/architecture.png)

Basta então sincronizarmos com nosso aws-cli usando `aws eks update-kubeconfig --name eks-store` e poderemos acessar nosso cluster remotamente.  

## Teste de Carga

