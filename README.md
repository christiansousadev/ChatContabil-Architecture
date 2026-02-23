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

📸 Demonstração Visual
🎨 Experiência de Entrada (UX/UI)
A interface foi projetada para ser moderna e intuitiva, com suporte total a temas Dark e Light e uma área de login segura que reforça a confiabilidade do sistema.

<p align="center">
<img width="48%" alt="LandingPage Black" src="https://github.com/user-attachments/assets/4ef1be78-f7a9-4b79-a53d-ef50078482e6" />
<img width="48%" alt="LandingPage White" src="https://github.com/user-attachments/assets/b1b44ab0-bc17-4c93-afc7-4220fc9b86c4" />
</p>

<p align="center">
<img width="60%" alt="Login" src="https://github.com/user-attachments/assets/0cf68c8b-96b1-47ab-ba6a-5778396e6fed" />
</p>

💬 O Core: Chat e Relatórios Inteligentes
O coração do sistema. Aqui o usuário interage em linguagem natural para extrair dados complexos. Note a precisão na geração do Resumo do Balancete, onde a IA interpreta os dados do banco e apresenta o resultado de forma legível antes de gerar o arquivo final.

<p align="center">
<img width="48%" alt="Chat 1" src="https://github.com/user-attachments/assets/0af87329-2264-411f-bd4c-8edf64579ae9" />
<img width="48%" alt="Chat 2" src="https://github.com/user-attachments/assets/0b469e12-4422-467e-a0aa-59ec783a6de8" />
</p>

⚙️ Painel Administrativo e Governança
Controle total sobre quem acessa o quê. O painel administrativo permite gerenciar usuários, permissões por empresa e monitorar logs, garantindo a conformidade com as políticas de segurança da informação.

<p align="center">
<img width="100%" alt="Painel Admin" src="https://github.com/user-attachments/assets/5d61bad4-0b26-450d-b75f-1dacb4ec0b08" />
</p>

<p align="center">
<img width="30%" alt="Menu Opções" src="https://github.com/user-attachments/assets/7eecdbdf-a7d8-4293-8dcb-5f775ed806c9" />
<img width="65%" alt="Perfil" src="https://github.com/user-attachments/assets/b71d795f-3639-4c7b-aa23-0f3ad64783f6" />
</p>

🤖 Configuração de IA e Prompt Engineering
O diferencial técnico: uma área dedicada para configurar múltiplos provedores de LLM (locais e cloud) e refinar os System Prompts. Isso permite "treinar" a IA para se comportar como um Auditor Sênior ou um Especialista em FP&A para cada tipo de relatório.

<p align="center">
<img width="100%" alt="LLM" src="https://github.com/user-attachments/assets/a798f63f-4ca4-43d0-9aab-db77e2cee50b" />
</p>

<p align="center">
<img width="100%" alt="Prompts" src="https://github.com/user-attachments/assets/9bbb4a3a-6ad3-4f4b-aad1-7b0f1dc1bdb2" />
</p>


⚙️ Automação de Fluxos (Workflows)
O ChatContabil vai além do chat passivo, permitindo a criação de Workflows Inteligentes. Através de uma interface baseada em nós (Node-based UI), é possível orquestrar tarefas complexas que conectam o banco de dados contábil a serviços externos e modelos de IA.

🛠️ Gerenciamento e Execução
O painel de controle permite gerenciar múltiplos fluxos de automação, monitorar taxas de sucesso e orquestrar integrações de forma visual e centralizada.

<p align="center">
<img width="100%" alt="API Manager" src="https://github.com/user-attachments/assets/eb7a04f0-eb8d-4957-84b6-50dd2f429070" />
</p>

🏗️ Anatomia de um Fluxo Contábil
A imagem abaixo demonstra um fluxo real de fechamento mensal:

Trigger: Ativado via Webhook ou agendamento cron.

Processamento: Execução de query SQL no Firebird, iteração de dados (Loop) e tomada de decisão lógica.

Ações: Geração automática do relatório (PDF/XLSX), upload para o Google Drive e envio de notificação por e-mail.

<p align="center">
<img width="100%" alt="Fluxo Automação" src="https://github.com/user-attachments/assets/48bb20f9-2f01-46f5-a7ca-d08eb974ba11" />
</p>

🧩 Biblioteca de Componentes (Nós)
O sistema conta com uma biblioteca extensível de blocos funcionais, incluindo:

Inteligência Artificial: Agentes autônomos baseados em GPT-4 ou Claude.

Conectores: SQL (Bancos de dados), Google Drive, SMTP (E-mail), HTTP Request.

Lógica Avançada: Código Javascript customizado, Condicionais (IF/ELSE) e Delays.

<p align="center">
<img width="50%" alt="Nós" src="https://github.com/user-attachments/assets/fd185398-97fe-4988-a7ac-3ba532404e8b" />
</p>

📖 Documentação da API (Swagger)
A arquitetura segue os padrões OpenAPI 3.0, garantindo que o sistema seja facilmente integrável com outros softwares. A documentação via Swagger detalha todos os endpoints de administração, configuração de LLMs e rotas de execução de IA, facilitando a manutenção e a escalabilidade técnica do projeto.

<p align="center">
<img width="100%" alt="Swagger" src="https://github.com/user-attachments/assets/f77c270f-cc0d-4d0d-841a-fff7e13e7f46" />
</p>
---

## 📂 Estrutura de Diretórios
```text
/
├── /plataformachat    # Interface React 19 (Vite/Rolldown)
├── /server            # Gateway Node.js (Orquestração e Relatórios)
└── /iapython          # Motor de IA (Python, RAG, Integração Firebird)
