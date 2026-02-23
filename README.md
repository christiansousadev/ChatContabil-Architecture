# 📊 ChatContabil-Architecture - Inteligência Artificial Aplicada à Contabilidade

> **⚠️ Aviso de Showcase:** Este repositório é uma vitrine arquitetural. Devido à sensibilidade dos dados contábeis e à propriedade intelectual envolvida (LGPD), o código-fonte principal é mantido de forma privada. Abaixo, detalho a engenharia por trás do sistema que integra bancos de dados contábeis, LLMs e automação de fluxos.

## 💡 Sobre o Projeto

O **ChatContabil** é um ecossistema inteligente que permite a gestores e contadores interagirem com dados financeiros complexos através de linguagem natural. O sistema não apenas responde perguntas, mas interpreta, processa e gera documentos contábeis oficiais (**DRE, Balanço, Balancete e Razão**) em tempo real, conectando o poder das LLMs à precisão dos dados de ERPs contábeis.

## 🚀 Diferenciais Técnicos

* **Extração de Relatórios via Chat:** Geração instantânea de relatórios contábeis apenas via comando de texto, respeitando períodos específicos e filtros de filiais.
* **Orquestração Multi-LLM:** Suporte híbrido para diversos modelos:
* **Modelos Locais:** Integração com **Phi-3** via Ollama para garantir privacidade total dos dados.
* **Modelos em Nuvem:** Integração via API com **Gemini, GPT-4, Grok e DeepSeek**.


* **RAG Personalizado (Retrieval-Augmented Generation):** Camada de recuperação que utiliza contexto contábil real para garantir que a IA não alucine e respeite as normas brasileiras de contabilidade.
* **Automação via Fluxo de Nós:** Interface visual baseada em grafos para criação de fluxos de automação, como envio de relatórios e alertas de inconsistências.

---

## 🏗️ Arquitetura e Stack

O sistema utiliza uma arquitetura de microsserviços desacoplados, garantindo que o processamento pesado de IA não afete a experiência de uso.

### **Frontend: Dashboard e Chat (`/plataformachat`)**

* **Stack Principal:** React 19, Next.js, Vite (Rolldown) e TailwindCSS.
* **Recurso Key:** Implementação do `@xyflow/react` para criar a interface visual de automação, permitindo ao usuário "desenhar" seus próprios fluxos de dados.

### **Backend: Orquestrador API (`/server`)**

* **Stack Principal:** Node.js (Express 5), JWT, Multer, Node-Cron e Swagger.
* **Papel no Sistema:** Atua como o Gateway principal. Gerencia autenticação, agendamentos (Cron), geração de arquivos (PDF/Excel) e a orquestração entre o usuário e o serviço de IA.

### **Microsserviço de IA e Dados (`/iapython`)**

* **Stack Principal:** Python (FastAPI), PyTorch, Transformers, Pandas e SQLAlchemy.
* **Engenharia de Dados:** Conexão híbrida via **Firebird** (sistemas legados) e **PostgreSQL** com **pgvector** para buscas semânticas de alta precisão.
* **Lógica Contábil:** Algoritmos dedicados para cálculos financeiros complexos direto na camada de dados antes da interpretação da LLM.

---

## 🔄 Funcionamento do Fluxo de Inteligência

* **Identificação de Intenção:** O usuário solicita uma informação (ex: *"Qual foi o lucro líquido da filial 1 no primeiro semestre?"*).
* **Roteamento (LLM Router):** O sistema identifica o tipo de relatório necessário e aciona a estratégia de extração de dados adequada.
* **Execução Contábil:** O microsserviço Python processa as queries SQL no banco de dados, aplicando regras de rollup e agrupamento de contas.
* **Contextualização via RAG:** O sistema busca no histórico e nas normas da empresa particularidades que devam ser consideradas para aquele período.
* **Entrega Estruturada:** A LLM recebe os dados brutos processados e responde ao usuário com a análise textual e o link para o relatório (PDF/XLSX) gerado.

