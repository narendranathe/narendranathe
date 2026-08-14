# Narendranath Edara

I build data pipelines at ExponentHR (payroll, 400 clients). Cut CDC ETL 30->8 min. Shipped a signed PyPI pkg, 330+ tests. Ex-Zomato, Udaan.

```
At a glance: 3 yrs DE, 6 total | payroll platform, 400 clients | CDC ETL 30m -> 8m (-67% compute) | PyPI pkg, 330+ tests, Sigstore-signed | ex-Zomato, ex-Udaan
```

---

## Repos, in order

**[repo-context-hooks](https://github.com/narendranathe/repo-context-hooks)** — gives coding agents memory across sessions.
Mechanism: hooks fire at session boundaries (start, pre-compact, end) and write state to checked-in markdown, so the next session reads the repo instead of re-deriving it.
Tradeoff: checked-in markdown over a database or cloud sync, because the repo is the one thing guaranteed to exist when the next session starts; telemetry rejected (off by default, preview before send) because a tool that reads your repos earns trust first.
Impact: ~600 tokens and ~5 min saved per resumed session vs cold rediscovery, from the tool's own local log: 110 events, 90/100 contract score against a 20/100 no-hooks baseline.

**[FinTune](https://github.com/narendranathe/fintune)** — Mistral-7B fine-tuned for financial sentiment, served like a product, not a demo.
Mechanism: QLoRA freezes the 4-bit base weights and trains only small adapter matrices; at serve time, PII is masked before inference and a drift monitor watches output after.
Tradeoff: regex that over-masks (any 8-17 digit string) over ML name detection, because a false positive costs readability while a false negative is a GLBA report; ~1-2% F1 loss accepted against full fine-tuning, which needs ~56 GB of VRAM.
Impact: fine-tune runs in ~6 GB vs ~56 GB, so it fits on one consumer GPU; 35+ tests cover the breaker and drift paths, not just the model.

**[Fraud Detection](https://github.com/narendranathe/fraud-detection-ml-platform)** — Kafka pipeline scoring transactions with LightGBM in real time.
Mechanism: a consumer pulls 50-message batches, posts each to a FastAPI scorer, and writes prediction plus latency to Postgres with dedupe-on-insert, so a replayed message is a no-op.
Tradeoff: auto-commit offsets plus dedupe keys over exactly-once delivery, same protection without the broker ceremony; the known cost is one fresh DB connection per score, which caps the path at ~0.5 predictions/s against a 100 TPS producer, visible on the Grafana panel in the README.
Impact: P99 1.12ms per score from the Prometheus histogram; longest run flagged 21 of 2,082 (0.94%) against a 2.03% training base rate, which exposed the untuned threshold.

**[AutoApply AI](https://github.com/narendranathe/autoapply-ai)** — document intelligence pipeline that turns web forms and job pages into structured data.
Mechanism: a Chrome MV3 content script watches the DOM in tiers (mutation observer first, resize observer with a 50px/400ms debounce for wizard steps, postMessage bridge for iframes), posts findings to a 40-endpoint FastAPI backend, and routes each question type to one of 7 LLM providers in priority order.
Tradeoff: Shadow DOM overlay plus sidepanel over rendering React into the host page, because CSS and CSP fights with Workday have no bottom; a body-level resize observer was rejected after it fired 10-15 times per step animation and raced the state map.
Impact: 355 tests, 11 migrations; the tier-1 observer alone covers ~95% of ATS platforms.

**[JobScout](https://github.com/narendranathe/job-scout)** — ingestion pipeline keeping 130+ fragile career-page sources alive.
Mechanism: 6 ATS APIs polled on tiers (24 companies every 5 min, full sweep hourly), each scraper wrapped in retry-with-backoff that returns an empty list instead of raising, results normalized into SQLite WAL and ranked by keyword plus TF-IDF.
Tradeoff: SQLite WAL over Postgres, because one worker means one writer and WAL gives concurrent reads with no server to run; let-it-crash error handling rejected, because one schema change must zero out one company, not the sweep.
Impact: $0/month on free tiers (~1,080 of 2,000 Action minutes); the 12am-5:30am skip cuts ~25% of compute with zero data loss.

**[tailor-resume](https://github.com/narendranathe/tailor-resume)** — stdlib-only engine that scores and rewrites a resume against a job description.
Mechanism: 5 input formats parse into one Profile type (PDFs through a 4-tier fallback chain with glyph cleanup), a weighted formula scores the match (40% keywords, 30% category coverage, 20% bullet quality, 10% seniority), and bullets are cut to 20 words at render time, not in the editor.
Tradeoff: deterministic stdlib core over LLM-first generation, because keyword coverage is measurable and free; the gate declines to generate below a score of 50, since a tool that always produces a resume lies some of the time.
Impact: 458+ tests; the error log shows why the gate matters, a 3-character token filter once scored "sql", "ml", and "etl" as zero overlap until the floor dropped to 2.

---

## Day job

Data engineer at ExponentHR, a payroll platform for ~400 clients. CDC ETL from 30 minutes to 8 (-67% compute). Deployment cycle from 3 months to 14 days. Self-healing SQL Agent monitoring and AAG failover runbooks. Before that: Zomato (300 restaurants, -Rs18 to +Rs2 per order) and Udaan (Rs5 Cr/month GMV in 3 months).

## Links and credentials

- [LinkedIn](https://linkedin.com/in/narendranathe) | [Portfolio](https://narendranathe.github.io) | [Substack](https://narendranathe.substack.com) | edara.narendranath@gmail.com
- M.S. Information Science & Technology, Missouri S&T, 4.0 GPA
- DP-700 Microsoft Certified Data Engineer
- [Published: Sentiment Analysis for Visitor Insights, Taylor & Francis](https://doi.org/10.1080/10495142.2025.2525123)
