# Arquitetura de Alto Nível - Sistema Fale Conosco

## 1. Visão Geral do Sistema

O sistema **Fale Conosco** é uma plataforma que centraliza a gestão e a realização de atendimentos ao público.  
Ele possibilita que **Solicitantes** abram chamados, enquanto **Atendentes**, **Gestores** e **Administradores** realizam o tratamento, acompanhamento e gestão das solicitações.

A solução é composta por aplicações web para os diferentes perfis de usuário, uma **API de Serviços** responsável pela lógica de negócio e integração com sistemas externos, além de uma **Base de Dados** que armazena as informações de forma estruturada.

## 2. Objetivos Arquiteturais

A arquitetura foi definida com os seguintes objetivos:

- **Separação clara de responsabilidades** entre apresentação, lógica de negócio e persistência.
- **Escalabilidade** para lidar com aumento de atendimentos, filas e operações simultâneas.
- **Integração segura** com o sistema corporativo de autenticação.
- **Flexibilidade para evolução**, permitindo inclusão de novos módulos, regras de negócio e fluxos.
- **Manutenibilidade**, baseada em uma estrutura modular e organizada por componentes.

## 3. Atores do Sistema

Os usuários identificados no sistema são:

- **Solicitante** – realiza a abertura e o acompanhamento de atendimentos.  
- **Atendente** – executa o atendimento, interage com o solicitante e conclui solicitações.  
- **Gestor** – administra unidades, acompanha métricas e supervisiona equipes.  
- **Administrador** – configura parâmetros globais e realiza a manutenção geral do sistema.  
- **Sistema de Autenticação** – serviço externo para login, perfis e verificação de identidade.

## 4. Arquitetura em Alto Nível

O sistema é dividido em quatro grandes blocos:

### 4.1. Portal do Solicitante (Aplicação Web - React)
Interface pública utilizada pelos solicitantes para abertura e consulta de atendimentos.

### 4.2. Aplicação Backoffice (Aplicação Web - React)
Interface destinada a Atendentes, Gestores e Administradores para:

- realizar atendimentos,
- gerenciar filas,
- configurar unidades,
- visualizar estatísticas.

### 4.3. API de Serviços (Java REST)
Responsável pela lógica de negócio, validações, regras do fluxo de atendimento, controle de filas, integrações com sistemas externos e persistência de dados.

### 4.4. Base de Dados (PostgreSQL)
Armazena informações de:

- atendimentos,
- usuários,
- unidades,
- configurações,
- estatísticas.

## 5. Diagrama de Alto Nível (C4 - Nível de Contêineres)

O diagrama de contêineres descreve como cada aplicação interage com a API e com o sistema de autenticação.  
Ele apresenta:

- Aplicações frontend (Portal + Backoffice),
- API de Serviços (backend),
- Base de Dados,
- Sistema de Autenticação,
- Atores externos.

## 6. Conclusão

Este documento apresenta uma visão geral da solução, descrevendo seus elementos principais e seus objetivos arquiteturais.  
A partir desta visão de alto nível, o próximo documento detalha internamente os componentes da API, permitindo entendimento aprofundado do funcionamento do sistema.
