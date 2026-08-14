<h1 align="center">Narendranath Edara</h1>

<p align="center">
  <a href="https://narendranathe.github.io"><img src="https://img.shields.io/badge/Portfolio-Live%20Site-2D5A4A?style=flat-square" alt="Portfolio" /></a>
  <a href="https://linkedin.com/in/narendranathe"><img src="https://img.shields.io/badge/LinkedIn-Narendranath%20Edara-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
  <a href="https://narendranathe.substack.com"><img src="https://img.shields.io/badge/Substack-Notes%20on%20AI%20Systems-FF6719?style=flat-square&logo=substack&logoColor=white" alt="Substack" /></a>
  <a href="mailto:edara.narendranath@gmail.com"><img src="https://img.shields.io/badge/Email-edara.narendranath%40gmail.com-EA4335?style=flat-square&logo=gmail&logoColor=white" alt="Email" /></a>
  <a href="https://doi.org/10.1080/10495142.2025.2525123"><img src="https://img.shields.io/badge/Publication-Taylor%20%26%20Francis-8A2BE2?style=flat-square" alt="Publication" /></a>
</p>

I spent 3 years in commercial ops learning what bad data costs. At Zomato that meant moving 300 restaurants from -Rs18 to +Rs2 per order. I kept waiting on data teams to answer basic questions. So I became one.

Now I build data pipelines at ExponentHR, a payroll platform for ~400 clients. I cut CDC ETL from 30 minutes to 8 and compute by 67%. On the side I ship a signed PyPI package with 330+ tests, because I like tools you can verify.

```
At a glance: 3 yrs DE, 6 total | payroll platform, 400 clients | CDC ETL 30m -> 8m (-67% compute) | PyPI pkg, 330+ tests, Sigstore-signed | ex-Zomato, ex-Udaan
```

---

## The repos, ranked by what they prove

**[repo-context-hooks](https://github.com/narendranathe/repo-context-hooks)** — gives coding agents memory across sessions.
Mechanism: hooks fire at session boundaries (start, pre-compact, end) and write state to checked-in markdown. The next session reads the repo instead of re-deriving it.
Tradeoff: checked-in markdown over a database or cloud sync. The repo is the one thing guaranteed to exist when the next session starts. Telemetry stays off by default with preview before send, because a tool that reads your repos earns trust first.
Impact: ~600 tokens and ~5 min saved per resumed session vs cold rediscovery. From the tool's own local log: 110 events, 90/100 contract score against a 20/100 no-hooks baseline.

**[FinTune](https://github.com/narendranathe/fintune)** — Mistral-7B fine-tuned for financial sentiment, served like a product, not a demo.
Mechanism: QLoRA freezes the 4-bit base weights and trains only small adapter matrices. At serve time, PII is masked before inference and a drift monitor watches output after.
Tradeoff: regex that over-masks (any 8-17 digit string) over ML name detection. A false positive costs readability. A false negative is a GLBA report. ~1-2% F1 loss accepted against full fine-tuning, which needs ~56 GB of VRAM.
Impact: fine-tune runs in ~6 GB vs ~56 GB, so it fits on one consumer GPU. 35+ tests cover the breaker and drift paths, not just the model.

**[Fraud Detection](https://github.com/narendranathe/fraud-detection-ml-platform)** — Kafka pipeline scoring transactions with LightGBM in real time.
Mechanism: a consumer pulls 50-message batches, posts each to a FastAPI scorer, and writes prediction plus latency to Postgres with dedupe-on-insert. A replayed message is a no-op.
Tradeoff: auto-commit offsets plus dedupe keys over exactly-once delivery. Same protection, no broker ceremony. The known cost is one fresh DB connection per score, which caps the path at ~0.5 predictions/s against a 100 TPS producer. The Grafana panel in the README shows it.
Impact: P99 1.12ms per score from the Prometheus histogram. Longest run flagged 21 of 2,082 (0.94%) against a 2.03% training base rate, which exposed the untuned threshold.

**[AutoApply AI](https://github.com/narendranathe/autoapply-ai)** — document intelligence pipeline that turns web forms and job pages into structured data.
Mechanism: a Chrome MV3 content script watches the DOM in tiers (mutation observer first, resize observer with a 50px/400ms debounce for wizard steps, postMessage bridge for iframes). It posts findings to a 40-endpoint FastAPI backend. Each question type routes to one of 7 LLM providers in priority order.
Tradeoff: Shadow DOM overlay plus sidepanel over rendering React into the host page. CSS and CSP fights with Workday have no bottom. A body-level resize observer was rejected after it fired 10-15 times per step animation and raced the state map.
Impact: 355 tests, 11 migrations. The tier-1 observer alone covers ~95% of ATS platforms.

**[JobScout](https://github.com/narendranathe/job-scout)** — ingestion pipeline keeping 130+ fragile career-page sources alive.
Mechanism: 6 ATS APIs polled on tiers (24 companies every 5 min, full sweep hourly). Each scraper runs inside retry-with-backoff that returns an empty list instead of raising. Results land normalized in SQLite WAL, ranked by keyword plus TF-IDF.
Tradeoff: SQLite WAL over Postgres. One worker means one writer, and WAL gives concurrent reads with no server to run. Let-it-crash error handling was rejected. One schema change must zero out one company, not the sweep.
Impact: $0/month on free tiers (~1,080 of 2,000 Action minutes). The 12am-5:30am skip cuts ~25% of compute with zero data loss.

**[tailor-resume](https://github.com/narendranathe/tailor-resume)** — stdlib-only engine that scores and rewrites a resume against a job description.
Mechanism: 5 input formats parse into one Profile type (PDFs through a 4-tier fallback chain with glyph cleanup). A weighted formula scores the match: 40% keywords, 30% category coverage, 20% bullet quality, 10% seniority. Bullets are cut to 20 words at render time, not in the editor.
Tradeoff: deterministic stdlib core over LLM-first generation. Keyword coverage is measurable and free. The gate declines to generate below a score of 50, since a tool that always produces a resume lies some of the time.
Impact: 458+ tests. The error log shows why the gate matters. A 3-character token filter once scored "sql", "ml", and "etl" as zero overlap until the floor dropped to 2.

---

## Day job and before

Data engineer at ExponentHR, payroll for ~400 clients. CDC ETL from 30 minutes to 8 (-67% compute). Deployment cycle from 3 months to 14 days. Self-healing SQL Agent monitoring and AAG failover runbooks.

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

- M.S. Information Science & Technology, Missouri S&T, 4.0 GPA
- DP-700 Microsoft Certified Data Engineer
- [Published: Sentiment Analysis for Visitor Insights, Taylor & Francis](https://doi.org/10.1080/10495142.2025.2525123)
