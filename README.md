# 📊 ChatController - Sistema de Chat Contábil (Showcase Architecture)

> **Aviso:** Este repositório é uma vitrine arquitetural (Showcase). Devido à sensibilidade dos dados contábeis e à propriedade intelectual envolvida, o código-fonte principal é mantido em um repositório privado. Aqui você encontrará a documentação da arquitetura, fluxo de dados e design do sistema.

## 💡 Sobre o Projeto
O **ChatController** é uma plataforma completa projetada para transformar a maneira como dados contábeis são analisados. O sistema integra uma interface conversacional intuitiva com serviços avançados de Inteligência Artificial, permitindo que os usuários façam consultas complexas em linguagem natural, automatizem a geração de relatórios e obtenham insights financeiros de forma ágil e segura.

## 🚀 Principais Funcionalidades
* **Interface Conversacional (Chat):** Comunicação em tempo real para consultas contábeis.
* **Análise de Dados com IA:** Interpretação de grandes volumes de dados financeiros utilizando modelos de Inteligência Artificial.
* **Automação de Relatórios:** Geração automatizada de balanços e demonstrativos com base nas interações do usuário.
* **Integração de APIs:** Comunicação fluida e assíncrona entre o painel do usuário, o servidor principal e os motores de IA.

---

## 🏗️ Arquitetura do Sistema e Stack Tecnológico

O sistema foi desenhado em uma arquitetura de microsserviços para garantir escalabilidade, resiliência e separação de responsabilidades.

### 1. Frontend: Plataforma de Chat (`/plataformachat`)
Responsável pela experiência do usuário e interface conversacional.
* **Stack:** React, Next.js
* **Papel:** Renderizar a interface de forma otimizada (SSR/SSG), gerenciar o estado da conversa e comunicar-se de forma segura com a API principal via requisições HTTP/WebSocket.

### 2. Backend: API Principal (`/server`)
O núcleo orquestrador do sistema.
* **Stack:** Node.js, Express/NestJS (ajuste conforme sua stack)
* **Papel:** Receber os prompts do usuário, gerenciar a autenticação/autorização, aplicar as regras de negócio iniciais e atuar como um Gateway de API, roteando as requisições pesadas para o serviço de IA.

### 3. Microsserviço de IA e Dados (`/iapython`)
O motor analítico da aplicação.
* **Stack:** Python, Pandas/NumPy, Bibliotecas de LLM (ex: LangChain, OpenAI API), SQL
* **Papel:** Receber os comandos em linguagem natural enviados pelo Node.js, converter as intenções do usuário em consultas SQL complexas, acessar o banco de dados contábil, processar os dados financeiros e retornar análises e relatórios estruturados para o servidor.

---

## 🔄 Fluxo de Dados (Data Flow)

1. **Input:** O usuário digita uma pergunta (ex: *"Gere o relatório de despesas operacionais do 3º trimestre"*) no frontend (React).
2. **Orquestração:** O Frontend envia o payload para a API em Node.js.
3. **Delegação:** O Node.js valida a requisição, verifica as permissões e encaminha o prompt via API interna para o microsserviço em Python.
4. **Processamento:** O Python aciona o modelo de IA, que entende o contexto contábil, executa a extração/cálculo no banco de dados e formata o relatório.
5. **Output:** A resposta é devolvida ao Node.js, que a repassa ao Frontend para ser exibida no chat do usuário.

---

## 🔒 Governança e Segurança de Dados
Devido à natureza crítica das informações (dados financeiros/contábeis), o sistema foi projetado com foco em:
* **Segurança de APIs:** Comunicação entre os serviços Node.js e Python protegida e validada.
* **Sanitização de Dados:** Tratamento rigoroso das entradas do usuário antes de qualquer execução no banco de dados para prevenir injeções de SQL.
* **Rastreabilidade:** Logs estruturados das consultas realizadas para fins de auditoria e monitoramento de performance.

---

## 📸 Demonstração Visual

*(Adicione aqui screenshots do painel ou um GIF demonstrando o chat em funcionamento)*

![ChatController Dashboard Demo](./assets/demo-placeholder.png)

> 🎥 **[Clique aqui para ver um vídeo de demonstração do sistema em funcionamento no YouTube/Loom]**

---

## 📂 Estrutura de Diretórios de Referência
Esta é a organização macro do repositório privado:

```text
/
├── /plataformachat    # Interface do chat (React/Next.js)
├── /server            # API orquestradora (Node.js)
└── /iapython          # Processamento de dados e IA (Python)
