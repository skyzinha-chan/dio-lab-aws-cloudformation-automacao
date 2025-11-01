# Desafio DIO: Implementando Infraestrutura Automatizada com AWS CloudFormation

Este repositório documenta a implementação do desafio "Implementando Infraestrutura Automatizada com AWS CloudFormation", parte do bootcamp da DIO. O objetivo é explorar como o CloudFormation vai além da simples criação de recursos, permitindo a automação, padronização e replicação de infraestruturas complexas.

## O que é Infraestrutura como Código (IaC)?

Infraestrutura como Código (IaC) é a prática de gerenciar e provisionar infraestrutura (redes, servidores, bancos de dados) através de arquivos de definição legíveis por máquina (como `.yaml` ou `.json`), em vez de configuração manual ou ferramentas interativas.

O AWS CloudFormation é o serviço nativo da AWS para IaC.

## Conceitos-Chave da Automação (Foco do Desafio)

Este laboratório focou em conceitos que permitem a automação em larga escala:

### 1. Padronização

O uso de templates garante que os recursos sejam sempre criados com a mesma configuração. Isso elimina o "drift" de configuração (diferenças entre ambientes).

* **Exemplo:** Um template define um Security Group padrão para todos os servidores web, garantindo que as portas corretas (80, 443) estejam sempre abertas e portas de gerenciamento (22, 3389) estejam sempre fechadas para a internet.

### 2. Replicação

Com um template parametrizado, é possível replicar uma arquitetura inteira de forma rápida e confiável.

* **Exemplo:** O mesmo template pode ser usado para criar ambientes idênticos para `Desenvolvimento`, `Homologação` e `Produção` simplesmente alterando os parâmetros de entrada (como o tipo de instância ou o nome do ambiente).

### 3. Segurança como Código

A infraestrutura de segurança também é definida no código. Isso permite auditorias de segurança, revisões de pull request para mudanças de firewall e um histórico de versionamento de quem alterou o quê.

* **Exemplo:** Definição de `IAM Roles` e `Policies` diretamente no template, garantindo que as permissões sejam aplicadas de forma consistente junto com os recursos que as utilizam.

## Formatos de Modelo: JSON vs. YAML

O CloudFormation aceita ambos os formatos:

* **JSON:** Formato mais rigoroso e menos propenso a erros de sintaxe (como indentação). Pode se tornar verboso.
* **YAML:** Muito mais legível para humanos, permite comentários (essencial para documentação) e é geralmente o formato preferido para templates complexos.

## Análise: AWS CloudFormation vs. Terraform

Um ponto importante do módulo foi a comparação entre as principais ferramentas de IaC do mercado:

| Característica | AWS CloudFormation | Terraform (by HashiCorp) |
| :--- | :--- | :--- |
| **Escopo** | Focado 100% na AWS. Nativo. | Multi-Cloud (AWS, Azure, GCP, etc.). |
| **Sintaxe** | JSON ou YAML. | HCL (HashiCorp Configuration Language). |
| **Gerenciamento de Estado** | Gerenciado automaticamente pela AWS (na própria Stack). | Gerenciado pelo usuário (normalmente em um bucket S3) ou pelo Terraform Cloud. |
| **Recursos** | Suporte imediato (Dia 0) para novos serviços da AWS. | Depende da comunidade/HashiCorp para atualizar o "provider". |
| **Plano de Execução** | O "Change Set" (conjunto de alterações) mostra o que será alterado. | O `terraform plan` é considerado por muitos como mais legível e claro. |

## Insights e Documentação da Experiência

Este desafio solidificou a diferença entre "criar uma stack" e "gerenciar infraestrutura".

O verdadeiro poder do CloudFormation não está em subir uma única instância EC2, mas em definir um arquivo `network.yaml` que cria uma VPC inteira e um `app.yaml` que consome os *Outputs* (como o ID da VPC) do primeiro template.

A prática de tratar a infraestrutura como código — versionando-a no Git, revisando mudanças em Pull Requests e automatizando a aplicação em um pipeline de CI/CD — é o pilar central de operações de nuvem modernas e maduras. O CloudFormation é a ferramenta fundamental para alcançar isso dentro do ecossistema AWS.
