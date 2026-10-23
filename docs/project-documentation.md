# PRE-DEFENSE — PROJECT DOCUMENTATION

**Multilingual Phishing Detection System for Kazakh, Russian and English Using Large Language Models**

|Item|Details|
|-|-|
|**Developer**|Imanbayev Islam|
|**Supervisor**|Zhanna Sadirmekova|
|**University / Programme**|AstanaIT University|
|**Repository**|https://github.com/Islam-ITUni/multilingual-phishing-detection-llm.git|
|**Version / date**|v0.1|
|**Release tag**|prob-period-1|

## Table of Contents

* [1. Project Proposal](#1-project-proposal)

  * [1.1 Project titles](#11-project-titles)
  * [1.2 Developer and supervisor](#12-developer-and-supervisor)
  * [1.3 Problem statement](#13-problem-statement)
  * [1.4 Target users](#14-target-users)
  * [1.5 Project aim](#15-project-aim)
  * [1.6 Objectives](#16-objectives)
  * [1.7 Expected outcomes](#17-expected-outcomes)
  * [1.8 Scope boundaries](#18-scope-boundaries)
* [2. Evidence of Relevance](#2-evidence-of-relevance)

  * [2.1 Relevance of the problem](#21-relevance-of-the-problem)
  * [2.2 Kazakh as a low-resource language](#22-kazakh-as-a-low-resource-language)
  * [2.3 Growing sophistication of attacks](#23-growing-sophistication-of-attacks)
* [3. Literature Review](#3-literature-review)

  * [3.1 Review method](#31-review-method)
  * [3.2 From rules to transformers in phishing detection](#32-from-rules-to-transformers-in-phishing-detection)
  * [3.3 Transformer models: BERT, RoBERTa, DistilBERT and multilingual variants](#33-transformer-models-bert-roberta-distilbert-and-multilingual-variants)
  * [3.4 Large language models and zero-shot detection](#34-large-language-models-and-zero-shot-detection)
  * [3.5 NLP challenges in low-resource languages (Kazakh)](#35-nlp-challenges-in-low-resource-languages-kazakh)
  * [3.6 Structured publication analysis](#36-structured-publication-analysis)
  * [3.7 Synthesis and research gap](#37-synthesis-and-research-gap)
* [4. Existing System Comparison](#4-existing-system-comparison)

  * [Summary](#summary)
* [5. Technology Comparison](#5-technology-comparison)

  * [5.1 Decision 1: LLM inference engine](#51-decision-1-llm-inference-engine)
  * [5.2 Decision 2: Backend framework](#52-decision-2-backend-framework)
  * [5.3 Decision 3: Database](#53-decision-3-database)
* [6. Requirements Specification](#6-requirements-specification)

  * [6.1 Functional requirements](#61-functional-requirements)
  * [6.2 Non-functional requirements](#62-non-functional-requirements)
* [7. Architecture and Diagrams](#7-architecture-and-diagrams)

  * [7.1 Architectural description](#71-architectural-description)
  * [7.2 System Context Diagram](#72-system-context-diagram)
  * [7.3 Use Case Diagram](#73-use-case-diagram)
  * [7.4 Component Diagram (Draft)](#74-component-diagram-draft)
  * [7.5 Request flow](#75-request-flow)
  * [7.6 Preliminary data model](#76-preliminary-data-model)
  * [7.7 Architecture deliverable files](#77-architecture-deliverable-files)
* [8. UX / Prototype Materials](#8-ux--prototype-materials)

  * [8.1 Key user scenarios](#81-key-user-scenarios)
  * [8.2 Wireframes](#82-wireframes)
  * [8.3 API contract: sample request and response](#83-api-contract-sample-request-and-response)
* [References](#references)

## 1\. Project Proposal

### 1.1 Project titles

|Language|Title|
|-|-|
|**English**|Multilingual Phishing Detection System for Kazakh, Russian and English Using Large Language Models|
|**Russian**|Система обнаружения многоязычного фишинга на казахском, русском и английском языках с использованием больших языковых моделей|
|**Kazakh**|Үлкен тілдік модельдерді қолдану арқылы қазақ, орыс және ағылшын тілдеріндегі көптілді фишингті анықтау жүйесі.|

### 1.2 Developer and supervisor

|Role|Name|
|-|-|
|**Developer (sole)**|Imanbayev Islam|
|**Supervisor**|Zhanna Sadirmekova|

### 1.3 Problem statement

Phishing remains one of the most common initial-access techniques in cyber-attacks, and the Anti-Phishing Working Group continues to document large and persistent volumes of phishing campaigns worldwide \[26]. Conventional e-mail and SMS filters rely on blacklists, hand-written rules, or classical machine-learning models trained on keyword statistics. These approaches work best for the languages and campaigns they were built and tuned for, which are predominantly English.

Kazakhstan is a bilingual society in which Kazakh and Russian are used side by side, and English is common in business and IT. Phishing messages in this environment are frequently written in Kazakh, in Russian, or in a mixture of both (code-switching), often impersonating local banks, payment services, government portals and delivery companies. Kazakh is a low-resource language in NLP: it has far fewer labelled datasets and dedicated models than English or Russian \[14, 15, 16, 17]. As a result, rule- and keyword-based filters have limited coverage of Kazakh vocabulary, morphology and phrasing, and attackers can further evade them with transliteration, look-alike characters and polite, context-rich wording.

In addition, large language models make it cheap for attackers to produce fluent, personalised phishing text in any language \[8, 10]. The same class of models, however, can understand context and intent rather than only surface keywords, and has shown promising zero-shot phishing detection ability \[9, 8]. The problem addressed by this project is the inability of standard spam filters to reliably catch context-rich, multilingual phishing messages written in Kazakh, Russian and English.

### 1.4 Target users

|User group|Needs|How they use the system|
|-|-|-|
|SOC analysts|Fast triage of suspicious messages, explanation of why a message is risky, history for investigations|Web UI and API; reviews risk score, reasons and extracted URLs; marks false positives|
|E-mail / IT administrators|Integration with existing mail infrastructure, control over data, monitoring and API keys|REST API integration (webhook or plugin), key management, metrics|
|General users|Simple yes/no style guidance in their own language, no technical jargon|Paste a message in the web UI and read a plain-language verdict|

### 1.5 Project aim

To design, implement and evaluate a web-based and API-accessible system that detects phishing messages written in Kazakh, Russian and English using large language models and transformer-based classifiers, outputs an explainable risk score, and measurably outperforms a conventional baseline classifier (Naive Bayes / TF-IDF) on a multilingual test set.

### 1.6 Objectives

**O1.** Review the literature on transformer models, LLM-based phishing detection and low-resource NLP, and compare existing systems and technologies (documentation phase).

**O2.** Collect, clean and label a multilingual (KZ/RU/EN) dataset of phishing and legitimate messages from public corpora, synthetic generation and consented samples, with documented provenance.

**O3.** Implement a preprocessing pipeline (normalisation, language detection, URL extraction, handling of transliteration and homoglyphs).

**O4.** Implement and compare three detection approaches: a Naive Bayes baseline, a fine-tuned multilingual DistilBERT classifier, and prompt-based zero/few-shot detection with an open-source LLM (Gemma-2 / Llama-3); use GPT-4o only as an offline upper-bound reference.

**O5.** Build a FastAPI backend that returns a risk score (0–100), a label and human-readable reasons, with API-key authentication and persistent history in PostgreSQL.

**O6.** Build a minimal web interface for the key user scenarios.

**O7.** Evaluate the system with Precision, Recall, F1 and False Positive Rate per language, and report latency; document results and limitations.

### 1.7 Expected outcomes

* A working prototype (API + web UI) that classifies Kazakh, Russian and English messages.
* A labelled multilingual evaluation dataset with documented sources and a datasheet.
* Quantitative comparison of baseline, fine-tuned transformer and LLM-based approaches (target: F1 above 92% overall; latency under 3 s per message).
* Project documentation, architecture diagrams, tests and a reproducible repository.

### 1.8 Scope boundaries

|In scope|Out of scope|
|-|-|
|Text-based detection of phishing in e-mail bodies/subjects and SMS-like messages in KZ, RU, EN|Image-, QR-code- and attachment-based phishing; voice phishing (vishing)|
|URL extraction and heuristic/lexical URL analysis; optional lookup in public blacklists|Full website crawling, rendering or screenshot analysis|
|REST API, minimal web UI, history and feedback storage|Production-grade mail gateway, SMTP/MTA deployment, enterprise SSO|
|Evaluation on a curated test set; comparison with a baseline|Real-time training on live customer mail; large-scale model pre-training|
|Prompt-based and fine-tuned (LoRA/DistilBERT) approaches|Training a Kazakh LLM from scratch|

## 2\. Evidence of Relevance

### 2.1 Relevance of the problem

Phishing remains a persistent and large-scale threat. The Anti-Phishing Working Group regularly reports high volumes of phishing campaigns worldwide \[26]. Email and messaging filters based on blacklists, hand-written rules or keyword statistics detect known patterns well, but they depend on the language and campaigns they were designed for \[7], \[21]. This makes the problem especially relevant for Kazakhstan, where Kazakh and Russian are used side by side and English is common in business and IT. Phishing messages there can appear in any of these languages or in a mix of them.

### 2.2 Kazakh as a low-resource language

Research shows that the world’s languages are very unevenly supported in NLP \[14], and that low-resource languages need dedicated techniques such as transfer learning and data augmentation \[15]. Kazakh is such a language. Dedicated datasets are still being created \[16], and a recent benchmark reports that even strong multilingual models, including Llama 3.1 and GPT-4, leave substantial room for improvement in Kazakh and Russian \[17]. Detection tools built mainly around English-language data are therefore likely to cover Kazakh and mixed Kazakh–Russian messages less well. This is a reasoned expectation from the literature, and the project tests it experimentally (see 2.4).

### 2.3 Growing sophistication of attacks

Large language models make it easy to write fluent, personalised phishing text in many languages. Studies show that LLM-generated phishing can be highly convincing \[8] and that popular chatbots can be misused to create phishing at scale \[10]. Messages like this lack the spelling errors and awkward phrasing that simple filters and users often rely on. At the same time, LLMs can understand context and intent, and early work shows promising LLM-based phishing detection with explanations \[8], \[9]. A system that detects phishing by meaning rather than keywords, and that covers Kazakh, Russian and English, therefore addresses a real gap.

## 3\. Literature Review

### 3.1 Review method

Sources were searched in IEEE Xplore, ACM Digital Library, ACL Anthology, arXiv and Google Scholar using combinations of the keywords: phishing detection, e-mail, transformer, BERT, RoBERTa, large language model, zero-shot, multilingual, low-resource, Kazakh, Russian. Inclusion criteria: peer-reviewed or widely cited preprints; direct relevance to phishing/spam text detection, multilingual transformers, LLM prompting, or low-resource NLP; preference for publications from 2021–2026. The reference list contains 25 scientific publications (of which 13 were published in 2021 or later) and 5 technical/web sources; the requirement is at least 12 used sources including 8 scientific ones, with the majority from the last five years.

### 3.2 From rules to transformers in phishing detection

Early anti-phishing filters used blacklists and hand-written rules; later work applied classical machine-learning (Naive Bayes, SVM, Random Forest \[24, 25]) over bag-of-words/TF-IDF and URL features \[21]. A systematic review of NLP-based phishing e-mail detection \[7] shows that the field moved from handcrafted features towards deep learning and, more recently, transformer-based representations. Classical models are fast and easy to deploy but see only surface features, and they must be retrained for each language and campaign style.

### 3.3 Transformer models: BERT, RoBERTa, DistilBERT and multilingual variants

The Transformer architecture \[22] underpins BERT \[1], which learns bidirectional context through masked-language-model pre-training and is fine-tuned for classification. RoBERTa \[2] showed that BERT was under-trained and improved results with a better pre-training recipe. DistilBERT \[3] compresses BERT by knowledge distillation, retaining most of its language-understanding performance while being substantially smaller and faster — attractive for the project’s latency target. Multilingual BERT transfers across languages \[5] and XLM-R was trained on 100 languages including Kazakh and Russian \[4], while monolingual Russian models such as RuBERT exist \[6]. The Hugging Face Transformers library provides all these models through a common API \[23]. Note that English-only DistilBERT checkpoints cannot be used for Kazakh; a multilingual checkpoint is required.

### 3.4 Large language models and zero-shot detection

Large language models can solve new tasks from instructions alone (zero-shot) or a few examples, and reasoning-style prompting can improve results \[11, 12]. For phishing, Heiding et al. \[8] compare LLM-generated and human-designed phishing and also evaluate LLMs as detectors; Koide et al. \[9] propose ChatSpamDetector, which uses an LLM to classify phishing e-mails and to explain its decision; Roy et al. \[10] show that popular chatbots can be misused to create convincing phishing and discuss detection countermeasures. Open-weight models such as Llama 3 \[18] and Gemma 2 \[19] make self-hosted, privacy-preserving inference possible, while commercial models such as GPT-4o \[20] serve as strong but external reference points. Parameter-efficient fine-tuning such as LoRA \[13] allows adapting an open model to the task with limited hardware.

### 3.5 NLP challenges in low-resource languages (Kazakh)

Joshi et al. \[14] show a very unequal distribution of NLP resources across the world’s languages, and Hedderich et al. \[15] survey techniques for low-resource settings (transfer learning, data augmentation, weak supervision). For Kazakh specifically, KazNERD \[16] contributed a named-entity dataset, and KazMMLU \[17] reports that even strong multilingual models (including Llama 3.1 and GPT-4) leave substantial room for improvement in Kazakh and Russian. Consequences for this project: (1) zero-shot LLM performance in Kazakh cannot be assumed and must be measured; (2) a Kazakh evaluation set must be built or collected; (3) cross-lingual transfer and data augmentation (e.g. translation of English phishing samples, template generation) are likely needed; (4) agglutinative morphology, Cyrillic/Latin transliteration and Kazakh–Russian code-switching must be handled in preprocessing.

### 3.6 Structured publication analysis

The analysis below records, for each source, the method and the finding that matters for this project.

|#|Source|Method / model|Data / domain|Key finding|Relevance to project|
|-|-|-|-|-|-|
|1|Devlin et al., 2019 \[1]|BERT architecture utilizing masked language model (MLM) pre-training followed by task-specific fine-tuning.|General English NLP datasets.|Deep bidirectional pre-training provides superior contextual representations for downstream text classification tasks.|Establishes the core transformer encoder foundation for the project's baseline classifier.|
|2|Liu et al., 2019 \[2]|RoBERTa, optimizing BERT using dynamic masking and larger batch sizes.|General English NLP corpora.|Removing the Next Sentence Prediction task and extending pre-training runtime significantly improves classification accuracy.|Serves as a primary candidate encoder for the classification module.|
|3|Sanh et al., 2019 \[3]|DistilBERT using knowledge distillation techniques.|General English NLP datasets.|Retains 97% of BERT's language understanding capability while reducing model size by 40% and increasing processing speed by 60%.|Informs the selection of the fast first-stage classifier needed to meet the sub-3-second latency requirement.|
|4|Conneau et al., 2020 \[4]|XLM-RoBERTa cross-lingual masked language modeling.|Multilingual corpus spanning 100 languages, including Kazakh (KZ) and Russian (RU).|Massive multilingual pre-training enables effective cross-lingual transfer learning to low-resource languages.|Justifies the selection of multilingual transformer checkpoints for handling Kazakh and Russian text.|
|5|Pires et al., 2019 \[5]|Empirical analysis of Multilingual BERT (mBERT).|Cross-lingual evaluation benchmarks.|mBERT enables zero-shot cross-lingual transfer between languages that share structural or vocabulary characteristics, though performance drops on low-resource scripts.|Confirms the feasibility and performance boundaries of cross-lingual transfer for Kazakh.|
|6|Kuratov \& Arkhipov, 2019 \[6]|RuBERT vocabulary and weight adaptation.|Russian language text corpora.|Regionally adapted BERT models consistently outperform generic multilingual encoders on localized language tasks.|Provides direct reference for optimizing the Russian language component of the bilingual dataset.|
|7|Salloum et al., 2022 \[7]|Systematic literature review of NLP techniques in cybersecurity.|Phishing email detection literature and datasets.|Maps the industry transition from handcrafted feature extraction to deep learning and transformer-based representations.|Provides domain overview and identifies benchmark feature extraction approaches.|
|8|Sahingoz et al., 2019 \[21]|Random Forest classifiers trained on NLP and lexical URL features.|Standard URL phishing datasets.|Combining lexical URL features with tree ensembles achieves detection accuracy exceeding 97%.|Guides the feature extraction logic and heuristic rules for the URL Analyzer component.|
|9|Heiding et al., 2023 \[8]|Comparative evaluation of LLM prompting (GPT-4, Claude, LLaMA) versus human models.|English phishing and spear-phishing emails.|LLMs produce highly persuasive spear-phishing text while simultaneously demonstrating high accuracy in intent detection.|Motivates the adoption of LLMs for context-aware intent detection and risk reasoning.|
|10|Koide et al., 2024 \[9]|ChatSpamDetector framework utilizing GPT-4 prompt engineering.|Phishing email corpus (.eml format).|LLMs classify phishing messages with 99.7% accuracy and generate clear, natural-language threat explanations in JSON format.|Serves as the primary architectural precedent for producing JSON-formatted risk scores and explanations.|
|11|Roy et al., 2023 \[10]|ScamLLM prompt evaluation and adversarial testing.|English phishing templates and chatbot prompt datasets.|Chatbots can be manipulated to generate highly evasive phishing attacks, necessitating semantic detection countermeasures.|Defines the threat landscape regarding automated, LLM-generated phishing campaigns.|
|12|Kojima et al., 2022 \[11]|Zero-shot Chain-of-Thought (CoT) prompting.|General reasoning benchmarks.|Appending simple prompt instructions like "Let's think step by step" unlocks multi-step reasoning in zero-shot LLM tasks.|Informs zero-shot prompt design to guide the LLM when breaking down suspicious message elements.|
|13|Wei et al., 2022 \[12]|Few-shot Chain-of-Thought (CoT) prompting.|Multi-factor complex reasoning tasks.|Explicit reasoning steps significantly boost classification accuracy on complex tasks requiring contextual assessment.|Applied in prompt engineering to generate 1–5 structured risk factors per analysis.|
|14|Hu et al., 2022 \[13]|Low-Rank Adaptation (LoRA) for parameter-efficient fine-tuning.|General LLM task adaptation.|Freezes pre-trained model weights and injects trainable rank decomposition matrices, reducing memory footprint by 3x.|Offers a lightweight fine-tuning path for adapting self-hosted open-weight LLMs.|
|15|Joshi et al., 2020 \[14]|Empirical survey of global linguistic resources in NLP.|Global NLP dataset availability metrics.|Identifies a severe disparity in resource allocation across languages, categorizing Kazakh in lower-resource tiers.|Establishes the theoretical justification for classifying Kazakh as a low-resource language in cybersecurity NLP.|
|16|Hedderich et al., 2021 \[15]|Systematic survey of low-resource NLP methodologies.|Low-resource language processing benchmarks.|Cross-lingual transfer, synthetic data augmentation, and weak supervision are required to overcome data scarcity.|Directs the project's data augmentation strategy (back-translation and synthetic template generation) for Kazakh.|
|17|Yeshpanov et al., 2022 \[16]|KazNERD dataset curation and baseline benchmarks.|Kazakh language text corpus.|Establishes a named entity recognition resource for Kazakh while highlighting the ongoing shortage of domain-specific datasets.|Highlights baseline dataset availability and preprocessing rules for Kazakh text.|
|18|Togmanov et al., 2025 \[17]|KazMMLU benchmark evaluation.|Kazakh and Russian educational, regional, and domain-specific knowledge datasets.|Demonstrates that leading LLMs (including Llama 3.1 and GPT-4) exhibit noticeable accuracy drops on Kazakh language tasks.|Identifies performance risks in zero-shot Kazakh LLM detection, validating the need for fine-tuning and local evaluation.|
|19|Llama Team, 2024 \[18]|Llama 3 open-weight model family (8B/70B parameter models).|Multilingual training corpus.|Delivers instruction-following and multi-step reasoning capabilities at accessible deployment scales.|Primary open-weight candidate for self-hosted second-tier LLM inference.|
|20|Gemma Team, 2024 \[19]|Gemma 2 open-weight model family (2B/9B/27B parameter models).|Multilingual training corpus.|Offers highly efficient inference throughput alongside strong multilingual classification performance.|Secondary candidate for low-latency local LLM evaluation.|
|21|OpenAI, 2024 \[20]|GPT-4o system architecture and capability evaluation.|Multilingual and multimodal benchmarks.|Achieves state-of-the-art zero-shot cross-lingual understanding and contextual threat assessment.|Serves as the offline upper-bound reference model for comparative evaluation.|

### 3.7 Synthesis and research gap

The literature shows that: (a) transformer encoders and LLMs are effective for text classification; (b) LLMs can both generate and detect phishing with explanations; and (c) Kazakh remains a low-resource language where multilingual models underperform. This project addresses the gap by evaluating LLM-based phishing detection jointly on Kazakh, Russian and English with an explainable risk score.

## 4\. Existing System Comparison

Four systems are compared across eight criteria. Ratings are a **preliminary qualitative assessment** based on the literature and public documentation; the entries for the proposed system are targets that the verification plan must confirm experimentally. Commercial-product cells should be re-checked against vendor documentation \[28] before the defence.

|Criterion|S1: Rule-based (SpamAssassin)|S2: Classic ML (RF + TF-IDF)|S3: Commercial gateway (Proofpoint)|S4: Proposed LLM system|
|-|-|-|-|-|
|**C1 Kazakh Language Support (KZ)**|Low capability. Depends entirely on manually written regex patterns and static keyword lists, which lack coverage for Kazakh vocabulary and grammar.|Low-to-medium capability. Effective only if trained directly on labelled Kazakh text; fails to handle complex Kazakh morphological variations.|Low capability. Proprietary engines are optimized for high-resource languages, with undocumented or limited support for Kazakh regional threats.|Medium (Target). Designed specifically to process Kazakh text using fine-tuned multilingual encoders and context-aware LLM prompts.|
|**C2 Russian and English Language Support**|Medium-to-high capability, performing best on English due to extensive community-maintained rule sets.|Medium-to-high capability, provided separate training pipelines are maintained for each language.|High capability, utilizing mature multi-language threat intelligence engines.|High (Target), utilizing pre-trained multilingual representations covering English, Russian, and Kazakh natively.|
|**C3 Context and Intent Understanding**|Very low. Inspects surface-level text patterns without analyzing semantic context or intent.|Low. Relies on bag-of-words statistics, ignoring sentence structure, tone, and subtle social engineering tactics.|Medium-to-high. Combines statistical machine learning with domain reputation and behavioral signals.|High. Evaluates the full semantic context, identifying urgency tactics, impersonation, and implicit threats.|
|**C4 Adaptation to New Campaigns**|Slow. Requires manual creation and deployment of new rule definitions for every new threat template.|Slow. Demands dataset re-labeling and complete model retraining to recognize novel phishing patterns.|Fast. Leverages automated, vendor-managed global threat intelligence feeds.|Medium-to-fast. Adapts rapidly through system prompt updates, few-shot examples, and parameter-efficient LoRA adjustments.|
|**C5 Explainability**|High. Outputs an explicit list of triggered rule names and assigned points.|Low-to-medium. Offers limited visibility restricted to feature importance weights and word scores.|Low-to-medium. Provides opaque risk scores dependent on proprietary vendor logs.|High (Target). Generates structured, natural-language explanations highlighting specific threat indicators in the input language.|
|**C6 Latency and Throughput**|Very high throughput with sub-millisecond execution times.|Very high throughput with lightweight inference overhead.|High throughput managed via scalable cloud gateway infrastructure.|Medium throughput. Uses a two-tier architecture to balance deep LLM reasoning while maintaining response times under the 3-second requirement.|
|**C7 Privacy and On-Premises Control**|High. Executes entirely within the local infrastructure without external data exposure.|High. Operates completely on-premises on local hardware.|Low to medium. Requires routing message traffic through proprietary vendor cloud servers.|High. Employs local open-source models for primary operations, reserving third-party cloud APIs strictly for offline benchmarks.|
|**C8 Cost and Maintenance**|Low software licensing costs, but high ongoing labor costs for rule maintenance.|Low infrastructure costs, but moderate effort required for continuous data collection and retraining.|High recurring enterprise licensing fees.|Moderate local hardware/GPU hosting costs with minimal manual rule maintenance.|

### Summary

Rule-based and classical ML systems are fast and private but have weak semantic understanding and need manual work per language. Commercial gateways have broad threat intelligence but are costly, opaque and their Kazakh coverage is not documented. The proposed system trades some latency for contextual understanding and explainability, keeps data local, and targets Kazakh/Russian/English explicitly.

## 5\. Technology Comparison

Three architectural decisions are evaluated, each with three alternatives. For decision 1 a weighted decision matrix is used (scores 1–5, 5 = best). The scores are the developer’s preliminary judgement from the literature and documentation and will be revisited after the first benchmarks.

### 5.1 Decision 1: LLM inference engine

|Criterion|Weight %|A: Fine-tuned DistilBERT (multilingual) \[3]|B: Llama-3 / Gemma-2 (open) \[18, 19]|C: GPT-4o API \[20]|
|-|-|-|-|-|
|**Multilingual quality (KZ/RU/EN)**|25|3|3|4|
|**Latency (< 3 s target)**|15|5|3|3|
|**Privacy / data control**|20|5|5|1|
|**Cost**|15|5|4|2|
|**Development effort**|10|3|3|5|
|**Explainability of output**|15|2|4|4|
|**Weighted total (max 5.0)**|100|3.85|3.70|3.05|

**Reading the result.** A (3.85) and B (3.70) are close and C (3.05) is clearly weaker mainly because of privacy and cost: sending message content to a third-party API conflicts with the privacy needs of administrators and many Kazakhstani organisations. A is fast and cheap but needs labelled Kazakh training data and cannot explain its verdicts; B understands context and gives reasons but is slower and its Kazakh ability must be measured \[17].

**Decision:** a two-tier design. A fine-tuned multilingual DistilBERT classifier is the fast first stage and a comparison model; an open-source LLM (Gemma-2 or Llama-3, self-hosted) handles uncertain cases and generates explanations. GPT-4o is used only offline, on non-sensitive or synthetic data, as an upper-bound benchmark. If the second tier proves too complex for a sole developer, the fallback is B alone for the MVP, with A as the evaluated baseline.

### 5.2 Decision 2: Backend framework

|Criterion|Django|Flask|FastAPI \[29]|
|-|-|-|-|
|**Async / concurrency**|Supported, but ecosystem is mainly synchronous|Mainly synchronous; async is limited|Native async (ASGI); suits waiting on model inference|
|**Automatic API docs**|Needs extra packages (DRF, drf-spectacular)|Needs extensions|Built-in OpenAPI/Swagger UI — helps demo and UX materials|
|**Request validation**|Serializers (DRF)|Manual or extensions|Pydantic type-based validation built in|
|**ML ecosystem fit**|Good (Python)|Good (Python)|Good (Python); common for model-serving APIs|
|**Built-in admin / auth / ORM**|Strong (batteries included)|Minimal|Minimal; add SQLAlchemy and API-key dependency|
|**Learning curve for the project**|Higher (large framework)|Low|Low–medium|

**Decision: FastAPI** — the API is the core product; automatic OpenAPI documentation, Pydantic validation and async support fit a model-serving service. Django’s admin and ORM are not needed for the MVP; Flask would require more manual work for validation and documentation.

### 5.3 Decision 3: Database

|Criterion|MongoDB|SQLite|PostgreSQL \[30]|
|-|-|-|-|
|**Data model fit**|Flexible documents; good for variable LLM output|Relational, simple|Relational + JSONB for variable LLM output|
|**Integrity and relations (users, keys, analyses, feedback)**|Weaker; references managed in app|Supported|Strong (constraints, foreign keys, transactions)|
|**Concurrency / multi-user**|Good|Limited write concurrency|Good|
|**Setup effort**|Separate server|None (file)|Separate server (Docker makes this easy)|
|**Scalability / production readiness**|High|Low|High|
|**Fit for this project**|Acceptable|Good for local tests only|Best overall|

**Decision: PostgreSQL** for the application (relational integrity plus JSONB for model outputs); SQLite may be used in automated tests for speed. MongoDB was not chosen because the data are mostly relational and the extra flexibility is not needed.

## 6\. Requirements Specification

Priorities follow MoSCoW (Must / Should / Could). Each requirement has a testable acceptance criterion. Numeric targets come from the project brief; those marked (proposed) are suggestions to confirm with your supervisor.

### 6.1 Functional requirements

|ID|Requirement|Priority|Acceptance criteria|
|-|-|-|-|
|**FR-1**|Accept message text (subject + body, up to 5,000 characters) via REST API and web form|Must|POST /api/v1/analyze with valid JSON returns HTTP 200 and a result object; empty or oversized input returns HTTP 422/413 with an error message|
|**FR-2**|Detect input language (Kazakh, Russian, English, mixed/other) and handle multilingual text|Must|On a labelled test set of at least 150 messages, language detection accuracy is ≥ 95% (proposed); detected language is returned in the response|
|**FR-3**|Normalise text (HTML stripping, Unicode normalisation, homoglyph and transliteration handling)|Must|Unit tests cover ≥ 10 normalisation cases incl. Kazakh-specific letters (ә, ғ, қ, ң, ө, ұ, ү, һ, і) and look-alike Latin/Cyrillic characters|
|**FR-4**|Extract and analyse URLs (lexical/heuristic checks: look-alike domain, IP host, excessive subdomains, shorteners; optional blacklist lookup)|Must|All URLs in a message are returned with a verdict and reason; ≥ 90% of URLs in a 50-URL test list are extracted correctly (proposed)|
|**FR-5**|Classify message as phishing / legitimate using the detection pipeline|Must|Returns label and confidence for every valid request; meets NFR-2 on the held-out test set|
|**FR-6**|Compute a risk score 0–100 and risk level (Low / Medium / High)|Must|Score is an integer in \[0, 100]; level thresholds are documented and tested; score increases monotonically with phishing probability|
|**FR-7**|Provide human-readable reasons (explanation) in the language of the input|Should|Response contains 1–5 reasons; for 20 manually reviewed phishing samples, at least 80% of reasons are judged relevant by the developer and supervisor (proposed)|
|**FR-8**|Store analysis history (with retention setting) and show it in the UI|Should|A user with a valid key can list their last N analyses; deleting an entry removes it from the database|
|**FR-9**|Allow feedback on a result (false positive / false negative)|Should|POST /api/v1/feedback stores the feedback linked to the analysis ID|
|**FR-10**|API-key authentication and per-key rate limiting|Must|Request without a valid key returns 401; exceeding the limit returns 429|
|**FR-11**|Web UI for the analyse and result screens (see Section 8)|Should|A user can paste text, press Analyze and see score, reasons and URLs without using the API directly|
|**FR-12**|Batch analysis endpoint (up to 20 messages per call)|Could|Returns one result per message in input order|
|**FR-13**|Audit logging of requests (without storing secrets)|Could|Log entry with timestamp, key ID, language and verdict for each request|

### 6.2 Non-functional requirements

|ID|Requirement|Priority|Acceptance criteria|
|-|-|-|-|
|**NFR-1**|Performance: response latency|Must|95th-percentile end-to-end latency < 3 s for messages ≤ 2,000 characters on the documented reference hardware, measured over ≥ 200 requests|
|**NFR-2**|Detection quality|Must|F1-score for the phishing class > 92% on the held-out multilingual test set; per-language F1 reported for KZ, RU, EN. Per-language minimum (proposed): 85%. Targets must be re-validated once the dataset exists|
|**NFR-3**|False positives|Should|False Positive Rate ≤ 5% on legitimate messages in the test set (proposed)|
|**NFR-4**|API security|Must|API keys stored hashed; TLS in any non-local deployment; input validation via schemas; rate limiting; no secrets in the repository (checked by .gitignore and secret scan)|
|**NFR-5**|Privacy|Must|Default pipeline runs on local models; message text is not sent to third-party services unless explicitly enabled in configuration; retention period configurable|
|**NFR-6**|Usability|Should|A new user completes the analyse scenario in ≤ 3 clicks without instructions; UI available in EN/RU/KZ labels (proposed)|
|**NFR-7**|Maintainability and testing|Should|Automated tests run with a single command; unit-test coverage of core modules ≥ 70% (proposed)|
|**NFR-8**|Reproducibility|Should|README instructions reproduce training/evaluation with fixed random seeds and a documented dataset version|

## 7\. Architecture and Diagrams

### 7.1 Architectural description

The system is a layered, service-style application. Clients (web UI, mail server plug-ins, scripts) call a FastAPI backend over HTTPS/JSON. The API layer authenticates the caller (API key), validates the request and passes the text through a **preprocessing** stage (normalisation, language detection). A **URL analyzer** extracts and scores URLs. A **fast classifier** (fine-tuned multilingual DistilBERT) produces an initial verdict; low-confidence cases are escalated to an **LLM adapter** that prompts a locally hosted open-source model (Gemma-2 / Llama-3) for a verdict and reasons. A **risk scorer** merges model and URL signals into a score 0–100 and an explanation. A repository layer stores results and feedback in PostgreSQL. Model names, thresholds and secrets are provided through configuration (.env), never hard-coded.

The diagrams are drafts and will evolve as the implementation progresses. Editable sources are stored as .drawio files (open them with diagrams.net) with PNG exports in the diagrams/ folder.

### 7.2 System Context Diagram

!\[Figure 1. System context diagram](../diagrams/01\_system\_context.png)

*Figure 1. System context — diagrams/01\_system\_context.drawio*

### 7.3 Use Case Diagram

!\[Figure 2. Use case diagram](../diagrams/02\_use\_case.png)

*Figure 2. Use cases — diagrams/02\_use\_case.drawio*

|Use case|Primary actor|Summary|
|-|-|-|
|**UC1 Submit text for analysis**|User, SOC analyst|Paste or send a message; system returns the result (includes language detection UC4)|
|**UC2 View risk score \& explanation**|User, SOC analyst|See score, level, reasons and URL verdicts|
|**UC3 Analyze URLs in message**|SOC analyst|Optional detail view that extends UC1|
|**UC5 Review analysis history**|SOC analyst|List and filter earlier analyses|
|**UC6 Mark false positive / negative**|SOC analyst|Feedback stored for later model evaluation|
|**UC7 Batch scan via API**|Mail server|Automated submission of messages|
|**UC8 Manage API keys**|Administrator|Create, revoke and rate-limit keys|
|**UC9 Monitor metrics \& health**|Administrator|View counts, latency and health status|

### 7.4 Component Diagram (Draft)

!\[Figure 3. Component diagram (draft)](../diagrams/03\_component\_draft.png)

*Figure 3. Component diagram (draft) — diagrams/03\_component\_draft.drawio*

### 7.5 Request flow

1. Client sends POST /api/v1/analyze with text and API key.
2. Auth \& rate limiting verify the key; the request body is validated.
3. Preprocessor normalises text; language detector labels it as kz / ru / en / mixed.
4. URL analyzer extracts URLs and computes lexical/heuristic signals.
5. Fast classifier returns phishing probability; if confidence is low, the LLM adapter is called with a language-aware prompt.
6. Risk scorer combines signals into a score, level and reasons.
7. Result is stored (according to retention settings) and returned as JSON.

### 7.6 Preliminary data model

|Table|Main fields|
|-|-|
|**api\_keys**|id, key\_hash, owner, created\_at, revoked\_at, rate\_limit|
|**analyses**|id, api\_key\_id, created\_at, language, text\_hash (and optional text), label, risk\_score, risk\_level, model\_version, latency\_ms, reasons (JSONB)|
|**urls**|id, analysis\_id, url, verdict, reason|
|**feedback**|id, analysis\_id, feedback\_type (FP/FN/confirm), comment, created\_at|

### 7.7 Architecture deliverable files

|Diagram|Editable source|Exported image|
|-|-|-|
|**System Context**|diagrams/01\_system\_context.drawio|diagrams/01\_system\_context.png|
|**Use Case**|diagrams/02\_use\_case.drawio|diagrams/02\_use\_case.png|
|**Component (draft)**|diagrams/03\_component\_draft.drawio|diagrams/03\_component\_draft.png|

## 8\. UX / Prototype Materials

### 8.1 Key user scenarios

|Scenario|Actor|Steps|Outcome|
|-|-|-|-|
|**S1 Check a suspicious message**|General user|Open web UI → paste text → Analyze → read verdict|Plain-language verdict with score and reasons in the message language|
|**S2 Triage and give feedback**|SOC analyst|Submit message → inspect URLs and reasons → mark as false positive or confirm|Decision recorded; feedback stored for evaluation|
|**S3 Integrate with a mail server**|Administrator|Create API key → configure webhook → send test message|JSON risk output received automatically|

### 8.2 Wireframes

Low-fidelity mockups of the two main screens (editable later in Figma or draw.io). The sample message is a synthetic Kazakh example.

!\[Figure 4. Wireframe 1, Analyze message screen](../diagrams/wireframe\_1\_analyze.png)

*Figure 4. Wireframe 1 — Analyze message screen*

!\[Figure 5. Wireframe 2, Analysis result screen](../diagrams/wireframe\_2\_result.png)

*Figure 5. Wireframe 2 — Analysis result screen*

### 8.3 API contract: sample request and response

All examples use synthetic data and a reserved example domain. Endpoint: **POST /api/v1/analyze**, header **X-API-Key: <your key>**.

**Request (Kazakh example)**

```json
{
  "text": "Құрметті клиент, сіздің банк шотыңыз уақытша бұғатталды.
           Растау үшін 24 сағат ішінде сілтемені басыңыз:
           http://bank-verify.example/login",
  "subject": "Шотыңыз бұғатталды!",
  "language\\\_hint": "auto",
  "options": { "explain": true, "analyze\\\_urls": true }
}
```

**Response 200 (illustrative values)**

```json
{
  "analysis\\\_id": "a7c1f3e2-0b9d-4c1e-9d1a-2f6c7b8e4d10",
  "label": "phishing",
  "risk\\\_score": 94,
  "risk\\\_level": "high",
  "confidence": 0.97,
  "language": { "detected": "kz", "confidence": 0.99 },
  "reasons": \\\[
    "Urgency: account described as temporarily blocked, 24-hour deadline",
    "Impersonates a bank but contains a look-alike link",
    "Requests verification through an external link"
  ],
  "urls": \\\[
    { "url": "http://bank-verify.example/login", "verdict": "suspicious",
      "reason": "look-alike domain, no HTTPS" }
  ],
  "model": { "stage": "llm", "name": "gemma-2", "version": "dev-0.1" },
  "latency\\\_ms": 1420
}
```

**Request and response (English, legitimate message)**

```jsonc
// request
{ "text": "Hi team, the meeting notes are attached. See you on Monday.",
  "options": { "explain": true } }

// response 200
{ "analysis\\\_id": "5d3e9a10-6a24-4f0b-8f6e-1c2b3a4d5e6f",
  "label": "legitimate", "risk\\\_score": 6, "risk\\\_level": "low",
  "confidence": 0.95, "language": { "detected": "en", "confidence": 0.99 },
  "reasons": \\\[], "urls": \\\[], "latency\\\_ms": 310 }
```

**Error response (HTTP 401)**

```json
{ "error": { "code": "unauthorized", "message": "Missing or invalid API key" } }
```

**Endpoint overview**

|Method \& path|Purpose|Auth|
|-|-|-|
|**POST /api/v1/analyze**|Analyse one message|API key|
|**POST /api/v1/analyze/batch**|Analyse up to 20 messages (Could)|API key|
|**GET /api/v1/history**|List previous analyses|API key|
|**POST /api/v1/feedback**|Report false positive / negative|API key|
|**GET /health**|Service health|None|

## References

IEEE-style numeric references, grouped by topic. Entries 1–25 are scientific publications; 26–30 are technical/web sources.

\[1] J. Devlin, M.-W. Chang, K. Lee, and K. Toutanova, “BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding,” in Proc. NAACL-HLT, 2019. arXiv:1810.04805.

\[2] Y. Liu et al., “RoBERTa: A Robustly Optimized BERT Pretraining Approach,” arXiv:1907.11692, 2019.

\[3] V. Sanh, L. Debut, J. Chaumond, and T. Wolf, “DistilBERT, a distilled version of BERT: smaller, faster, cheaper and lighter,” arXiv:1910.01108, 2019.

\[4] A. Conneau et al., “Unsupervised Cross-lingual Representation Learning at Scale,” in Proc. ACL, 2020. arXiv:1911.02116.

\[5] T. Pires, E. Schlinger, and D. Garrette, “How multilingual is Multilingual BERT?,” in Proc. ACL, 2019. arXiv:1906.01502.

\[6] Y. Kuratov and M. Arkhipov, “Adaptation of Deep Bidirectional Multilingual Transformers for Russian Language,” arXiv:1905.07213, 2019.

\[7] S. Salloum, T. Gaber, S. Vadera, and K. Shaalan, “A Systematic Literature Review on Phishing Email Detection Using Natural Language Processing Techniques,” IEEE Access, vol. 10, 2022. doi:10.1109/ACCESS.2022.3183083.

\[8] F. Heiding, B. Schneier, A. Vishwanath, J. Bernstein, and P. S. Park, “Devising and Detecting Phishing: Large Language Models vs. Smaller Human Models,” arXiv:2308.12287, 2023.

\[9] T. Koide, N. Fukushi, H. Nakano, and D. Chiba, “ChatSpamDetector: Leveraging Large Language Models for Effective Phishing Email Detection,” arXiv:2402.18093, 2024.

\[10] S. S. Roy, P. Thota, K. V. Naragam, and S. Nilizadeh, “From Chatbots to PhishBots? Preventing Phishing Scams Created Using ChatGPT, Google Bard and Claude,” arXiv:2310.19181, 2023.

\[11] T. Kojima, S. S. Gu, M. Reid, Y. Matsuo, and Y. Iwasawa, “Large Language Models are Zero-Shot Reasoners,” in Proc. NeurIPS, 2022. arXiv:2205.11916.

\[12] J. Wei et al., “Chain-of-Thought Prompting Elicits Reasoning in Large Language Models,” in Proc. NeurIPS, 2022. arXiv:2201.11903.

\[13] E. J. Hu et al., “LoRA: Low-Rank Adaptation of Large Language Models,” in Proc. ICLR, 2022. arXiv:2106.09685.

\[14] P. Joshi, S. Santy, A. Budhiraja, K. Bali, and M. Choudhury, “The State and Fate of Linguistic Diversity and Inclusion in the NLP World,” in Proc. ACL, 2020. arXiv:2004.09095.

\[15] M. A. Hedderich, L. Lange, H. Adel, J. Strötgen, and D. Klakow, “A Survey on Recent Approaches for Natural Language Processing in Low-Resource Scenarios,” in Proc. NAACL-HLT, 2021. arXiv:2010.12309.

\[16] R. Yeshpanov, Y. Khassanov, and H. A. Varol, “KazNERD: Kazakh Named Entity Recognition Dataset,” in Proc. LREC, 2022. arXiv:2111.13419.

\[17] M. Togmanov et al., “KazMMLU: Evaluating Language Models on Kazakh, Russian, and Regional Knowledge of Kazakhstan,” in Proc. ACL, 2025. arXiv:2502.12829.

\[18] A. Dubey et al. (Llama Team, AI @ Meta), “The Llama 3 Herd of Models,” arXiv:2407.21783, 2024.

\[19] Gemma Team, Google DeepMind, “Gemma 2: Improving Open Language Models at a Practical Size,” arXiv:2408.00118, 2024.

\[20] OpenAI, “GPT-4o System Card,” arXiv:2410.21276, 2024.

\[21] O. K. Sahingoz, E. Buber, O. Demir, and B. Diri, “Machine learning based phishing detection from URLs,” Expert Systems with Applications, vol. 117, 2019. doi:10.1016/j.eswa.2018.09.029.

\[22] A. Vaswani et al., “Attention Is All You Need,” in Proc. NeurIPS, 2017. arXiv:1706.03762.

\[23] T. Wolf et al., “Transformers: State-of-the-Art Natural Language Processing,” in Proc. EMNLP: System Demonstrations, 2020. arXiv:1910.03771.

\[24] L. Breiman, “Random Forests,” Machine Learning, vol. 45, no. 1, pp. 5–32, 2001.

\[25] F. Pedregosa et al., “Scikit-learn: Machine Learning in Python,” Journal of Machine Learning Research, vol. 12, pp. 2825–2830, 2011.

\[26] Anti-Phishing Working Group (APWG), “Phishing Activity Trends Reports.” \[Online]. Available: https://apwg.org/trendsreports/ (accessed Oct. 2026).

\[27] The Apache Software Foundation, “Apache SpamAssassin Documentation.” \[Online]. Available: https://spamassassin.apache.org/ (accessed Oct. 2026).

\[28] Proofpoint, Inc., “Email Protection (product documentation).” \[Online]. Available: https://www.proofpoint.com/ (accessed Oct. 2026).

\[29] S. Ramírez, “FastAPI Documentation.” \[Online]. Available: https://fastapi.tiangolo.com/ (accessed Oct. 2026).

\[30] The PostgreSQL Global Development Group, “PostgreSQL Documentation.” \[Online]. Available: https://www.postgresql.org/docs/ (accessed Oct. 2026).

