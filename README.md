## Visão Geral

Este projeto foi desenvolvido para o Tech Challenge da FIAP com o objetivo de implementar uma arquitetura AWS para hospedagem de uma aplicação de Feature Flags.

A solução foi construída utilizando serviços da AWS com foco em:

- Segurança
- Isolamento de rede
- Boas práticas de arquitetura cloud
- Separação entre camada de aplicação e banco de dados

A aplicação utilizada foi o projeto Toggle Master:

https://github.com/dougls/toggle-master-monolith

## Demonstração em Vídeo

Vídeo do projeto:
https://www.youtube.com/watch?v=UNmb7gWnkCQ

# Arquitetura

A arquitetura foi projetada utilizando uma VPC dedicada, com separação entre recursos públicos e privados.

A instância EC2 responsável pela aplicação está localizada em uma subnet pública, enquanto o banco PostgreSQL em RDS permanece isolado em subnets privadas.

O acesso externo ocorre através do Internet Gateway e toda comunicação com o banco acontece internamente dentro da VPC.

![Arquitetura AWS](docs/Archicheture-overview.png)

## Componentes AWS Utilizados

| Serviço | Finalidade |
|----------|------------|
| VPC | Isolamento da rede |
| Public Subnet | Hospedagem da EC2 |
| Private Subnets | Hospedagem do RDS |
| Internet Gateway | Acesso externo |
| EC2 | Execução da aplicação |
| RDS PostgreSQL | Persistência dos dados |
| Security Groups | Controle de acesso |

## Fluxo da Aplicação

1. O usuário acessa a aplicação via Internet.
2. A requisição passa pelo Internet Gateway.
3. O tráfego é direcionado para a instância EC2.
4. A aplicação processa a requisição.
5. Quando necessário, a EC2 consulta o banco PostgreSQL no RDS.
6. A resposta é retornada ao usuário.

O banco de dados permanece isolado e sem acesso direto pela internet.

## Segurança

Foram utilizadas as seguintes práticas:

### Security Group da EC2

- SSH (22) liberado apenas para IP autorizado.
- Porta 5000 liberada para acesso à aplicação.

### Security Group do RDS

- Porta 5432 liberada somente para a EC2.
- Sem acesso público.

### Isolamento de Rede

- EC2 em subnet pública.
- RDS em subnets privadas.
- Comunicação realizada apenas dentro da VPC.

## Documentação Completa

O passo a passo completo da implementação está disponível em:

docs/implementation-guide.md

## Autor

Jairo

FIAP Pós-Tech
DevOps & Cloud Computing
