# Trabalho Prático

# Documento de Requisitos do Sistema Fale Conosco

Este documento define os requisitos do sistema **Fale Conosco**, uma plataforma web desenvolvida para facilitar e organizar o atendimento ao público.

## 1. Introdução

### 1.1 Objetivo

Este documento define os requisitos do sistema Fale Conosco, que visa facilitar o atendimento ao público por meio de uma aplicação web, garantindo eficiência e organização na realização dos atendimentos.

### 1.2 Escopo

O sistema atende aos seguintes perfis de usuários:

* **Solicitantes**: Solicitar atendimento.
* **Atendentes**: Realizar atendimentos e controle de fila.
* **Gestores**: Configurar unidades de atendimento e visualizar estatísticas dos atendimentos realizados.
* **Administradores**: Gerenciamento global do sistema (unidades, usuários, atendimentos) e manutenção técnica.

### 1.3 Principais Funcionalidades

* Cadastro e autenticação de usuários.
* Atendimento de solicitações.
* Atribuição de atendentes nas unidades específicas.
* Configuração de unidades de atendimento.
* Geração de relatórios e estatísticas de atendimento das solicitações.
* Monitoramento e manutenção técnica do sistema.

### 1.4 Dependências

* Autenticação de usuários.

---

## 2. Requisitos Funcionais (RF)

### 2.1 Solicitante

| ID | Descrição | Prioridade |
| :--- | :--- | :--- |
| **RF001** | Permitir a seleção da unidade e tipo de atendimento. | Alta |
| **RF002** | Permitir a identificação (nome, CPF/CNPJ) e se o atendimento é preferencial. | Alta |
| **RF003** | Informar sobre a posição na fila de atendimento. | Alta |
| **RF004** | Permitir a solicitação de atendimento via videoconferência. | Alta |
| **RF005** | Permitir realizar uma avaliação do atendimento recebido. | Média |

### 2.2 Atendente

| ID | Descrição | Prioridade |
| :--- | :--- | :--- |
| **RF006** | Exibir a fila de atendimentos da unidade na ordenação padrão. | Alta |
| **RF007** | Oferecer interface de gestão de fila com filtros por tempo de espera, ordem de chegada, prioridades e tipo de atendimento. | Alta |
| **RF008** | Exibir um chat que permita comunicação bidirecional em tempo real com o Solicitante. | Alta |
| **RF009** | Permitir o encerramento do atendimento que foi concluído com sucesso. | Alta |
| **RF010** | Permitir o encerramento do atendimento por Inatividade do solicitante. | Média |
| **RF011** | Permitir a exibição de informações sobre atendimentos realizados (número, data/horário de início/fim, avaliação). | Média |
| **RF012** | Permitir que o Atendente defina seu status (Disponível, Ocupado, Ausente). | Média |
| **RF013** | Permitir a criação de anotações de trabalho vinculadas ao registro do atendimento, visíveis a outros Atendentes e Gestores da sua unidade. | Média |
| **RF014** | Enviar respostas rápidas pré-definidas em interações comuns via chat. | Média |

### 2.3 Gestor

| ID | Descrição | Prioridade |
| :--- | :--- | :--- |
| **RF015** | Permitir a alocação de um ou mais atendentes em uma unidade. | Alta |
| **RF016** | Permitir a edição de horários de funcionamento e tempo de inatividade máximo do chat (3-10 min). | Média |
| **RF017** | Permitir a edição das respostas rápidas pré-definidas para o chat da sua unidade. | Média |
| **RF018** | Exibir painel em tempo real com número de solicitantes na fila, tempo médio de espera, atendimentos em andamento e status de cada Atendente. | Alta |
| **RF019** | Exibir métricas históricas de atendimento e permitir download de relatório (tempo médio, quantidade, média de avaliação). | Média |

### 2.4 Administrador

| ID | Descrição | Prioridade |
| :--- | :--- | :--- |
| **RF020** | Permitir a criação de usuários com nível de acesso controlado via perfil assinalado. | Alta |
| **RF021** | Permitir inativar/deletar usuários. | Alta |
| **RF022** | Permitir a criação e edição das Unidades de Atendimento (nome, status, horários, gestor, atendente, link de videoconferência e respostas rápidas). | Alta |
| **RF023** | Disponibilizar painel e download do relatório com Visão Geral dos Atendimentos (total, tempo, avaliação, unidade, atendente). | Média |
| **RF024** | Permitir a criação e exibição de mensagens de avisos internos. | Média |
| **RF025** | Registrar logs de ações administrativas para auditoria. | Média |
| **RF026** | Gerar e permitir acesso a logs de erro para análise e manutenção. | Média |

---

## 3. Requisitos Não Funcionais (RNF)

| ID | Descrição | Categoria |
| :--- | :--- | :--- |
| **RNF001** | Sistema disponível **99,9%** do tempo (exceto manutenção). | Disponibilidade |
| **RNF002** | Suportar até **500 usuários simultâneos**, com tempo de resposta `< 2 segundos` para 95% das requisições. | Desempenho |
| **RNF003** | Criptografar dados sensíveis e exigir **MFA** para Administradores, Gestores e Atendentes. | Segurança |
| **RNF004** | A interface deve ser intuitiva. | Usabilidade |

---

## 4. Regras de Negócio (RN)

| ID | Descrição |
| :--- | :--- |
| **RN001** | Solicitantes devem fornecer identificação e número de processo (a depender do tipo de atendimento) válidos para solicitação. |
| **RN002** | Atendentes só podem visualizar atendimentos da **sua unidade**. |
| **RN003** | Gestores só podem configurar Atendentes e horário de funcionamento da **sua unidade**. |
| **RN004** | Atendimentos preferenciais têm **prioridade** na fila, conforme legislação aplicável. |
| **RN005** | O tempo máximo de inatividade no chat deve ser **configurável entre 3 e 10 minutos**. |

---

## 5. Matriz de Acessos (Resumo)

A hierarquia de perfis é: **Administrador > Gestor > Atendente > Solicitante**.

| Recurso | Solicitante | Atendente | Gestor | Administrador |
| :--- | :--- | :--- | :--- | :--- |
| **Atendimento** | Criar (C) | Ver (V) (unidade) | Ver/Editar (V/E) (unidade) | Ver (V) (global) |
| **Usuário** | * | * | V/E (alocar) | C/V/E/D |
| **Unidade** | * | V (própria) | V/E (própria) | C/V/E/D |
| **Logs** | * | * | * | V/C (admin/erros) |
| **Configurações** | * | V (próprias) | V/E (unidade) | C/V/E/D (global) |

> Legenda: **C** = Criar, **V** = Ver, **E** = Editar, **D** = Desativar/Deletar, **\*** = Sem permissão.

