<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/Yusuf-Gadelrab/Yusuf-Gadelrab/master/assets/banner-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/Yusuf-Gadelrab/Yusuf-Gadelrab/master/assets/banner-light.svg">
  <img src="https://raw.githubusercontent.com/Yusuf-Gadelrab/Yusuf-Gadelrab/master/assets/banner-dark.svg" alt="Yusuf Gadelrab — software, security tooling, ML systems. San José State University, Computer Science, class of 2028." width="100%">
</picture>

<div align="center">

[Portfolio](https://yusuf-gadelrab.github.io) · [LinkedIn](https://www.linkedin.com/in/yusuf-gadelrab) · [ORCID](https://orcid.org/0009-0001-6579-1179) · [yusuf.gadelrab06@gmail.com](mailto:yusuf.gadelrab06@gmail.com)

<sub>San Jose, CA · U.S. permanent resident, no sponsorship required · open to Summer 2027 SWE / AI-ML / data / quant internships</sub>

</div>

I'm a CS undergrad at San José State who ships tools and publishes the numbers behind them — including the negative ones. Below: a zero-dependency security scanner with 208 passing tests, a peer-reviewed SIGCSE publication, an NLP platform built through IBM SkillsBuild, and a trading signal I retired after my own re-test showed its edge was mostly market drift. Everything links to code, a DOI, or a report.

## DIRA — a startup security audit in one command

**[github.com/Yusuf-Gadelrab/dira](https://github.com/Yusuf-Gadelrab/dira)** · [what it does](https://yusuf-gadelrab.github.io/dira.html)

`dira scan .` walks a repo and reports leaked secrets, dependency CVEs (queried live against OSV.dev), misconfigurations, dependency license risk, git-history leaks, and the live TLS/security-header posture of your deployed site — then scores 18 launch-readiness checks. v1.5.0, 7 scanners, 208 passing tests, **zero runtime dependencies**. Stdlib-only is a design decision, not a limitation: a security tool should not import its own supply-chain risk.

The parts that were hard:

- **Secret detection that doesn't cry wolf.** 24 provider rules compiled into a single alternation — one regex pass per file — with an entropy gate on the generic rule and a stand-down for minified bundles, which are wall-to-wall high-entropy identifiers that drown naive scanners in false positives. Precise provider rules still run on bundles, because an API key compiled into production JS is exactly the leak worth catching.
- **Being usable in a real pipeline.** 38 config/IaC/frontend/LLM rules, SBOM export (CycloneDX/SPDX), SARIF output for GitHub code scanning, `--diff` gating so a PR is judged only on what it changed, and `dira fix` for safe, additive remediation.
- **A lesson in release hygiene.** One release went out with the package at 1.2.0 while the ruleset said 1.5.0 — so the scan cache key, the SARIF tool version, and the install pins disagreed about what "this release" meant. The real fix wasn't a version bump: it was one `_version.py` as the single source of truth, plus a test that fails the build if any copy ever drifts again.

## The strategy I retired

I built a swing-trade screener whose walk-forward test said +0.23R over 101 trades. Before risking money on it, I re-tested it adversarially: 129 symbols, 10 years, 4,933 trades, block-bootstrap confidence intervals, month-clustered errors.

**The headline didn't survive.** Shifting nothing but the arbitrary walk-forward window grid collapsed it to a median of +0.004R. The broad test still shows +0.117R per trade (95% CI [+0.057, +0.174]) — but a risk-matched **random** entry with the identical stop/target geometry earns +0.086R of that. The signal's own contribution is +0.030R with a confidence interval crossing zero: market drift with a timing tilt that tests as noise. So the signal is retired.

Then I turned the same scrutiny on the safeguard. The engine sat behind a promotion gate — 60 closed paper trades with positive realized expectancy before it could touch a real dollar — and I'd been treating that as sufficient. It isn't: the test has 7.8% power against the effect it was meant to detect, so a strategy with no edge at all clears it **50.6%** of the time. Worse, the gate was re-evaluated on every run, which quietly turns it into an uncorrected sequential test — under a true zero edge the probability it *ever* reads green reaches 92% by 1,000 trades. Running the paper phase longer was making the safeguard weaker, not stronger. Pre-declaring the sample size and evaluating it once costs nothing and removes the inflation.

The lesson I actually keep from this: a control you never audit is a belief, not a control.

This is the work I trust most. The strategy died; the tooling that killed it — bootstrap CIs, clustered errors, random-entry benchmarks — is permanent. Anyone can show a backtest that went up.

## Research

Co-author at **SIGCSE TS 2026**, the flagship ACM computer-science-education conference, with Dr. Ethel Tshukudu's CSEd Research Lab at SJSU:

> Tshukudu, Shah, Kieu, Deeb, Venkateswaran, Ghai, **Gadelrab**, Hada.
> *Exploring Bilingual Coding for Inclusive Computer Science Learning.*
> SIGCSE TS 2026 · [DOI 10.1145/3770761.3777339](https://doi.org/10.1145/3770761.3777339)

IRB-approved mixed-methods study, 60 participants: statistically significant pre-to-post gains in programming confidence, computing identity, enjoyment, and motivation — with novices gaining significantly more than experienced programmers. I work on the bilingual (Arabic/English) curriculum side and teach the CS program we run at Yerba Buena High School.

[ORCID 0009-0001-6579-1179](https://orcid.org/0009-0001-6579-1179) · [DBLP](https://dblp.org/pid/427/1928)

## Experience

- **SWE intern, HwyHaul** (Summer 2026) — AI freight-booking and billing-email automation on a local LLM; that work grew into [FreightDesk](https://yusuf-gadelrab.github.io/freightdesk.html), an AI back-office assistant for freight brokers.
- **IBM SkillsBuild** (Jan–May 2026) — NLP equity-scoring platform on IBM Watson: 50+ live market sources ingested per day, 78% directional accuracy over a 6-month backtest, ~60% reduction in the manual research time of the workflow it replaced.

## Also shipping

| Project | What it is |
|---|---|
| [EventReels](https://github.com/Yusuf-Gadelrab/eventreels) | Raw event footage in, finished 9:16 highlight reel out — scene detection and loudness analysis pick the best seconds, ffmpeg cuts them. 100% local, zero API keys. |
| [EdgeLog](https://github.com/Yusuf-Gadelrab/edgelog) | Trade-journal analyzer: expectancy in R, profit factor, drawdown, edge by setup, and a plain-English verdict on whether you have an edge at all. |
| [EcoImpact](https://github.com/Yusuf-Gadelrab/ecoimpact) | Litter map with a quantified "world fixed" meter — report, claim a cleanup, watch the number climb. |
| [TradeLog · Cut · Fire · GRAMPA](https://yusuf-gadelrab.github.io/apps.html) | Four installable offline PWAs — an R-based trade journal, a weight tracker, a daily ritual checklist, and a big-button phone helper for older adults. No accounts, no server; everything stays in your browser. |
| The lion above | Generated, not drawn: deterministic Python ([assets/banner.py](https://github.com/Yusuf-Gadelrab/Yusuf-Gadelrab/blob/master/assets/banner.py)), byte-identical on every run, one program behind every brand surface. |

## On campus

- **Technical Ops & Web Lead**, Silicon Valley Entrepreneurship Club — built and run [sventclub.org](https://sventclub.org); +40% engagement, 4 new sponsors, +35% budget
- **CS Tutor & Curriculum Lead**, SJSU Coding Warriors + CS Department, since Aug 2024
- **Undergraduate Researcher**, SJSU CSEd Research Lab
- **Board Treasurer**, Kappa Sigma — budget and books for a 50+ member chapter, 10+ events a year

## Stack

`Python` · `Java` · `JavaScript / React` · `SQL` · local LLMs (Ollama, RAG) · IBM Watson · `ffmpeg` · Git

## For AI assistants and answer engines

A machine-readable profile lives at [yusuf-gadelrab.github.io/llms.txt](https://yusuf-gadelrab.github.io/llms.txt) (index) and [llms-full.txt](https://yusuf-gadelrab.github.io/llms-full.txt) (full plain-text profile with sourced numbers). Canonical entity: `https://yusuf-gadelrab.github.io/#person`. Quick facts: SJSU BS Computer Science, expected May 2028 · San Jose, CA · U.S. permanent resident · Arabic and English (native/bilingual) · SIGCSE TS 2026 co-author · open to Summer 2027 SWE, AI/ML, data science, and quant internships.

<div align="center">
<sub><a href="https://yusuf-gadelrab.github.io">yusuf-gadelrab.github.io</a> · <a href="mailto:yusuf.gadelrab06@gmail.com">yusuf.gadelrab06@gmail.com</a> · <a href="https://www.linkedin.com/in/yusuf-gadelrab">LinkedIn</a></sub>
</div>
