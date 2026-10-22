# Multilingual Phishing Detection with LLMs (Kazakh · Russian · English)

Pre-Defense 1 repository.
Developer: Imanbayev Islam (GitHub: Islam-ITUni)
Supervisor: Zhanna Sadirmekova
University: AstanaIT University

## Project titles

|Language|Title|
|-|-|
|English|Multilingual Phishing Detection System for Kazakh, Russian and English Using Large Language Models|
|Русский|Система обнаружения многоязычного фишинга на казахском, русском и английском языках с использованием больших языковых моделей|
|Қазақша|Үлкен тілдік модельдерді қолдану арқылы қазақ, орыс және ағылшын тілдеріндегі көптілді фишингті анықтау жүйесі|

## Problem statement

Standard spam and phishing filters (blacklists, hand-written rules, classical ML on keywords) struggle with
context-rich, multilingual phishing, especially in Kazakh, a low-resource language, and in mixed
Kazakh–Russian text. Attackers can additionally use LLMs to produce fluent, personalised phishing in any
language. This project builds a system that understands the intent of a message and returns an
explainable risk score.

## Target users

* SOC analysts: fast triage with reasons and URL analysis
* E-mail / IT administrators: REST API integration, key management, local (private) inference
* General users: paste a message, get a plain-language verdict

## Expected outcomes

* A working prototype (API and web UI) that classifies Kazakh, Russian and English messages.
* A labelled multilingual evaluation dataset with documented sources and a datasheet.
* A quantitative comparison of the baseline, the fine-tuned transformer and the LLM-based approach
(targets: F1 above 92% overall, latency under 3 s per message).
* Project documentation, architecture diagrams, tests and a reproducible repository.

## Team and responsibilities

|Member|Role|Responsibilities|
|-|-|-|
|Imanbayev Islam|Sole developer|Analysis, design, dataset preparation, implementation, evaluation, documentation|


## Scope

In scope: text-based phishing detection (KZ / RU / EN), language detection, URL extraction and heuristic
analysis, risk scoring (0–100) with explanations, REST API, minimal web UI, history and feedback, evaluation
against a baseline (Naive Bayes).

Out of scope: image/QR/attachment phishing, vishing, production mail gateway, website crawling,
training an LLM from scratch.

## Technology choices

|Decision|Choice|Alternatives considered|
|-|-|-|
|Detection engine|Two-tier: fine-tuned multilingual DistilBERT (fast) + open-source LLM (Gemma-2 / Llama-3) for uncertain cases and explanations; GPT-4o only as offline benchmark|DistilBERT only · Llama/Gemma only · GPT-4o API|
|Backend|FastAPI|Django, Flask|
|Database|PostgreSQL (SQLite for tests)|MongoDB, SQLite|

Full comparison and justification: [`docs/project-documentation.md`](docs/project-documentation.md).

## Project status

|Item|Status|
|-|-|
|Documentation (proposal to UX materials)|Draft|
|Verification and evaluation plan|Planned|
|Dataset collection|Planned|
|Prototype implementation (`src/`)|Not started|
|Tests (`tests/`)|Not started|

Last updated: October 2026.

## Repository structure

```text
├── docs/        # Project documentation (project-documentation.md)
├── diagrams/    # Editable sources (.drawio) and PNG exports
├── src/         # API, model handling, helper code
├── tests/       # Automated test scripts
├── config/      # Environment configuration templates (.env.example)
└── data/        # Only small synthetic/anonymised samples; no private data is committed
```

## Getting started

```bash
git clone https://github.com/Islam-ITUni/multilingual-phishing-detection-llm.git
cd multilingual-phishing-detection-llm
cp config/.env.example .env      
python -m venv .venv
source .venv/bin/activate        
```

Planned API: `POST /api/v1/analyze`. See the sample request/response in `docs/project-documentation.md` (Section 8).

## Documentation

* Project documentation: [`docs/project-documentation.md`](docs/project-documentation.md)
* Diagrams: [`diagrams/`](diagrams/)
* Task board (YouTrack): https://multilingual-phishing-detection-llm.youtrack.cloud/projects/MPD

## Security

API keys, tokens, `.env` files, model weights and confidential/raw e-mail data must never be committed.
See `.gitignore`. Use `config/.env.example` as a template only.

## Author

Imanbayev Islam. All commits are made from this personal account to document individual contribution.

