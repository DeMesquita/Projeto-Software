# Arquitetura Detalhada – Componentes do Sistema Fale Conosco

## 1. Introdução

Este documento detalha a arquitetura interna da **API de Serviços** do sistema Fale Conosco, utilizando o **Nível de Componentes do Modelo C4**.  
Aqui são descritas as camadas, os componentes responsáveis pela lógica de negócio e suas relações com a base de dados e sistemas externos.

---

## 2. Estrutura Arquitetural da API

A API segue uma organização em três camadas principais:

### ✔ 2.1. Camada de Controllers (Entrada HTTP - REST)

Os *controllers* são responsáveis por receber as requisições HTTP provenientes do Portal e do Backoffice.  
Eles fazem validações iniciais, chamam os serviços correspondentes e retornam as respostas ao cliente.

**Principais componentes:**

- `AtendimentoController`
- `FilaController`
- `UsuarioController`
- `UnidadeController`
- `ConfiguracaoController`
- `EstatisticasController`

---

### ✔ 2.2. Camada de Services (Regras de Negócio)

Implementa as regras e processos centrais do sistema.  
Aqui ocorrem validações avançadas, cálculos, manipulação do fluxo de atendimento, operações de fila e comunicação com integrações externas.

**Responsabilidades incluem:**

- Criar, atualizar e encerrar atendimentos.
- Gerenciar a fila de atendimento.
- Consultar métricas e estatísticas.
- Configurar parâmetros da plataforma.
- Executar lógicas de autenticação via serviço externo.

**Principais componentes:**

- `AtendimentoService`
- `FilaService`
- `UsuarioService`
- `UnidadeService`
- `ConfiguracaoService`
- `EstatisticasService`
- `AuthClient` (integração via HTTP com o Sistema de Autenticação)
- `ChatGateway` (processamento de eventos WebSocket)

---

### ✔ 2.3. Camada de Repositórios (Persistência de Dados)

Os repositórios acessam o banco de dados utilizando modelos de domínio e operações CRUD.  
Cada repositório é responsável por um conjunto específico de dados.

**Principais componentes:**

- `AtendimentoRepository`
- `UsuarioRepository`
- `UnidadeRepository`
- `ConfiguracaoRepository`
- `EstatisticasRepository`

Esses componentes interagem diretamente com a **Base de Dados (PostgreSQL)** utilizando JDBC ou outra solução de persistência adotada.

---

## 3. Integrações Externas

### ✔ 3.1. Sistema de Autenticação
A API consulta perfis, permissões e valida credenciais via componente `AuthClient`.

### ✔ 3.2. Comunicação em tempo real (Chat)
O `ChatGateway` envia eventos de atendimento em tempo real para as interfaces que exibem o chat ao usuário.

---

## 4. Diagrama de Componentes (C4 - Nível 3)

O diagrama apresenta visualmente:

- Controllers e seus fluxos
- Services e suas responsabilidades
- Repositórios e persistência
- Integração com sistemas externos
- Fluxos entre camadas e DB

O diagrama gerado no arquivo `diagramas_components.puml` representa fielmente essa organização.

---

## 5. Relação entre Requisitos e Componentes

Alguns exemplos:

- **RF - Criar atendimento**  
  AtendimentosController → AtendimentoService → AtendimentoRepository → DB

- **RF - Gerenciar fila**  
  FilaController → FilaService → AtendimentoRepository

- **RF - Consultar estatísticas**  
  EstatisticasController → EstatisticasService → EstatisticasRepository

- **RF - Autenticação de usuário**  
  UsuarioController → UsuarioService → AuthClient → Sistema de Autenticação

---

## 6. Conclusão

A arquitetura detalhada permite compreender claramente como o sistema está organizado internamente.  
O uso do modelo C4 facilita a evolução, comunicação entre membros da equipe e garante que a solução esteja alinhada com boas práticas de projeto de software.
