# ⚽ Futebol Insights Bot

Automação de dados esportivos construída com **n8n**, integrando APIs de futebol, processamento de dados e um agente conversacional via Telegram.

## 📋 Sobre o projeto

Este projeto nasceu da ideia de aplicar automação e ciência de dados a um tema do dia a dia: futebol. Ele é composto por dois workflows complementares:

### 1. Resumo diário automatizado (`bot_diario_telegram.json`)
Workflow agendado que roda automaticamente todos os dias, consulta uma API de futebol, processa os dados dos jogos e retorna as informações relevantes.

**Fluxo:**
`Schedule Trigger` → `HTTP Request` (consulta a API de futebol) → `Code (Python)` (tratamento e estruturação dos dados)

### 2. Agente interativo de esportes (`agente_esportes.json`)
Um agente conversacional que responde perguntas sob demanda via Telegram, usando um LLM (Google Gemini) com memória de contexto para manter conversas coerentes.

**Fluxo:**
`Telegram Trigger` → `AI Agent` (com `Simple Memory` para contexto da conversa + `Google Gemini Chat Model` como modelo de linguagem) → `HTTP Request Tool` (busca dados esportivos sob demanda) → `Send a text message` (resposta ao usuário)

Além disso, o mesmo agente também dispara um resumo automático agendado (`Schedule Trigger` → `HTTP Request` → `Code (JavaScript)` → `Send a text message`).

## 🛠️ Tecnologias e conceitos aplicados

- **n8n** — orquestração visual de workflows
- **API-Football** — fonte de dados esportivos, consultada via parâmetro `date`
- **Telegram Bot API** — interface de entrada e saída para o usuário
- **Google Gemini (LLM)** — modelo de linguagem para o agente conversacional
- **Simple Memory (buffer window)** — controle de contexto para manter a conversa coerente sem estourar o limite de tokens
- **JavaScript e Python** (nós de código) — tratamento e transformação de dados dentro do próprio workflow

## 💡 Principais aprendizados técnicos

- A API-Football é consultada de forma mais confiável usando o parâmetro `date` diretamente.
- A interface em português do n8n pode corromper nomes de parâmetros HTTP; usar URLs dinâmicas com descrições em inglês (via toggle de expressão) é um workaround mais estável.
- Nem todo modelo de linguagem lida bem com *tool calls* dentro de agentes n8n — vale testar mais de um modelo até encontrar o que responde de forma confiável às ferramentas conectadas.
- Manter a janela de contexto da memória do agente enxuta evita estouro de tokens e respostas mais lentas ou inconsistentes.

## 📂 Estrutura do repositório

```
├── bot_diario_telegram.json     # Workflow de resumo diário agendado
├── agente_esportes.json          # Workflow do agente interativo + resumo agendado
└── README.md
```

## 🚀 Como importar no n8n

1. Abra sua instância do n8n
2. Vá em **Workflows → Import from File**
3. Selecione o arquivo `.json` desejado
4. Configure suas próprias credenciais (API-Football, Telegram Bot Token, Google Gemini API Key) — os workflows não incluem nenhuma credencial ou chave, apenas a estrutura da automação

## 👤 Autor

**Vinicios Oliveira** — Estudante de Ciência de Dados (FATEC Cotia)
[LinkedIn](https://www.linkedin.com/in/vinicios-oliveira-835947324)

---

*Projeto acadêmico desenvolvido para aplicar conceitos de automação, integração de APIs e IA generativa em um contexto prático e de interesse pessoal.*
