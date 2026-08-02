<div align="center">

![Header](https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=12&height=180&section=header&text=Alex%20Chang&fontSize=42&fontColor=ffffff&animation=fadeIn&desc=Backend%20/%20Full-Stack%20Software%20Engineer&descAlignY=62&descSize=18)

<img src="https://readme-typing-svg.demolab.com/?font=Fira+Code&pause=1000&color=A78BFA&center=true&vCenter=true&width=640&lines=Backend+%26+Microservices+Engineer;Rewriting+Java+Microservices+in+Go;High-Concurrency+%26+Ledger+Correctness;Proving+Equivalence+with+Contract+Tests" alt="Typing SVG" />

[![Location](https://img.shields.io/badge/Taichung%2C%20Taiwan-7C3AED?style=for-the-badge&logo=googlemaps&logoColor=white)]()
[![LinkedIn](https://img.shields.io/badge/LinkedIn-6D28D9?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/alexchang1229/)
[![Gmail](https://img.shields.io/badge/Gmail-8A2BE2?style=for-the-badge&logo=gmail&logoColor=white)](mailto:johnjon823@gmail.com)
[![GitHub](https://img.shields.io/badge/GitHub-4C1D95?style=for-the-badge&logo=github&logoColor=white)](https://github.com/AlexChang1999)

![Profile Views](https://komarev.com/ghpvc/?username=AlexChang1999&color=8a2be2&style=for-the-badge)
![Followers](https://img.shields.io/github/followers/AlexChang1999?style=for-the-badge&color=8a2be2&logo=github&logoColor=white)
![Stars](https://img.shields.io/github/stars/AlexChang1999?style=for-the-badge&color=8a2be2&logo=github&logoColor=white)

</div>

---

## 🟣 About Me

I'm a backend engineer working on **microservice architecture**, **high-concurrency system design**, and **ledger correctness**. I built **Lucky Star Casino** — a 7-service Java/Spring Boot casino ledger platform — and I'm now **rewriting it in Go, service by service**.

**The interesting part isn't the rewrite — it's proving it's equivalent.** Every replaced service has to pass the *same black-box contract suite* as the Java original, so "it behaves identically" is evidence, not a claim. Along the way I document every silent failure mode I hit (**39 and counting**): the ones with no error message, where health checks stay green and only the balance is wrong.

**開發背景**：後端工程師，專注微服務架構、高併發與**帳務正確性**。目前正在把自己開發的 7 服務 Java/Spring Boot 娛樂城**逐服務重構為 Go**，並用**同一份黑箱契約測試對兩版都跑**來證明等價——而不是宣稱等價。

🟣 **Open To:** Backend / Go Engineer roles · Taiwan (remote or onsite)

---

## 🛠️ Tech Stack

![Skills](https://skillicons.dev/icons?i=go,java,spring,python,mysql,postgres,redis,mongodb,docker,git,linux,githubactions&theme=dark)

![Gin](https://img.shields.io/badge/Gin-00ADD8?style=for-the-badge&logo=go&logoColor=white)
![GORM](https://img.shields.io/badge/GORM-00ADD8?style=for-the-badge&logo=go&logoColor=white)

![Kafka](https://img.shields.io/badge/Kafka-000000?style=for-the-badge&logo=apachekafka&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=for-the-badge&logo=prometheus&logoColor=white)
![JMeter](https://img.shields.io/badge/JMeter-D22128?style=for-the-badge&logo=apachejmeter&logoColor=white)
![Codex](https://img.shields.io/badge/Codex-412991?style=for-the-badge&logo=openai&logoColor=white)
![Claude](https://img.shields.io/badge/Claude-D97757?style=for-the-badge&logo=claude&logoColor=white)

---

## 🚀 Featured Projects

### 🐹 Lucky Star Casino **Go** — Rewriting a Running Java Platform in Go

> **Not "a casino written in Go" — an engine swap on a system that already runs.**
> Every behaviour has an existing correct answer; the job is to match it, not invent it.
> And "it matches" needs proof: **the same black-box contract suite runs against both
> the Java service and its Go replacement, and both must be green.**

| Category | Details |
|---|---|
| Stack | **Go 1.26** · Gin · GORM · MySQL 8.4 · MongoDB · Redis · **Kafka** (`segmentio/kafka-go`) · Docker · GitHub Actions |
| **Equivalence** | Cross-language contract suite: **11 tests / 15 table cases, green against Java (:8082) *and* Go (:8182)** |
| **Ledger correctness** | Idempotency via UNIQUE-key conflict (not check-then-insert), optimistic locking with `RowsAffected` checks, **in-transaction compensation** for MySQL's non-aborting duplicate-key errors |
| **Distributed consistency** | Transactional Outbox: business write + event write in **one** transaction; poller uses `FOR UPDATE SKIP LOCKED`; only ACK'd events get marked SENT |
| **Measured** | 20 concurrent debits on one wallet → **all 20 succeed**; RR isolation → **19/20 hit deadlock 1213**, RC → 0; event latency **208–372 ms**; image **36.3 MB** (scratch, `CGO_ENABLED=0`) |
| **Engineering rigor** | `-race` everywhere · CI spins up **real MySQL + Kafka** · **39 documented landmines**, most with *no error message* · 4 ADRs, two of which formally overturn the original team's decisions |
| Repository | [GitHub →](https://github.com/AlexChang1999/lucky-star-casino-go) |

### 📡 Lucky Star Notify Go — Hand-Rolled STOMP 1.2 Server

The methodology proof for the rewrite above: the first service ported to Go, with **no
WebSocket/STOMP framework** — the protocol subset is implemented from the spec, because
a framework would have been in the way rather than helpful.

| Category | Details |
|---|---|
| Stack | **Go** · standard-library `net/http` (deliberately *not* Gin) · WebSocket · Kafka · Prometheus |
| **Equivalence** | Contract suite **14/14 green against both Java and Go** |
| **Measured** | Image **18.6 MB** · **12.9 MiB idle RSS** (vs. a 1.28 GB-limited JVM) · broadcast p95 **4.75 ms** |
| Why it matters | Shows *when to use a framework and when not to* — the part of the stack where hand-rolling was the right call |
| Repository | [GitHub →](https://github.com/AlexChang1999/Lucky_Star_Notify_Go) |

### 🎰 Lucky Star Casino — Microservices Casino Ledger Platform (Java, the original)

The system being rewritten: 7 Spring Boot services, 555 `.java` files, dual datastores,
Kafka event bus, Transactional Outbox, Redis as primary storage for leaderboards and sessions.

| Category | Details |
|---|---|
| Stack | Java · Spring Boot · Spring Cloud Gateway · PostgreSQL · Redis · Kafka · Docker · Prometheus |
| Scale | Multi-service architecture with a dedicated API gateway and message queue |
| Performance | Designed around a documented high-concurrency architecture ([design doc](https://drive.google.com/file/d/1TazUv2ptJqzXvXUxr06XM8-N4Nqm6c-M/view)) |
| Security | Focus on transaction consistency and ledger integrity across distributed services |
| Repository | [GitHub →](https://github.com/opitt2029/Lucky_Star_Casino) |

### 📈 Albee Stock — Multi-Bot Automated Trading System

Multi-bot architecture for automated US stock trading strategies, each bot running an independent strategy via Alpaca Paper Trading, with a custom backtesting engine and risk controls.

| Category | Details |
|---|---|
| Stack | Python · FastAPI · React (Vite) · SQLite/Alembic · Alpaca API |
| Scale | 9 trading strategies, multi-bot management, local LLM-assisted strategy workbench |
| Repository | [GitHub →](https://github.com/AlexChang1999/Albee_Stock) |
### 🛋️ Sogno di Casa — Premium Furniture E-Commerce Platform

Full-stack e-commerce platform for high-end designer furniture, with product browsing, cart, membership system, and an admin back office.

| Category | Details |
|---|---|
| Stack | Java 21 · Spring Boot 3.2 · Spring Security (JWT) · PostgreSQL · Vanilla JS |
| Features | JWT stateless auth with email OTP verification, product/brand/designer catalog, cart & checkout, admin CRUD |
| Repository | [GitHub →](https://github.com/AlexChang1999/Sogno_di_Casa) |

### 🤖 TrumpTrueSocial_Bot — 24/7 Social Monitoring Bot

Always-on worker that monitors a public figure's Truth Social posts and pushes real-time notifications to Telegram and Discord, running independently of any local machine.

| Category | Details |
|---|---|
| Stack | Python · Telegram Bot API · Discord Webhooks · Oracle Cloud / Fly.io |
| Design | Persistent polling loop (5-min interval) with RSS fallback and de-duplication to prevent repeat notifications |
| Repository | [GitHub →](https://github.com/AlexChang1999/TrumpTrueSocial_Bot) |

---

## 💼 Experience

**Lucky Star Casino — Go Rewrite** · Solo (2026.7 – Present)

• Rewriting a running 7-service Java/Spring Boot platform into Go, **one service at a time**, with a black-box contract suite that must stay green against **both** implementations.
• Ported the wallet ledger: idempotency via UNIQUE-key conflict, optimistic locking verified by `RowsAffected`, and a Transactional Outbox that writes the business row and the event **in the same transaction**.
• Found and fixed **failure modes that produce no error message** — MySQL's case-insensitive default collation weakening idempotency keys; gap-lock deadlocks (19/20 concurrent bets) fixed by pinning the transaction to READ COMMITTED; a background poller silently blocking the ledger's hot path.
• Built the CI that makes it hold: lint (incl. build-tagged files) → unit `-race` → **real MySQL + Kafka integration** → contract tests → container image.

**Lucky Star Casino** — Backend Engineer, Java (2026.5 – Present)

• Designed and built a microservices-based casino ledger platform with a dedicated API gateway and message queue.
• Implemented high-throughput transaction handling and monitoring for distributed transaction consistency.
• Documented and applied a high-concurrency system design for scalable service-to-service communication.

---

## 📊 GitHub Analytics

<div align="center">

![GitHub Stats](https://github-stats-extended.vercel.app/api?username=AlexChang1999&show_icons=true&theme=tokyonight&hide_border=true&bg_color=0d1117&title_color=A78BFA&icon_color=A78BFA)
![Streak Stats](https://github-readme-streak-stats.herokuapp.com/?user=AlexChang1999&theme=tokyonight&hide_border=true&background=0d1117&ring=A78BFA&fire=A78BFA)

![Top Langs](https://github-stats-extended.vercel.app/api/top-langs?username=AlexChang1999&layout=compact&theme=tokyonight&hide_border=true&bg_color=0d1117&title_color=A78BFA)

**🏆 Trophies**

![Trophies](https://trophy.benkou.dev/?username=AlexChang1999&theme=algolia&no-frame=true&column=7&margin-w=8&margin-h=8)

![Activity Graph](https://github-readme-activity-graph.vercel.app/graph?username=AlexChang1999&theme=tokyo-night&hide_border=true&bg_color=0d1117&color=A78BFA&line=A78BFA&point=ffffff)

</div>

---

## 🎯 Current Focus

**Currently building:** the Go rewrite of Lucky Star Casino — wallet ledger, Transactional Outbox, cross-language contract tests
**Next up:** Kafka consumers + CQRS read model, then a **Go-written API gateway** (JWT, rate limiting, circuit breaking) replacing Spring Cloud Gateway
**Exploring:** goroutine/GC tuning with `pprof`, distributed transaction patterns, OpenTelemetry tracing across services
**Open to:** Backend / **Go** Engineer roles in Taiwan

---

## 📫 Connect

[![LinkedIn](https://img.shields.io/badge/LinkedIn-6D28D9?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/alexchang1229/)
[![Gmail](https://img.shields.io/badge/Gmail-8A2BE2?style=for-the-badge&logo=gmail&logoColor=white)](mailto:johnjon823@gmail.com)

---

<div align="center">

*"Building reliable systems, one commit at a time."*

![Footer](https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=12&height=100&section=footer)

</div>
