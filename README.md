<h1 align="center">Narendranath Edara (Naren)</h1>

<p align="center">
  <strong>Data engineer at ExponentHR. Cut CDC ETL 30 min to 8 min, deploys 3 months to 14 days. Open source: 330+ tests, zero deps, signed releases.</strong>
</p>

<p align="center">
  <img src="https://komarev.com/ghpvc/?username=narendranathe&label=Profile%20views&color=0e75b6&style=flat" alt="narendranathe profile views" />
</p>

<p align="center">
  <a href="https://narendranathe.github.io"><img src="https://img.shields.io/badge/Portfolio-Live%20Site-2D5A4A?style=flat-square" alt="Portfolio" /></a>
  <a href="https://linkedin.com/in/narendranathe"><img src="https://img.shields.io/badge/LinkedIn-Narendranath%20Edara-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
  <a href="https://narendranathe.substack.com"><img src="https://img.shields.io/badge/Substack-Notes%20on%20AI%20Systems-FF6719?style=flat-square&logo=substack&logoColor=white" alt="Substack" /></a>
  <a href="mailto:edara.narendranath@gmail.com"><img src="https://img.shields.io/badge/Email-edara.narendranath%40gmail.com-EA4335?style=flat-square&logo=gmail&logoColor=white" alt="Email" /></a>
  <a href="https://doi.org/10.1080/10495142.2025.2525123"><img src="https://img.shields.io/badge/Publication-Taylor%20%26%20Francis-8A2BE2?style=flat-square" alt="Publication" /></a>
</p>

## What I Build

At ExponentHR, I own ETL reliability, deployment automation, and database operations for a multi-tenant HR and payroll platform serving an enterprise client base. I rebuilt the CDC pipeline from 30 minutes to under 8, cut ETL compute cost by 67%, and compressed the deployment cycle from 3 months to 14 days. I also built a self-healing SQL Agent that recovers failed jobs on its own and wrote the AAG failover runbooks the team runs when a database needs to fail over.

Outside of work I write production code, not portfolio filler: FastAPI services, retrieval pipelines, model routing, and a PyPI package with 330+ tests, zero runtime dependencies, and Sigstore-signed releases. Six projects below, ranked by how much of the engineering you can actually verify.

## Where I Fit Best

- Data platform reliability: ETL/CDC pipelines, deployment automation, database failover
- Production ML systems: serving, drift monitoring, automatic recovery
- Backend systems with retrieval, vector search, and model routing
- Open source shipped with real test suites, signed releases, and no unnecessary dependencies

## Featured Systems

<table>
  <tr>
    <td width="50%" valign="top">
      <h3><a href="https://github.com/narendranathe/repo-context-hooks">repo-context-hooks</a></h3>
      Zero-dependency PyPI package that hooks into a coding agent's lifecycle (PostCompact, PreCompact, SessionEnd) to persist project context across sessions instead of losing it to a cold restart. Releases ship with Sigstore attestations you can verify yourself with <code>gh attestation verify</code>.<br/><br/>
      <sub><strong>330+ tests</strong> | <strong>zero runtime deps</strong> | <strong>Sigstore-signed</strong> | <strong>PyPI</strong></sub>
    </td>
    <td width="50%" valign="top">
      <h3><a href="https://github.com/narendranathe/fraud-detection-ml-platform">Fraud Detection ML Platform</a></h3>
      Streams transactions through Kafka into a LightGBM classifier serving predictions at P99 1.12ms, with MLflow tracking every training run and Prometheus/Grafana watching the live service. That latency puts it in the same class as a card-present authorization check, not a nightly batch score.<br/><br/>
      <sub><strong>Kafka</strong> | <strong>LightGBM</strong> | <strong>P99 1.12ms</strong> | <strong>MLflow</strong> | <strong>Prometheus/Grafana</strong></sub>
    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">
      <h3><a href="https://github.com/narendranathe/fintune">FinTune</a></h3>
      Fine-tunes Mistral-7B with QLoRA, quantizes to 4-bit for inference, and serves it through FastAPI behind a PII redaction layer. A drift monitor tracks output distribution and a circuit breaker pulls the model out of rotation automatically, no 2 AM page required.<br/><br/>
      <sub><strong>QLoRA</strong> | <strong>4-bit NF4</strong> | <strong>PII redaction</strong> | <strong>drift monitor</strong> | <strong>circuit breaker</strong> | <strong>35+ tests</strong></sub>
    </td>
    <td width="50%" valign="top">
      <h3><a href="https://github.com/narendranathe/autoapply-ai">AutoApply AI</a></h3>
      Document intelligence platform: a FastAPI backend with 40+ endpoints and a Chrome MV3 extension on top, built around pgvector retrieval and a routing layer that picks between LLM providers per request. Parsing, embedding, and retrieval all run as backend services, not client-side scripts.<br/><br/>
      <sub><strong>40+ endpoints</strong> | <strong>pgvector</strong> | <strong>LLM routing</strong> | <strong>Chrome MV3</strong> | <strong>355 tests</strong></sub>
    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">
      <h3><a href="https://github.com/narendranathe/job-scout">JobScout</a></h3>
      Ingestion engineering exercise: 130+ site-specific scrapers behind circuit breakers, so one broken scraper doesn't take the whole run down with it. Parsed results land in SQLite and get ranked with TF-IDF instead of a black-box relevance API.<br/><br/>
      <sub><strong>130+ scrapers</strong> | <strong>circuit breakers</strong> | <strong>SQLite</strong> | <strong>TF-IDF ranking</strong></sub>
    </td>
    <td width="50%" valign="top">
      <h3><a href="https://github.com/narendranathe/tailor-resume">tailor-resume</a></h3>
      The document-parsing and scoring engine extracted out of the AutoApply AI backend into its own package, shipped through a CLI, a Streamlit app, an MCP server, and a PyPI install. 190 tests cover the core logic once instead of four times across four front ends.<br/><br/>
      <sub><strong>CLI</strong> | <strong>Streamlit</strong> | <strong>MCP</strong> | <strong>PyPI</strong> | <strong>190 tests</strong></sub>
    </td>
  </tr>
