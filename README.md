# 🗺️ Documentação da Arquitetura C4 do Sistema Fale Conosco

## 1. Nível de Contexto: Canal de Atendimento Fale Conosco

### Descrição do Diagrama

O **Diagrama de Contexto** do sistema **Fale Conosco**.

* **Sistema Principal:** O **Fale Conosco** é a plataforma central para gestão de filas e realização de atendimentos.
* **Pessoas (Usuários):** Quatro perfis de usuários interagem diretamente com o sistema por meio de uma Interface Web:
    * **Solicitantes:** Buscam e solicitam atendimento.
    * **Atendentes:** Realizam atendimentos e controlam a fila.
    * **Gestores:** Configuram unidades de atendimento e visualizam estatísticas.
    * **Administradores:** Realizam operação e manutenção técnica.
* **Sistemas Externos:** O sistema depende do **Sistema de Autenticação** corporativo, que gerencia as identidades e perfis dos usuários. A comunicação para autenticação é feita via **HTTPS**.
Trabalho Final/out/diagrama_conteiner
![Diagrama de Contexto](Trabalho%20Final/out/diagrama_contexto/diagrama_contexto.png)


## 2. Nível de Contêineres: Fale Conosco
#### Fluxo de Comunicação:

1.  **Usuários $\to$ Frontends:** Todos os usuários acessam o sistema pela Interface Web.
2.  **Frontends $\to$ API:** Ambas as aplicações **React** se comunicam com a **API de Serviços (Java)** para ler e escrever dados via **HTTPS/JSON**.
3.  **API $\to$ Base de Dados:** A **API de Serviços** acessa e manipula os dados na **Base de Dados (PostgreSQL)**, usando **JDBC**.
4.  **API $\to$ Sistema Externo:** A **API de Serviços** consulta o **Sistema de Autenticação** externo (via **HTTPS**) para validar credenciais e buscar perfis.
![Diagrama de Contêiner](Trabalho%20Final/out/diagrama_conteiner/diagrama_conteiner.png)

## 3. Nível de Componentes: Fale Conosco

### Descrição Geral

O **Nível de Componentes** detalha a estrutura interna de cada contêiner do sistema Fale Conosco.  
Enquanto o nível de contêineres descreve *o que existe*, este nível mostra *como cada parte é organizada internamente*, destacando responsabilidades, fluxos de comunicação e separação das camadas.

A seguir, os três diagramas de componentes são apresentados com suas respectivas explicações.

---

### 3.1. Componentes da API de Serviços (Java REST)

O diagrama da API de Serviços mostra a distribuição interna da aplicação responsável por toda a lógica de negócio, fila de atendimentos, regras operacionais e persistência de dados.

A API está organizada em:

- **Controllers (REST/WebSocket)** — Recebem requisições dos frontends.  
- **Services** — Implementam regras de negócio.  
- **Repositórios** — Realizam a persistência dos dados no PostgreSQL.  
- **Cliente de Autenticação** — Integra com o Sistema de Autenticação corporativo.

![Diagrama de Componentes – API de Serviços](Trabalho%20Final/out/diagrama_components/diagrama_componentes1.png)

---

### 3.2. Componentes do Portal do Solicitante (Aplicação Web – React)

O Portal do Solicitante é acessado pelo público externo e permite:

- Abertura de atendimentos  
- Consulta de status e detalhes  
- Autenticação  

A aplicação é organizada em:

- **Interface Web (React SPA)**  
- **Módulos de Solicitação e Consulta**  
- **Cliente de API para comunicação com a API de Serviços**  
- **Cliente de Autenticação via HTTPS**

![Diagrama de Componentes – Portal do Solicitante](Trabalho%20Final/out/diagrama_components/diagrama_componentes2.png).

---

### 3.3. Componentes da Aplicação Backoffice (Aplicação Web – React)

A Aplicação Backoffice é utilizada por Atendentes, Gestores e Administradores.  
Suas principais funções são:

- Operação de atendimentos  
- Consulta e atualização da fila  
- Gerenciamento de unidades  
- Visualização de dashboards e métricas  
- Autenticação interna  

Os principais módulos são:

- **Fila de Atendimentos**  
- **Atendimento**  
- **Gestão de Unidades**  
- **Dashboards e Métricas**  
- **Cliente de API Backoffice**  
- **Cliente de Autenticação**

![Diagrama de Componentes – Aplicação Backoffice](Trabalho%20Final/out/diagrama_components/diagrama_componentes3.png).

---

