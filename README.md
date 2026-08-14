<h1 align="center">Narendranath Edara</h1>

<p align="center">
  <a href="https://narendranathe.github.io"><img src="https://img.shields.io/badge/Portfolio-Live%20Site-2D5A4A?style=flat-square" alt="Portfolio" /></a>
  <a href="https://linkedin.com/in/narendranathe"><img src="https://img.shields.io/badge/LinkedIn-Narendranath%20Edara-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
  <a href="https://narendranathe.substack.com"><img src="https://img.shields.io/badge/Substack-Notes%20on%20AI%20Systems-FF6719?style=flat-square&logo=substack&logoColor=white" alt="Substack" /></a>
  <a href="mailto:edara.narendranath@gmail.com"><img src="https://img.shields.io/badge/Email-edara.narendranath%40gmail.com-EA4335?style=flat-square&logo=gmail&logoColor=white" alt="Email" /></a>
  <a href="https://doi.org/10.1080/10495142.2025.2525123"><img src="https://img.shields.io/badge/Publication-Taylor%20%26%20Francis-8A2BE2?style=flat-square" alt="Publication" /></a>
</p>

**Builds:** the detection and recovery layer under payroll data pipelines: CDC, failover runbooks, self-healing SQL Agent monitoring.
**Scale:** CDC 30 to 8 min with the freshness SLA held, 99.9% less data moved, releases 3 months to 14 days, failover MTTR under 1 hr.
**Proof:** `pip install repo-context-hooks`, then check the Sigstore signature. 330+ tests, zero dependencies.

---

I spent 3 years in commercial ops learning what bad data costs. At Zomato that meant moving 300 restaurants from -Rs18 to +Rs2 per order. I kept waiting on data teams to answer basic questions, so I became one.

Now I build data pipelines at ExponentHR, an HR and payroll vendor. CDC ETL runs went from 30 minutes to under 8 with the freshness SLA held, and compute dropped 67%.

## The repos, ranked by what they prove

**[repo-context-hooks](https://github.com/narendranathe/repo-context-hooks): zero-dependency git hooks that hand an LLM agent the repo's current state at session start.**
Mechanism: Pre- and post-commit hooks serialize branch, staged diff, recent commits, and project layout into a markdown file checked into the repo, so the next agent session reads one file instead of re-walking the tree.
Tradeoff: Checked-in markdown and a standard-library-only runtime over a daemon or hosted state store, because the tool installs into any repo with zero footprint and the snapshot is versioned and diffable in git itself. Rejected an embeddings index: for a file this size, a full read beats a vector store plus a build step.
Impact: 330+ passing tests at v1.0, zero runtime dependencies, Sigstore-signed PyPI releases a reviewer can verify without asking me.

**[FinTune](https://github.com/narendranathe/fintune): Mistral-7B fine-tuned for financial sentiment, served behind guardrails with self-recovery.**
Mechanism: LoRA adapters train on top of a frozen 4-bit NF4 base (quantized: weights stored at 4-bit precision to cut memory), so only the adapter weights update. At serve time each request passes a PII redactor before inference, KL divergence between recent and reference output feeds the drift monitor, and a three-state breaker picks the recovery: reload the model, shed batch size, or drop to a smaller quantized checkpoint.
Tradeoff: QLoRA adapters over full fine-tuning, so training fits on one GPU. Full-parameter tuning multiplies VRAM cost for a gain this dataset cannot show.
Impact: 35+ tests across five layers: data, model, guardrails, serving, and recovery.

**[Fraud Detection](https://github.com/narendranathe/fraud-detection-ml-platform): Kafka to LightGBM scoring with exactly-once processing and full serving metrics.**
Mechanism: Consumers commit Kafka offsets only after the score write succeeds, so a crash mid-batch replays instead of double-counting; that is the exactly-once part. LightGBM serves the score, MLflow versions the model, and Prometheus records latency histograms that Grafana renders.
Tradeoff: Gradient-boosted trees over a neural net, because the features are tabular and trees train in minutes and score in microseconds. A neural net would blow the single-digit-millisecond P99 budget for no measured gain on this data.
Impact: P99 of 1.12 ms at 100+ TPS sustained. Training data is synthetic, 100K generated transactions at about 2% fraud, and the repo README says so up front.

**[AutoApply AI](https://github.com/narendranathe/autoapply-ai): document-intelligence backend that reads job posts and writes grounded answers.**
Mechanism: Each generation request walks a six-provider LLM cascade with per-provider fallback. pgvector, inside the same Postgres that holds the records, retrieves prior work history to ground the answer, and a Chrome MV3 extension drives 11 ATS adapters that pierce shadow DOM and queue submissions when offline.
Tradeoff: A provider cascade over a single API, because one provider's rate limit or outage halts a batch run mid-form. pgvector over a standalone vector database, because Postgres was already the system of record: one less service to deploy and back up.
Impact: 355 backend tests over 40+ endpoints. Private deployment; public release waits on tracked security fixes.

**[JobScout](https://github.com/narendranathe/job-scout): 109 career pages scraped on a schedule, built so one broken source cannot kill the run.**
Mechanism: Each source sits behind its own circuit breaker; after repeated failures the breaker opens, that scraper is skipped, and the run continues. Results land in SQLite in WAL mode (write-ahead log: readers never block the writer), TF-IDF scores new postings against 95+ resume variants, and matches above threshold push to Discord and Telegram.
Tradeoff: SQLite WAL over Postgres, because the dataset fits in one file and WAL gives concurrent reads with no server to run. Rejected any hosted database because the whole design runs free on GitHub Actions minutes.
Impact: 109 sources monitored at zero monthly cost, where a dead scraper now costs one source instead of the run.

**[tailor-resume](https://github.com/narendranathe/tailor-resume): parses a resume and a job post, then rewrites bullets to fit a measured page budget.**
Mechanism: After parsing and matching, the rewriter checks each bullet against a character budget calibrated from compiled PDF output, so length is enforced against rendered lines, not token counts.
Tradeoff: Deterministic budgets over asking the model to "keep it short", because token counts do not predict rendered lines. A budget fails loudly at write time instead of overflowing the PDF silently.
Impact: 190 tests across parse, match, and render. Supporting tool for the resume system, positioned that way on purpose.

---

## Day job and before

Data engineer at ExponentHR, an HR and payroll vendor. CDC ETL from 30 minutes to under 8 with the freshness SLA held, compute down 67%. Deployment cycle from 3 months to 14 days. Self-healing SQL Agent monitoring, and AAG failover runbooks with MTTR under 1 hr.

Zomato: 300 restaurants, -Rs18 to +Rs2 per order. Udaan: Rs5 Cr/month GMV in 3 months.

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
- [Publication, Taylor & Francis](https://doi.org/10.1080/10495142.2025.2525123)