📸 Demonstração Visual
🎨 Experiência de Entrada (UX/UI)
A interface foi projetada para ser moderna e intuitiva, com suporte total a temas Dark e Light e uma área de login segura.

<p align="center">
<img width="48%" alt="LandingPage Black" src="https://github.com/user-attachments/assets/4ef1be78-f7a9-4b79-a53d-ef50078482e6" />
<img width="48%" alt="LandingPage White" src="https://github.com/user-attachments/assets/b1b44ab0-bc17-4c93-afc7-4220fc9b86c4" />
</p>

<p align="center">
<img width="60%" alt="Login" src="https://github.com/user-attachments/assets/0cf68c8b-96b1-47ab-ba6a-5778396e6fed" />
</p>

💬 O Core: Chat e Relatórios Inteligentes
O coração do sistema, onde a IA interpreta os dados do banco e apresenta resultados legíveis antes da geração do arquivo final.

<p align="center">
<img width="48%" alt="Chat 1" src="https://github.com/user-attachments/assets/0af87329-2264-411f-bd4c-8edf64579ae9" />
<img width="48%" alt="Chat 2" src="https://github.com/user-attachments/assets/0b469e12-4422-467e-a0aa-59ec783a6de8" />
</p>

⚙️ Painel Administrativo e Governança
Controle total de permissões por empresa e monitoramento de logs de segurança.

<p align="center">
<img width="100%" alt="Painel Admin" src="https://github.com/user-attachments/assets/5d61bad4-0b26-450d-b75f-1dacb4ec0b08" />
</p>

<p align="center">
<img width="30%" alt="Menu Opções" src="https://github.com/user-attachments/assets/7eecdbdf-a7d8-4293-8dcb-5f775ed806c9" />
<img width="65%" alt="Perfil" src="https://github.com/user-attachments/assets/b71d795f-3639-4c7b-aa23-0f3ad64783f6" />
</p>

🤖 IA e Prompt Engineering
Área dedicada para configurar provedores de LLM e refinar os System Prompts para cada tipo de auditoria ou relatório.

<p align="center">
<img width="100%" alt="LLM" src="https://github.com/user-attachments/assets/a798f63f-4ca4-43d0-9aab-db77e2cee50b" />
</p>

<p align="center">
<img width="100%" alt="Prompts" src="https://github.com/user-attachments/assets/9bbb4a3a-6ad3-4f4b-aad1-7b0f1dc1bdb2" />
</p>

⚙️ Automação de Fluxos (Workflows)
Interface de automação visual para orquestrar tarefas complexas conectando banco de dados, IA e serviços externos.

API Manager: Painel de controle para gerenciar e monitorar a saúde dos fluxos.

<p align="center">
<img width="100%" alt="API Manager" src="https://github.com/user-attachments/assets/eb7a04f0-eb8d-4957-84b6-50dd2f429070" />
</p>

Anatomia do Fluxo: Exemplo de fluxo com Trigger (Webhook), Processamento (SQL/Loop) e Ações (Drive/Email).

<p align="center">
<img width="100%" alt="Fluxo Automação" src="https://github.com/user-attachments/assets/48bb20f9-2f01-46f5-a7ca-d08eb974ba11" />
</p>

Biblioteca de Nós: Componentes prontos para IA, Conectores de dados e Lógica Avançada.

<p align="center">
<img width="50%" alt="Nós" src="https://github.com/user-attachments/assets/fd185398-97fe-4988-a7ac-3ba532404e8b" />
</p>

📖 Documentação da API (Swagger)
Padronização seguindo OpenAPI 3.0 para garantir integrabilidade e escalabilidade.

<p align="center">
<img width="100%" alt="Swagger" src="https://github.com/user-attachments/assets/f77c270f-cc0d-4d0d-841a-fff7e13e7f46" />
</p>

