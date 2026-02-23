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
<img width="1917" height="1024" alt="LandingPage Black" src="https://github.com/user-attachments/assets/4ef1be78-f7a9-4b79-a53d-ef50078482e6" />
<img width="1914" height="1026" alt="LandingPage White" src="https://github.com/user-attachments/assets/b1b44ab0-bc17-4c93-afc7-4220fc9b86c4" />
<img width="1918" height="1002" alt="Login" src="https://github.com/user-attachments/assets/0cf68c8b-96b1-47ab-ba6a-5778396e6fed" />
<img width="199" height="206" alt="Menu Opções" src="https://github.com/user-attachments/assets/7eecdbdf-a7d8-4293-8dcb-5f775ed806c9" />
<img width="705" height="699" alt="Perfil" src="https://github.com/user-attachments/assets/b71d795f-3639-4c7b-aa23-0f3ad64783f6" />

<img width="1362" height="594" alt="Chat 1" src="https://github.com/user-attachments/assets/0af87329-2264-411f-bd4c-8edf64579ae9" />
<img width="1917" height="898" alt="Chat 2" src="https://github.com/user-attachments/assets/0b469e12-4422-467e-a0aa-59ec783a6de8" />
<img width="1688" height="557" alt="Chat 3" src="https://github.com/user-attachments/assets/b44b1dbc-043f-4888-b7f5-53f9960493c3" />
<img width="1913" height="616" alt="Painel Admin" src="https://github.com/user-attachments/assets/5d61bad4-0b26-450d-b75f-1dacb4ec0b08" />
<img width="1854" height="799" alt="LLM" src="https://github.com/user-attachments/assets/a798f63f-4ca4-43d0-9aab-db77e2cee50b" />
<img width="1863" height="547" alt="Prompts" src="https://github.com/user-attachments/assets/9bbb4a3a-6ad3-4f4b-aad1-7b0f1dc1bdb2" />


### Automação de Fluxos (Workflows)
<img width="1845" height="445" alt="API Manager" src="https://github.com/user-attachments/assets/eb7a04f0-eb8d-4957-84b6-50dd2f429070" />
<img width="1906" height="903" alt="Fluxo Automação" src="https://github.com/user-attachments/assets/48bb20f9-2f01-46f5-a7ca-d08eb974ba11" />
<img width="453" height="599" alt="Nós" src="https://github.com/user-attachments/assets/fd185398-97fe-4988-a7ac-3ba532404e8b" />


### Documentação da API (Swagger)
<img width="1985" height="1035" alt="Swagger" src="https://github.com/user-attachments/assets/f77c270f-cc0d-4d0d-841a-fff7e13e7f46" />

---

## 📂 Estrutura de Diretórios
```text
/
├── /plataformachat    # Interface React 19 (Vite/Rolldown)
├── /server            # Gateway Node.js (Orquestração e Relatórios)
└── /iapython          # Motor de IA (Python, RAG, Integração Firebird)
