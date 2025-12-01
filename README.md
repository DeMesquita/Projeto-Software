# 🗺️ Documentação da Arquitetura C4 do Sistema Fale Conosco

## 1. Nível de Contexto: Canal de Atendimento Fale Conosco

### Descrição do Diagrama

O **Diagrama de Contexto** do sistema **Fale Conosco**.

* **Sistema Principal:** O **Fale Conosco** é a plataforma central para gestão de filas e realização de atendimentos.
* **Pessoas (Usuários):** Quatro perfis de usuários interagem diretamente com o sistema por meio de uma Interface Web:
    * **Solicitantes:** Buscam e solicitam atendimento.
    * **Atendentes:** Realizam atendimentos e controlam a fila.
    * **Gestores:** Configuram unidades de atendimento e visualizam estatísticas.
    * **Administradores:** Realizam gerenciamento global e manutenção técnica.
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
