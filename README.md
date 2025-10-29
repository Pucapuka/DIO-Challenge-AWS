# DIO-Challenge-AWS
Desafio de Projeto AWS do BootCamp DIO TQI Modernização com GenAI

# Arquitetura AWS para Microsserviços

## Visão Geral

Esta documentação descreve uma arquitetura de referência para aplicações baseadas em microsserviços na AWS, projetada para oferecer escalabilidade, resiliência e segurança. A estrutura organiza os serviços em camadas lógicas que representam diferentes responsabilidades dentro do sistema.

## Estrutura da Arquitetura

### Camada 1: Edge e Entrada
**Função:** Gerenciar o tráfego de entrada e fornecer proteção na borda da rede

- **Route S3**: Serviço de DNS para roteamento de tráfego e health checks
- **CloudFront**: CDN para distribuição de conteúdo estático e dinâmico
- **AWS WAF**: Firewall de aplicação web para proteção contra ameaças
- **Application Load Balancer**: Balanceamento de carga em nível de aplicação
- **API Gateway**: Gerenciamento de APIs REST e HTTP

### Camada 2: Computação e Microsserviços
**Função:** Execução da lógica de negócio em containers e funções

- **Amazon EKS**: Orquestração de containers Kubernetes para microsserviços
- **Amazon ECS Fargate**: Opção serverless para execução de containers
- **AWS Lambda**: Funções para processamento event-driven
- **Auto Scaling Group**: Instâncias EC2 para workloads stateful
- **Service Mesh**: Istio/Envoy para gerenciamento de tráfego entre serviços

**Exemplos de Microsserviços:**
- User Service: Gerenciamento de usuários e autenticação
- Order Service: Processamento de pedidos
- Payment Service: Integração com gateways de pagamento
- Catalog Service: Catálogo de produtos

### Camada 3: Dados e Armazenamento
**Função:** Persistência de dados e armazenamento

- **Amazon Aurora**: Banco relacional com replicação Multi-AZ
- **DynamoDB**: Banco NoSQL para alta performance
- **ElastiCache**: Cache em Redis para sessões e dados quentes
- **Amazon S3**: Armazenamento de objetos para mídia e backups

### Camada 4: Mensageria e Streaming
**Função:** Comunicação assíncrona entre serviços

- **Amazon SQS**: Filas para desacoplamento de serviços
- **Amazon SNS**: Sistema pub/sub para notificações
- **EventBridge**: Barramento de eventos para integrações
- **Step Functions**: Orquestração de workflows complexos
- **Kinesis**: Processamento de streams de dados

### Camada 5: Observabilidade e Segurança
**Função:** Monitoramento, auditoria e gestão de segurança

- **CloudWatch**: Coleta de métricas e logs
- **X-Ray**: Tracing distribuído para diagnóstico
- **CloudTrail**: Auditoria de atividades da AWS
- **GuardDuty**: Detecção de ameaças
- **Secrets Manager**: Gestão de credenciais

### Camada 6: CI/CD e Infraestrutura
**Função:** Automação de deploy e gestão de infraestrutura

- **CodePipeline**: Pipeline de integração e entrega
- **CodeBuild**: Serviço de build e teste
- **CodeDeploy**: Automação de deployment
- **IAM**: Gestão de identidade e acesso
- **CloudFormation**: Infraestrutura como código

## Fluxos de Trabalho

### Fluxo Síncrono (Request/Response)
1. Requisição do usuário via DNS (Route 53)
2. Passa pela CDN (CloudFront) e proteção (WAF)
3. Balanceamento de carga (ALB) e API Gateway
4. Processamento pelos microsserviços no EKS
5. Acesso aos bancos de dados (Aurora/DynamoDB)
6. Retorno da resposta ao usuário

### Fluxo Assíncrono (Event-driven)
1. Serviço publica evento no SQS/SNS
2. Lambda functions ou workers consomem as mensagens
3. Processamento em background
4. Atualização em bancos de dados
5. Notificações via EventBridge quando necessário

### Fluxo de Observabilidade
1. Serviços emitem métricas para CloudWatch
2. Traces distribuídos coletados via X-Ray
3. Logs centralizados para análise
4. Alertas configurados para métricas críticas

## Vantagens da Arquitetura

- **Escalabilidade**: Auto-scaling nativo em todos os componentes
- **Resiliência**: Multi-AZ e replicação de dados
- **Segurança**: Proteção em camadas com WAF, IAM e encriptação
- **Desacoplamento**: Serviços independentes com comunicação assíncrona
- **Observabilidade**: Monitoramento completo da stack
- **Custo-efetividade**: Pagamento por uso e opções serverless

## Considerações de Implementação

- **VPC Design**: Subnets públicas e privadas em 3 AZs
- **Network Security**: Security Groups e NACLs adequadamente configurados
- **Data Persistence**: Estratégias de backup e recovery definidas
- **Disaster Recovery**: Planos para failover entre regiões quando necessário
- **Cost Management**: Tagging consistente e monitoramento de custos

## Diagrama da Arquitetura

O diagrama correspondente a esta arquitetura está disponível no formato draw.io (.xml) e pode ser visualizado importando o arquivo na ferramenta.

## Próximos Passos

1. Customizar a arquitetura conforme requisitos específicos do projeto
2. Definir políticas de segurança e compliance
3. Estabelecer métricas de monitoramento e alertas
4. Implementar pipelines de CI/CD
5. Configurar estratégias de backup e disaster recovery

---

*Esta arquitetura serve como ponto de partida para implementações de microsserviços na AWS, podendo ser adaptada conforme requisitos específicos de cada projeto.*
