<h1 align="center">Narendranath Edara</h1>

<p align="center">
  <strong>I spent three years at Zomato and Udaan watching bad data cost real money.<br/>
  Now I build payroll data pipelines at ExponentHR that fail loud and recover on their own: CDC in 8 minutes instead of 30, at a third of the compute.</strong>
</p>

<p align="center">
  <a href="https://narendranathe.github.io"><img src="https://img.shields.io/badge/Portfolio-Live%20Site-2D5A4A?style=flat-square" alt="Portfolio" /></a>
  <a href="https://linkedin.com/in/narendranathe"><img src="https://img.shields.io/badge/LinkedIn-Narendranath%20Edara-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
  <a href="https://narendranathe.substack.com"><img src="https://img.shields.io/badge/Substack-Notes%20on%20AI%20Systems-FF6719?style=flat-square&logo=substack&logoColor=white" alt="Substack" /></a>
  <a href="mailto:edara.narendranath@gmail.com"><img src="https://img.shields.io/badge/Email-edara.narendranath%40gmail.com-EA4335?style=flat-square&logo=gmail&logoColor=white" alt="Email" /></a>
  <a href="https://doi.org/10.1080/10495142.2025.2525123"><img src="https://img.shields.io/badge/Publication-Taylor%20%26%20Francis-8A2BE2?style=flat-square" alt="Publication" /></a>
</p>

**At a glance:** six years working with data, three of them engineering it, now building the detection and recovery layer under payroll pipelines at ExponentHR. CDC runs went from 30 minutes to 8 by moving only changed rows instead of full-table reloads (about 99.9% less data over a year), with compute down 67% and the freshness SLA held; the Python is public proof: a signed PyPI package with 330+ tests. Before engineering, the commercial side: Zomato (300 restaurants, -Rs18 to +Rs2 per order) and Udaan (Rs5 Cr/month GMV in 3 months).

I spent three years in commercial ops learning what bad data costs before I became a data engineer. The habit that carried over is designing for recovery: self-healing SQL Agent monitoring, idempotent reruns (a failed run just runs again, no manual cleanup), and AAG failover runbooks with MTTR under one hour.

## The repos, ranked by what they prove