</table>

## Core Stack

<p align="left">
  <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python" />
  <img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white" alt="TypeScript" />
  <img src="https://img.shields.io/badge/SQL%20%2F%20T--SQL-CC2927?style=flat-square&logo=microsoftsqlserver&logoColor=white" alt="SQL and T-SQL" />
  <img src="https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white" alt="FastAPI" />
  <img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white" alt="PostgreSQL" />
  <img src="https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white" alt="Redis" />
  <img src="https://img.shields.io/badge/Kafka-231F20?style=flat-square&logo=apachekafka&logoColor=white" alt="Kafka" />
  <img src="https://img.shields.io/badge/Apache%20Spark-E25A1C?style=flat-square&logo=apachespark&logoColor=white" alt="Apache Spark" />
  <img src="https://img.shields.io/badge/Azure-0078D4?style=flat-square&logo=microsoftazure&logoColor=white" alt="Azure" />
  <img src="assets/badges/pgvector.svg" alt="pgvector" />
  <img src="assets/badges/rag.svg" alt="RAG" />
  <img src="assets/badges/vectorless-rag.svg" alt="Vectorless RAG" />
  <img src="assets/badges/mcp.svg" alt="MCP" />
  <img src="https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white" alt="PyTorch" />
  <img src="https://img.shields.io/badge/Hugging%20Face-FFD21E?style=flat-square&logo=huggingface&logoColor=black" alt="Hugging Face" />
  <img src="https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikitlearn&logoColor=white" alt="scikit-learn" />
  <img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white" alt="Docker" />
  <img src="https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white" alt="Kubernetes" />
  <img src="https://img.shields.io/badge/MLflow-0194E2?style=flat-square" alt="MLflow" />
  <img src="https://img.shields.io/badge/Prometheus-E6522C?style=flat-square&logo=prometheus&logoColor=white" alt="Prometheus" />
  <img src="https://img.shields.io/badge/Grafana-F46800?style=flat-square&logo=grafana&logoColor=white" alt="Grafana" />
  <img src="https://img.shields.io/badge/Azure%20DevOps-0078D7?style=flat-square&logo=azuredevops&logoColor=white" alt="Azure DevOps" />
  <img src="https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white" alt="GitHub Actions" />
</p>

## Earlier Foundation

- Missouri S&T: built Azure anomaly detection pipelines, migrated workloads to AKS with HPA, and published NLP research.
- Zomato: took per-order unit economics from -Rs18 to +Rs2 across 300 restaurants.
- Udaan: helped scale a category to Rs5 Cr/month GMV within 3 months.

## Credentials

- M.S. Information Science & Technology, Missouri S&T, 4.0 GPA
- DP-700 Microsoft Certified Data Engineer
- [Published researcher: Sentiment Analysis for Visitor Insights](https://doi.org/10.1080/10495142.2025.2525123)
