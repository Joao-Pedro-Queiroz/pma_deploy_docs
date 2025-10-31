# Projeto - AWS + EKS

## Configuração AWS CLI

Baixar o AWS CLI e utilizar o aws configure com as chaves de acesso.

[AWS CLI - Instalação](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

## Criação do Cluster na AWS

Criação do Cluster EKS:
![Cluster Funcionando](../img/cluster_running.png)

Ao final, teremos um cluster que, por padrão, tera duas instancias de subnets publicas e privadas, onde no meio delas existe um load balancer para controlar o tráfego de rede, enquanto as aplicações ficam na subnet privada. Deste modo, temos um sistema seguro onde o ususario comum é incapaz de ter acesso à nossa rede após o load balancer:  
![Arquitetura do Load Balancer](../img/architecture.png)

Basta então sincronizarmos com o AWS CLI usando `aws eks update-kubeconfig --name eks-store` e poderemos acessar nosso cluster remotamente.  

## Teste de Carga

<video width="640" height="360" controls>
  <source src="../video/teste_carga.mp4" type="video/mp4">
  Seu navegador não suporta o elemento de vídeo.
</video>

## CI/CD

O Jenkins é responsável pela integração contínua (CI) e a entrega contínua (CD) do projeto.

[Documentação Jenkins](https://joao-pedro-queiroz.github.io/pma_apis_docs/jenkins/main/)

## 💰 Custos

A partir do painel **Billing and Cost Management** da AWS, é possível acompanhar detalhadamente os custos do ambiente em execução no EKS, incluindo EC2, balanceadores de carga e demais serviços associados.

---

### 🔹 Visão Geral dos Custos

A imagem abaixo mostra o **resumo dos custos mensais** até o momento, incluindo o custo acumulado no mês atual e a previsão total para o mês:

![Resumo de Custos](../img/cost_summary.png)

- **Month-to-date cost:** US$ 51.90  
- **Total forecasted cost:** US$ 57.37  
- **Último mês:** Sem custos registrados, indicando início recente de uso dos recursos.

---

### 🔹 Distribuição por Serviço

O gráfico abaixo mostra o **breakdown de custos** por serviço da AWS:

![Distribuição de Custos por Serviço](../img/cost_breakdown.png)

Principais serviços com custo associado:
- **Amazon Elastic Container Service for Kubernetes (EKS)** — custos do cluster e seus nós de controle.  
- **Amazon Elastic Compute Cloud (EC2)** — instâncias utilizadas pelos *worker nodes*.  
- **Amazon Elastic Load Balancing (ALB)** — balanceador de carga público responsável pelo tráfego externo.  
- **Impostos e outros serviços menores.**

---

### 🔹 Recomendações de Otimização

A AWS fornece recomendações automáticas de otimização de custo, como mostrado no painel:

- 💡 **Criar um monitor de anomalias de custo (Anomaly Monitor):** identifica aumentos inesperados no gasto.  
- 💡 **Habilitar o Cost Optimization Hub:** permite gerar relatórios de economia.  
- 💡 **Adicionar contatos de cobrança alternativos:** melhora a visibilidade e controle financeiro.

Essas ações ajudam a manter os custos previsíveis e evitar gastos indevidos.

---

### 🔹 Análise Detalhada

Para análises mais completas, é possível acessar o [**AWS Cost Explorer**](https://console.aws.amazon.com/cost-reports/home) e filtrar custos por:
- Serviço (EKS, EC2, etc.)  
- Região  
- Tag de projeto  
- Período mensal ou diário

---

📊 *Essas informações ajudam a manter o controle financeiro da infraestrutura em nuvem, permitindo identificar rapidamente aumentos de custo e otimizar os recursos utilizados no cluster EKS.*

## PaaS

