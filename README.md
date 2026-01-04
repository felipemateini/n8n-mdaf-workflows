# Versão em Português

# MateiniFinPrd — Automação Inteligente de Captura de Despesas (n8n)

Workflow de automação que recebe **mensagens de voz pelo Telegram**, transcreve e analisa o áudio com **Google Gemini 2.5 Flash**, extrai dados estruturados de despesa e armazena os registros **aprovados** no **BigQuery**. Criado para **controle financeiro pessoal** com processamento de linguagem em **Português do Brasil**.

---

## ⚙️ Visão Geral do Fluxo

1. **Recebe mensagens do Telegram**
2. Envia mensagem solicitando **aguardar um instante**
3. Verifica se a mensagem contém um **arquivo de áudio (voz)**
4. Se sim:
   - Faz download do áudio
   - Envia para o **Gemini 2.5 Flash** para:
     - Transcrição
     - Extração de campos de despesa (data, categoria, valor, fonte, modalidade, etc.)
5. Converte a saída do Gemini em **JSON válido e tipado**
6. Solicita **aprovação do usuário (Aprovar/Reprovar)** com botões no Telegram
7. Se aprovado:
   - Insere o registro na tabela do **BigQuery**
   - Confirma sucesso no Telegram
8. Se reprovado:
   - Informa a recusa no Telegram
9. Se não houver áudio:
   - Solicita que o usuário **envie uma mensagem de voz**

---

## 🧠 Regras de Inteligência

- A data da despesa é interpretada com base na **data original da mensagem**
- A classificação segue uma **taxonomia fixa**, como:
  - *Alimentação → Restaurante*
  - *Investimento → Reserva de Emergência*
- Valores são extraídos de expressões naturais como:
  - `"45 reais"`
  - `"R$ 23,50"`
  - `"vinte e cinco"`
  - `"trinta com 60"`

---

## 🛠️ Tecnologias Utilizadas

| Camada | Tecnologia |
|---|---|
| Automação | n8n |
| Trigger | API do Telegram Bot |
| IA | Google Gemini 2.5 Flash |
| Transformação | Validação JavaScript + parsing JSON |
| Armazenamento | Google BigQuery |
| Versionamento | Git & GitHub |

---

## 📦 Requisitos

- Git instalado localmente
- Credenciais configuradas no n8n para:
  - **Telegram**
  - **Google Gemini**
  - **BigQuery OAuth2**
- Tabela no BigQuery criada com schema compatível:



# English version 

# MateiniFinPrd — Financial Expense Capture Automation (n8n)

An intelligent automation workflow that receives **voice messages via Telegram**, transcribes and analyzes them using **Google Gemini**, extracts structured expense data, and stores approved records in **BigQuery**. Designed for **Brazilian Portuguese financial speech processing** and personal finance tracking.

---

## ⚙️ Workflow Overview

1. **Receives Telegram messages**
2. Asks the user to **wait a moment**
3. Checks if the message contains a **voice audio file**
4. If yes:
   - Downloads the audio
   - Sends it to **Gemini 2.5 Flash** for:
     - Transcription
     - Expense field extraction (date, category, source, value, payment method, etc.)
5. Converts Gemini output into **clean validated JSON**
6. Requests user **approval (Aprovar/Reprovar)** via Telegram buttons
7. If approved:
   - Inserts the record into **BigQuery table `planejamento_familiar_001.f_debitos_`**
   - Confirms success on Telegram
8. If rejected:
   - Notifies refusal on Telegram
9. If no voice file:
   - Prompts the user to **send an audio message**

---

## 🧠 Intelligence Rules

- Audio is interpreted relative to the **original Telegram message date**
- Categories and sub-types follow strict predefined taxonomies (e.g., *Alimentação → Restaurante*, *Investimento → Reserva de Emergência*)
- Monetary values are parsed from natural speech expressions such as:
  - `"45 reais"`
  - `"R$ 23,50"`
  - `"vinte e cinco"`
  - `"trinta com 60"`

---

## 🛠️ Technologies Used

| Layer | Technology |
|---|---|
| Automation | n8n |
| Trigger | Telegram Bot API |
| AI Audio Analysis | Google Gemini 2.5 Flash |
| Transformation | JavaScript validation & JSON parsing |
| Storage | Google BigQuery (Cloud Data Warehouse) |
| Versioning | Git & GitHub |

---

## 📦 Requirements

- Git installed locally
- A Telegram Bot configured in n8n Credentials
- A Google Gemini (PaLM/Gemini) API Key configured in n8n
- BigQuery OAuth2 configured in n8n
- BigQuery table created with matching schema:
