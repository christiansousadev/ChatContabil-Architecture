# 📊 ChatContabil-Architecture - Inteligência Artificial Aplicada à Contabilidade

> **Aviso de Showcase:** Este repositório é uma vitrine arquitetural. Devido à sensibilidade dos dados contábeis (LGPD/Segredo de Negócio), o código-fonte principal é mantido de forma privada. Abaixo, detalho a engenharia por trás do sistema que integra bancos de dados contábeis, LLMs e automação de fluxos.

## 💡 Sobre o Projeto
O **ChatContabil** é um ecossistema inteligente que permite a gestores e contadores interagirem com dados financeiros complexos através de linguagem natural. O sistema não apenas responde perguntas, mas interpreta, processa e gera documentos contábeis oficiais (DRE, Balanço, Balancete e Razão) em tempo real, conectando o poder das LLMs à precisão dos dados de ERPs contábeis.

## 🚀 Diferenciais Técnicos
* **Extração de Relatórios via Chat:** Geração instantânea de DRE, Balanço Patrimonial, Balancetes e Razão apenas via comando de texto, respeitando períodos específicos e filtros de filiais.
* **Orquestração Multi-LLM:** Suporte híbrido para modelos:
    * **Locais (Privacidade):** Integração com **Phi-3** via Ollama para processamento local.
    * **Web/Cloud:** Integração via API com **Gemini, GPT-4, Grok e DeepSeek**.
* **RAG Personalizado (Retrieval-Augmented Generation):** Implementação de uma camada de recuperação que utiliza contexto contábil real para garantir que a IA não alucine sobre as normas brasileiras de contabilidade.
* **Automação via Fluxo de Nós:** Interface visual para criação de fluxos de automação (envio de relatórios, alertas de inconsistências) utilizando lógica baseada em grafos.

---

## 🏗️ Arquitetura e Stack

O sistema utiliza uma arquitetura de microsserviços desacoplados, garantindo que o processamento pesado de IA não afete a experiência do usuário no chat.

### 1. Frontend: Dashboard e Chat (`/plataformachat`)
* **Stack:** React 19, Next.js, Vite (Rolldown), TailwindCSS.
* **Recurso Key:** Uso de `@xyflow/react` para a criação da interface visual de automação por nós, permitindo ao usuário "desenhar" o fluxo de geração de relatórios.

### 2. Backend: Orquestrador (`/server`)
* **Stack:** Node.js (Express 5), JWT, Multer, Node-Cron, Swagger.
* **Papel:** Atua como Gateway de API. Gerencia a autenticação, faz o agendamento de tarefas (Cron), gera PDFs e arquivos Excel e orquestra a comunicação entre o usuário e o microsserviço de IA.

### 3. Microsserviço de IA e Dados (`/iapython`)
* **Stack:** Python (FastAPI), PyTorch, Transformers, Pandas, SQLAlchemy.
* **Engenharia de Dados:** Conexão híbrida via **Firebird** (sistemas legados) e **PostgreSQL** com **pgvector** para busca semântica no RAG.
* **Lógica Contábil:** Algoritmos para cálculo de DRE e Balancetes direto na camada de dados, enviando apenas o resultado estruturado para a LLM interpretar.

---

## 🔄 Funcionamento do Fluxo de Inteligência

1. **Intenção do Usuário:** O usuário solicita: *"Qual foi o lucro líquido da filial 1 no primeiro semestre?"*.
2. **Interpretação (LLM Router):** O sistema identifica que é uma consulta de DRE e aciona a estratégia de extração de dados.
3. **Execução Contábil:** O microsserviço Python executa as queries SQL no banco (Firebird/Postgres), aplica as regras de rollup e agrupamento de contas.
4. **Contextualização (RAG):** O RAG busca no histórico e nas normas da empresa se há particularidades para aquele período.
5. **Resposta Estruturada:** A LLM recebe os dados brutos + contexto e responde ao usuário com o valor e o link para o relatório (PDF/XLSX) gerado em segundos.

---

## 📸 Demonstração Visual

### Interface do Chat e Relatórios
*(Espaço para screenshot do chat gerando um DRE ou Balancete)*
![Interface do Chat](./assets/chat-demo.png)

### Automação de Fluxos (Workflows)
*(Espaço para screenshot da tela de nós/flowchart de automação)*
![Workflow de Automação](./assets/nodes-demo.png)

### Documentação da API (Swagger)
*(Espaço para screenshot do Swagger UI)*
![Documentação Swagger](./assets/swagger-demo.png)

---

## 📂 Estrutura de Diretórios
```text
/
├── /plataformachat    # Interface React 19 (Vite/Rolldown)
├── /server            # Gateway Node.js (Orquestração e Relatórios)
└── /iapython          # Motor de IA (Python, RAG, Integração Firebird)