📂 Estrutura de Diretórios
Plaintext
/plataformachat
├── /src
│   ├── /pages           # Telas principais (Chat, Admin, RAG, Workflow Editor)
│   ├── /components      # Componentes modulares e reutilizáveis
│   │   └── /api         # Módulos de gestão de monitoramento, relatórios e automação
│   │       └── /workflows # Engine visual de automação (Nodes, Edges e UI)
│   ├── /hooks           # Custom Hooks para lógica de API, Webhooks e Fluxos
│   ├── /utils           # Helpers de formatação, validação, auth e storage
│   ├── /assets          # Ativos estáticos e identidade visual da plataforma
│   ├── App.jsx          # Orquestrador de rotas e contextos globais
│   └── main.jsx         # Ponto de entrada da aplicação
├── /cert                # Certificados SSL para ambiente de desenvolvimento seguro
├── /public              # Ativos públicos acessíveis via raiz
├── Dockerfile.web* # Arquivos de containerização (Dev e Produção)
├── docker-compose* # Orquestração de ambientes multi-stage
├── tailwind.config.js   # Configuração do motor de design system
└── vite.config.js       # Configuração do Bundler e Proxy reverso

/server
├── /rotas               # Definição de endpoints Express
│   ├── /apimanager      # Rotas para gestão de chaves, fluxos e agendamentos
│   ├── /components      # Lógica de rotas específicas (Chat DRE, Balanço, Razão)
│   └── index.js         # Centralizador de rotas
├── /services            # A "Engenharia" do sistema
│   ├── /workflows       # Motor de Automação (Engine e histórico)
│   │   └── /nodes       # Implementação individual de cada nó (SQL, HTTP, IF, etc.)
│   ├── /apimanager      # Serviços de suporte (Proxy, Scheduler, DB Helpers)
│   └── llm_interpret.js # Integração e interpretação de prompts via LLM
├── /lib                 # Bibliotecas utilitárias e wrappers
│   ├── auth.js          # Middleware de autenticação e JWT
│   ├── llm.js           # Wrapper para comunicação com provedores de IA
│   └── swagger.js       # Configuração da documentação OpenAPI
├── /docs                # Documentação OpenAPI/Swagger modularizada (YAML)
│   ├── chat.yaml, dre.yaml, workflows.yaml, etc.
├── /storage             # Persistência de arquivos (Relatórios, Avatares, Logs)
├── index.js             # Ponto de entrada da aplicação
├── db.js                # Singleton de conexão com o banco de dados
├── nlp_config.json      # Configurações de processamento de linguagem natural
└── Dockerfile           # Receita para deploy em containers

/iapython
├── /balancete, /balanco, /dre, /razao   # Módulos core de extração e lógica contábil
│   ├── api_*.py                         # Endpoints específicos de cada relatório
│   └── *_core.py                        # Regras de negócio e processamento de dados
├── /rag                                 # Camada de Retrieval-Augmented Generation
│   ├── rag_*.py                         # Estratégias de recuperação por tipo de relatório
│   ├── rag_index.py                     # Orquestração de busca semântica
│   └── nlp_config.json                  # Configurações de processamento de linguagem
├── /reports                             # Geração de documentos (PDF/XLSX/CSV)
│   ├── report_*.py                      # Templates e formatação de saída
│   └── report_index.py                  # Gerenciador de exportações
├── /sql                                 # Repositório de queries SQL otimizadas
│   ├── balanco.sql, balancete.sql, etc. # Consultas nativas para o banco Firebird/Postgres
├── /services                            # Camada de infraestrutura e utilitários
│   ├── db.py                            # Gerenciamento de conexões (Firebird/SQLAlchemy)
│   └── utils.py                         # Funções auxiliares de sanitização e cálculo
├── /data                                # Metadados e estruturas de configuração (JSON)
├── /cache                               # Armazenamento temporário de processamentos (ignorado no git)
├── main.py                              # Ponto de entrada da API FastAPI
├── requirements.txt                     # Dependências do motor de IA e Dados
└── Dockerfile                           # Configuração de containerização do micr

**Desenvolvido por Christian Sousa**
*Desenvolvimento de sistemas inteligentes e automação.*