**[repo-context-hooks](https://github.com/narendranathe/repo-context-hooks): gives a coding agent memory of your repo between sessions.**
**How it works.** Each commit fires hooks that write the branch, staged diff, recent history, and project layout into a markdown file checked into the repo, so the next session reads one file and starts work with full context.
**Why this design.** Checked-in markdown and a standard-library-only runtime, because the repo is the one thing guaranteed to exist when the next session starts. An embeddings index would add a build step and a dependency to solve a lookup one file already handles.
**The result.** 330+ tests, zero runtime dependencies, Sigstore-signed releases on PyPI: `pip install repo-context-hooks` and check the signature.

**[FinTune](https://github.com/narendranathe/fintune): a Mistral-7B fine-tune with production serving: guardrails, drift watch, self-recovery.**
**How it works.** Training is QLoRA: the base model stays frozen at 4-bit precision and only small adapter matrices learn, so the fine-tune fits on one GPU. Serving adds a PII redactor before inference, a drift monitor scoring KL divergence (a distance score between recent and reference output), and a three-state circuit breaker that reloads the model, sheds batch size, or shifts to a smaller checkpoint.
**Why this design.** Adapters over full fine-tuning: at this dataset size, adapters reach the same quality at a fraction of the VRAM.
**The result.** 35+ tests across five layers: data, model, guardrails, serving, and recovery.

**[Fraud Detection](https://github.com/narendranathe/fraud-detection-ml-platform): a Kafka pipeline that scores transactions in about a millisecond.**
**How it works.** Consumers commit Kafka offsets only after each score is written, so a crash mid-batch replays cleanly and every transaction scores exactly once. LightGBM serves the score, MLflow versions the model, Prometheus and Grafana watch the serving path.
**Why this design.** LightGBM over a neural net: the features are tabular, and trees match that accuracy while training in minutes and scoring in microseconds.
**The result.** P99 of 1.12 ms at 100+ TPS sustained. Training data is synthetic by design (100K generated transactions, about 2% fraud), stated up front in the README.

**[AutoApply AI](https://github.com/narendranathe/autoapply-ai): document intelligence that reads job posts and writes grounded answers.**
**How it works.** Each generation request walks a six-provider LLM cascade with per-provider fallback, pgvector inside the same Postgres retrieves prior work history to ground the answer, and a Chrome MV3 extension drives 11 ATS adapters through shadow DOM with offline queuing.
**Why this design.** The cascade keeps runs moving through any provider's rate limit or outage, and pgvector keeps Postgres as the only datastore to deploy and back up.
**The result.** 355 backend tests over 40+ endpoints. Private deployment today; the README lists the security fixes scheduled before a public release.

**[JobScout](https://github.com/narendranathe/job-scout): 109 career pages on a schedule, each source isolated so every sweep finishes.**
**How it works.** Each scraper sits behind its own circuit breaker: after repeated failures the breaker opens, that source gets skipped, and the sweep completes. Results land in SQLite in WAL mode (write-ahead log, so reads never block writes), TF-IDF scores new postings against 95+ resume variants, and matches push to Discord and Telegram.
**Why this design.** SQLite WAL over Postgres: the whole dataset stays one file, reads run concurrently with writes, and the design lives free on GitHub Actions minutes.
**The result.** 109 sources at zero dollars a month, where one broken scraper costs one source and the other 108 still deliver.

**[tailor-resume](https://github.com/narendranathe/tailor-resume): rewrites resume bullets to fit a measured page budget.**
**How it works.** After parsing the resume and the job post, the rewriter checks every bullet against a character budget calibrated from compiled PDF output, so length is enforced against rendered lines.
**Why this design.** Deterministic budgets over asking the model to keep it short: tokens do not map to rendered lines, and a budget catches overflow at write time, when the fix is cheap.
**The result.** 190 tests across parse, match, and render, supporting the resume system behind the tailored PDFs.

---

## Tools, each with a repo above as proof

<p align="left">
  <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python" />
  <img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white" alt="TypeScript" />
  <img src="https://img.shields.io/badge/SQL%20%2F%20T--SQL-CC2927?style=flat-square&logo=microsoftsqlserver&logoColor=white" alt="SQL and T-SQL" />
  <img src="https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white" alt="FastAPI" />
  <img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white" alt="PostgreSQL" />
  <img src="https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white" alt="Redis" />
  <img src="https://img.shields.io/badge/Kafka-231F20?style=flat-square&logo=apachekafka&logoColor=white" alt="Kafka" />
  <img src="https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white" alt="PyTorch" />
  <img src="https://img.shields.io/badge/Hugging%20Face-FFD21E?style=flat-square&logo=huggingface&logoColor=black" alt="Hugging Face" />
  <img src="https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikitlearn&logoColor=white" alt="scikit-learn" />
  <img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white" alt="Docker" />
  <img src="https://img.shields.io/badge/MLflow-0194E2?style=flat-square" alt="MLflow" />
  <img src="https://img.shields.io/badge/Prometheus-E6522C?style=flat-square&logo=prometheus&logoColor=white" alt="Prometheus" />
  <img src="https://img.shields.io/badge/Grafana-F46800?style=flat-square&logo=grafana&logoColor=white" alt="Grafana" />
  <img src="https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white" alt="GitHub Actions" />
</p>

## Credentials

- M.S. Information Science and Technology, Missouri S&T, 4.0 GPA
- DP-700: Microsoft Certified Fabric Data Engineer Associate
- [An Examination of Sentiment Analysis as a Tool for Gathering Visitor Insights from Online Review Sites for a Museum](https://doi.org/10.1080/10495142.2025.2525123), *Journal of Nonprofit and Public Sector Marketing*, Taylor & Francis, 2025, with D. Bojanic and J. Zhang
