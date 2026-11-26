<div align="center">

![Header](https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=12&height=180&section=header&text=Alex%20Chang&fontSize=42&fontColor=ffffff&animation=fadeIn&desc=Backend%20/%20Go%20Software%20Engineer&descAlignY=62&descSize=18)

<img src="https://readme-typing-svg.demolab.com/?font=Fira+Code&pause=1000&color=A78BFA&center=true&vCenter=true&width=640&lines=Backend+%26+Microservices+Engineer;Rewriting+Java+Microservices+in+Go;Layered+Architecture+%C2%B7+DI+%C2%B7+DTO%2FBO%2FPO;High-Concurrency+%26+Ledger+Correctness;Proving+Equivalence+with+Contract+Tests" alt="Typing SVG" />

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

I'm a backend engineer working on **microservice architecture**, **high-concurrency design**, and **ledger correctness**. I led the technical side of **Lucky Star Casino** — a 7-service Java/Spring Boot casino ledger platform (a simulation, no real money) — and I'm now **rewriting it in Go, service by service**.

**The interesting part isn't the rewrite — it's proving it's equivalent.** Every replaced service has to pass the *same black-box contract suite* as the Java original, so "it behaves identically" is evidence, not a claim. Along the way I document every silent failure mode I hit (**39 and counting**): the ones with no error message, where health checks stay green and only the balance is wrong.

I also keep a small Go service, **fish-room-go**, as a reference for how I structure code day to day: layered architecture, dependency injection, DTO/BO/PO, and tests that run under `-race`.

**開發背景**：後端工程師，專注微服務架構、高併發與**帳務正確性**。目前正在把自己主導開發的 7 服務 Java/Spring Boot 娛樂城（模擬平台，無真實金流）**逐服務重構為 Go**，並用**同一份黑箱契約測試對兩版都跑**來證明等價——而不是宣稱等價。另有個人專案 fish-room-go，展示我平常的分層、依賴注入與測試寫法。

🟣 **Open To:** Backend / Go Engineer roles · Taiwan (remote or onsite)

---

## 🛠️ Tech Stack

![Skills](https://skillicons.dev/icons?i=go,java,spring,python,mysql,postgres,redis,docker,git,linux,githubactions&theme=dark)

![Fiber](https://img.shields.io/badge/Fiber-00ADD8?style=for-the-badge&logo=go&logoColor=white)
![Gin](https://img.shields.io/badge/Gin-00ADD8?style=for-the-badge&logo=go&logoColor=white)
![GORM](https://img.shields.io/badge/GORM-00ADD8?style=for-the-badge&logo=go&logoColor=white)

![Kafka](https://img.shields.io/badge/Kafka-000000?style=for-the-badge&logo=apachekafka&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=for-the-badge&logo=prometheus&logoColor=white)
![JMeter](https://img.shields.io/badge/JMeter-D22128?style=for-the-badge&logo=apachejmeter&logoColor=white)
![Codex](https://img.shields.io/badge/Codex-412991?style=for-the-badge&logo=openai&logoColor=white)
![Claude](https://img.shields.io/badge/Claude-D97757?style=for-the-badge&logo=claude&logoColor=white)

---

## 🚀 Featured Projects

### 🐟 fish-room-go — Layered Go Admin API (Reference Implementation)

A back-office API for fish-game room settings, written to show how I structure a Go service: router → handler → service → repository, manual constructor DI, and separate DTO / BO / PO models. A personal project, not a production system.

| Category | Details |
|---|---|
| Stack | **Go** · Fiber v3 · MySQL 8 · squirrel + `database/sql` (no ORM) · Docker |
| Design | Activity-period overlap checked under `FOR UPDATE`; a UNIQUE key guarantees one default site; `close` is idempotent; all SQL parameterized |
| Concurrency | Bet records are written in batches through a buffered channel; when the queue is full, `Push` times out after 3 s and the handler returns **503** |
| Quality | 65 tests; CI runs `gofmt`, `go vet` and `go test -race` |
| Note | Depends on my private `gokit` module, so it can be read but not built from outside |
| Repository | [GitHub →](https://github.com/AlexChang1999/Golang-Interview) |

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

The system being rewritten: a simulated casino (no real money) built by a team of 4 in 9 weeks, where I was the technical lead. 7 Spring Boot services, 555 `.java` files, dual datastores, Kafka event bus, Transactional Outbox, Redis as primary storage for leaderboards and sessions.

| Category | Details |
|---|---|
| Stack | Java · Spring Boot · Spring Cloud Gateway · PostgreSQL · Redis · Kafka · Docker · Prometheus |
| Correctness | Idempotency key + optimistic locking for balances; Transactional Outbox + Saga for reliable events |
| Resilience | Token-bucket rate limiting and circuit breaking to protect services under load |
| Engineering | 717 JUnit tests, 12 ADRs, and a Node.js tool that generates the 108-task progress table and fails CI when it drifts from the code |
| Design doc | [High-concurrency architecture](https://drive.google.com/file/d/1TazUv2ptJqzXvXUxr06XM8-N4Nqm6c-M/view) |
| Repository | [GitHub →](https://github.com/opitt2029/Lucky_Star_Casino) |

### 📈 Albee Stock — Multi-Bot Automated Trading System

Multi-bot architecture for automated US stock trading strategies, each bot running an independent strategy via Alpaca Paper Trading, with a custom backtesting engine and risk controls.

| Category | Details |
|---|---|
| Stack | Python · FastAPI · React (Vite) · SQLite/Alembic · Alpaca API |
| Scale | 9 trading strategies, multi-bot management, local LLM-assisted strategy workbench |
| Repository | [GitHub →](https://github.com/AlexChang1999/Albee_Stock) |

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

• Rewriting a running 7-service Java/Spring Boot platform into Go (Gin, GORM, MySQL, Redis, Kafka), **one service at a time**, with a black-box contract suite that must stay green against **both** implementations.
• Ported the wallet ledger: idempotency via UNIQUE-key conflict, optimistic locking verified by `RowsAffected`, and a Transactional Outbox that writes the business row and the event **in the same transaction**.
• Found and fixed **failure modes that produce no error message** — MySQL's case-insensitive default collation weakening idempotency keys; gap-lock deadlocks (19/20 concurrent bets) fixed by pinning the transaction to READ COMMITTED; a background poller silently blocking the ledger's hot path.
• Built the CI that makes it hold: lint (incl. build-tagged files) → unit `-race` → **real MySQL + Kafka integration** → contract tests → container image.

**Lucky Star Casino** — Backend Engineer & Technical Lead, Java (2026.5 – Present)

• Led a team of 4 through a 9-week build of a microservices casino ledger platform with an API gateway and a Kafka message queue.
• Kept balances correct under concurrency with idempotency keys and optimistic locking; kept events reliable with Transactional Outbox and Saga.
• Added token-bucket rate limiting, circuit breaking and Prometheus monitoring; backed the code with 717 JUnit tests and 12 ADRs.

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
**Exploring:** goroutine/GC tuning with `pprof`, OpenTelemetry tracing across services, MongoDB, and MCP (Model Context Protocol) — none of these are in my projects yet

---

## 📫 Connect

[![LinkedIn](https://img.shields.io/badge/LinkedIn-6D28D9?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/alexchang1229/)
[![Gmail](https://img.shields.io/badge/Gmail-8A2BE2?style=for-the-badge&logo=gmail&logoColor=white)](mailto:johnjon823@gmail.com)

---

<div align="center">

*"Building reliable systems, one commit at a time."*

![Footer](https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=12&height=100&section=footer)

</div>
