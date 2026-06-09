<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0d1117,50:1a2744,100:0d1117&height=220&section=header&text=Shubham%20Singh&fontSize=56&fontColor=e6edf3&animation=fadeIn&fontAlignY=40&desc=Backend%20Engineer%20%E2%80%94%20Production%20Systems%20%7C%20Django%20%C2%B7%20PostgreSQL%20%C2%B7%20VPS&descAlignY=62&descSize=17&descColor=8b949e" width="100%"/>

</div>

<div align="center">

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0a66c2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/shubham-singh-dev)
[![LeetCode](https://img.shields.io/badge/LeetCode-FFA116?style=for-the-badge&logo=leetcode&logoColor=black)](https://leetcode.com/Sshubham_singh)
[![CWMS Live](https://img.shields.io/badge/CWMS%20Live%20System-sakuntalamindia.com-00b37e?style=for-the-badge&logo=nginx&logoColor=white)](https://sakuntalamindia.com)
[![Email](https://img.shields.io/badge/Email-subhamsinghraigarh%40gmail.com-ea4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:subhamsinghraigarh@gmail.com)

</div>

<br/>

---

## `$ whoami`

```python
class ShubhamSingh:
    degree      = "B.Tech CSE — OP Jindal University (2022–2026) | CGPA: 7.64"
    role        = "Backend Engineer"
    stack       = ["Django 5.x", "PostgreSQL", "Redis", "Nginx", "Gunicorn", "Linux VPS"]
    speciality  = ["REST APIs", "RBAC Systems", "Payroll Engines", "Production Deployments"]
    shipped     = "CWMS — a live workforce management system serving a real paying client"
    philosophy  = "Build things that work in production. Not just in development."
```

I build backend systems that handle **real users, real data, and real consequences** — not localhost demos.

My flagship project, **CWMS**, is deployed on a Hetzner VPS (Ubuntu + Nginx + Gunicorn + Certbot SSL), managing **160 daily-wage construction workers** across 3 sites for a paying contractor client. It handles attendance, payroll, advances, leaves, billing, financial audit logs, and role-scoped access — all in production.

<br/>

---

## ⚡ Engineering Snapshot

<div align="center">

| Domain | Competency |
|---|---|
| **Backend** | Django 5.2 · DRF · JWT Auth · Swagger/OpenAPI 3.0 |
| **Databases** | PostgreSQL 18 · Redis (session cache + dashboard acceleration) |
| **Infrastructure** | Hetzner VPS · Ubuntu · Nginx · Gunicorn · Certbot SSL |
| **Security** | 3-role RBAC · IDOR protection · CSRF hardening · Audit logging |
| **Concurrency** | `transaction.atomic()` + `select_for_update()` — race-condition-free payroll |
| **Testing & CI** | pytest · GitHub Actions · Coverage tracking · CI on every push |
| **Architecture** | Dual-interface (HTML portal + REST API) · Redis-cached dashboards |

</div>

<br/>

---

## 🏗️ Flagship Project — CWMS

> **Production system. Paying client. Real data. Live since June 2026.**

<div align="center">

[![Live System](https://img.shields.io/badge/Live%20System-sakuntalamindia.com-00b37e?style=for-the-badge&logo=nginx&logoColor=white)](https://sakuntalamindia.com)
[![GitHub](https://img.shields.io/badge/Source%20Code-GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Subham-Singh-Dev/cwms)

</div>

**CWMS (Contractor Workforce Management System)** is a full-stack production application built for Sakuntalam India Services — a construction contractor managing daily-wage workers across 3 sites: Raigarh, Bhilai, and Korba.

### What it manages

160 workers · 3 construction sites · 22 employee roles · Attendance · Monthly payroll · Advance deductions · Leave tracking · Expense management (13 categories) · Client billing · Financial audit logs · PDF payslip generation

### Architecture

```
Internet (HTTPS)
       │
  Nginx (port 80 → 301 HTTPS | port 443 SSL — Certbot)
       │ serves /static/ and /media/ directly
  Gunicorn (unix socket, 3 workers)
       │
  Django CWMS (config/wsgi.py)
       ├── PostgreSQL 18    ← all persistent data (47 migrations)
       └── Redis            ← dashboard cache (26ms vs 2118ms uncached)

Two interfaces (both live simultaneously):
  /portal/ + /king/  → HTML UI, session auth (managers & owner)
  /api/              → REST JSON, JWT auth (external/mobile clients)
```

### Engineering Highlights

**Role-Based Access Control (3-tier)**
```
King (Owner)   → full system access, financial reports, all sites
Manager        → scoped to assigned site only, IDOR-protected DB queries
Worker         → self-service portal (phone + password login, payslip view)
```

**Atomic Payroll Engine**

Advance deductions processed inside `transaction.atomic()` with `select_for_update()` — FIFO ordering guarantees financial integrity even under 100–500+ concurrent workers. No race conditions. No double-deductions.

**Production Hardening Decisions**

| Problem Encountered | Root Cause | Resolution |
|---|---|---|
| PostgreSQL `permission denied for schema public` | PG 15+ permission model change | Granted explicit privileges to `cwms_user` |
| CSRF 403 on all POST requests | Wrong `CSRF_TRUSTED_ORIGINS` domain | Corrected env config |
| Infinite SSL redirect loop | `SECURE_SSL_REDIRECT=True` behind Nginx proxy | Removed Django-level redirect; Nginx handles HTTP→HTTPS |
| Static files not loading (CSS broken) | Nginx `root` vs `alias` misconfiguration | Corrected to `alias`; fixed `www-data` group permissions |
| Fake GSTIN on PDF exports | Hardcoded placeholder overriding `.env` | Removed hardcoded constants; `.env` is single source of truth |

**Redis Caching Impact**

Dashboard response time: **2118ms → 26ms** (98.8% reduction) via Redis-cached aggregations.

**CI/CD Pipeline**

Every push to `main` triggers GitHub Actions: install → migrate → run 60 pytest tests → report coverage. Dummy env vars in `ci.yml` for seamless pipeline runs.

### Tech Stack

![Django](https://img.shields.io/badge/Django%205.2-092E20?style=flat-square&logo=django&logoColor=white)
![Python](https://img.shields.io/badge/Python%203.11-3776AB?style=flat-square&logo=python&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL%2018-336791?style=flat-square&logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-009639?style=flat-square&logo=nginx&logoColor=white)
![Gunicorn](https://img.shields.io/badge/Gunicorn-499848?style=flat-square&logo=gunicorn&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu%2026.04-E95420?style=flat-square&logo=ubuntu&logoColor=white)
![Hetzner](https://img.shields.io/badge/Hetzner%20VPS-D50C2D?style=flat-square&logo=hetzner&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)
![DRF](https://img.shields.io/badge/Django%20REST%20Framework-ff1709?style=flat-square&logo=django&logoColor=white)
![Swagger](https://img.shields.io/badge/Swagger%20OpenAPI%203.0-85EA2D?style=flat-square&logo=swagger&logoColor=black)
![JWT](https://img.shields.io/badge/JWT%20Auth-000000?style=flat-square&logo=jsonwebtokens&logoColor=white)
![pytest](https://img.shields.io/badge/pytest-0A9EDC?style=flat-square&logo=pytest&logoColor=white)

<br/>

---

## 🛠️ Technical Skills

### Backend Engineering
![Django](https://img.shields.io/badge/Django-092E20?style=flat-square&logo=django&logoColor=white)
![DRF](https://img.shields.io/badge/Django%20REST%20Framework-ff1709?style=flat-square&logo=django&logoColor=white)
![JWT](https://img.shields.io/badge/JWT%20Auth-000000?style=flat-square&logo=jsonwebtokens&logoColor=white)
![Swagger](https://img.shields.io/badge/Swagger%20OpenAPI-85EA2D?style=flat-square&logo=swagger&logoColor=black)
![RBAC](https://img.shields.io/badge/RBAC%20Systems-6e40c9?style=flat-square&logoColor=white)

### Languages
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![C++](https://img.shields.io/badge/C++-00599C?style=flat-square&logo=cplusplus&logoColor=white)
![Java](https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white)

### Databases
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=flat-square&logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)

### Infrastructure & DevOps
![Linux](https://img.shields.io/badge/Linux%20%2F%20Ubuntu-FCC624?style=flat-square&logo=linux&logoColor=black)
![Nginx](https://img.shields.io/badge/Nginx-009639?style=flat-square&logo=nginx&logoColor=white)
![Gunicorn](https://img.shields.io/badge/Gunicorn-499848?style=flat-square&logo=gunicorn&logoColor=white)
![Hetzner](https://img.shields.io/badge/Hetzner%20VPS-D50C2D?style=flat-square&logo=hetzner&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)
![Certbot](https://img.shields.io/badge/Certbot%20SSL-003A70?style=flat-square&logo=letsencrypt&logoColor=white)

### Testing & Quality
![pytest](https://img.shields.io/badge/pytest-0A9EDC?style=flat-square&logo=pytest&logoColor=white)
![Coverage](https://img.shields.io/badge/Coverage%20Tracking-brightgreen?style=flat-square)
![CI/CD](https://img.shields.io/badge/CI%2FCD%20on%20every%20push-2088FF?style=flat-square&logo=githubactions&logoColor=white)

<br/>

---

## 🚀 Other Projects

### URL Shortener API *(In Progress)*

[![Repo](https://img.shields.io/badge/View%20Repo-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/Subham-Singh-Dev/url-shortener-api)

REST API built around Redis-first performance. Redis-backed redirect caching + click analytics. IP-level rate limiting (10 shortens/IP/hour via Redis). JWT user management.

**Stack:** Django · DRF · PostgreSQL · Redis · Docker · Railway

---

### SwiftRideLLD — Ride-Sharing Low-Level Design *(In Progress)*

[![Repo](https://img.shields.io/badge/View%20Repo-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/Subham-Singh-Dev/SwiftRideLLD)

In-memory ride-sharing platform in C++ demonstrating production-grade LLD. Pluggable driver matching strategies (`NearestDriver` / `BestRatedDriver`) swappable at runtime. Full ride lifecycle state machine. Decorator-based fare calculation.

**Patterns:** Strategy · Factory · Singleton · Observer · Decorator

<br/>

---

## 📊 GitHub Stats

<div align="center">

<img height="175em" src="https://github-readme-stats.vercel.app/api?username=Subham-Singh-Dev&show_icons=true&theme=github_dark&include_all_commits=true&count_private=true&hide_border=true&bg_color=0d1117"/>
<img height="175em" src="https://github-readme-stats.vercel.app/api/top-langs/?username=Subham-Singh-Dev&layout=compact&langs_count=6&theme=github_dark&hide_border=true&bg_color=0d1117"/>

</div>

<div align="center">

[![GitHub Streak](https://streak-stats.demolab.com?user=Subham-Singh-Dev&theme=github-dark-blue&hide_border=true&background=0d1117)](https://git.io/streak-stats)

</div>

<br/>

---

## 🧩 LeetCode

<div align="center">

[![LeetCode Stats](https://leetcard.jacoblin.cool/Sshubham_singh?theme=dark&font=Fira%20Code&ext=heatmap)](https://leetcode.com/Sshubham_singh)

</div>

**121 problems solved** — strong in Arrays, Strings, Linked Lists, Binary Search, Recursion.

<br/>

---

## 📌 What Sets My Work Apart

**Deployed, not just developed.** CWMS runs on a Hetzner VPS — Ubuntu, Nginx, Gunicorn, Certbot-managed SSL, systemd service files, Unix socket IPC. I've navigated production failure modes that don't appear in tutorials: Nginx `alias` vs `root` bugs, SSL redirect loops behind reverse proxies, PostgreSQL 15+ schema permission changes.

**Security built in from day one.** RBAC with 3 tiers. IDOR protection via scoped DB queries. CSRF hardening. Audit logs that record actor, IP, and timestamp on every financial action. JWT for API clients, session auth for the portal.

**Concurrency-aware payroll.** `transaction.atomic()` + `select_for_update()` with FIFO advance deduction. 100–500+ concurrent workers without a single race condition.

**APIs that document themselves.** Swagger/OpenAPI 3.0 on every project — no guesswork for API consumers.

**Tested and tracked.** 60 pytest tests. Coverage reporting. CI pipeline on every push to `main`.

<br/>

---

<div align="center">

*Backend engineer — open to internships and full-time roles*

[subhamsinghraigarh@gmail.com](mailto:subhamsinghraigarh@gmail.com) · [LinkedIn](https://linkedin.com/in/shubham-singh-dev)

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0d1117,50:1a2744,100:0d1117&height=100&section=footer" width="100%"/>

</div>
