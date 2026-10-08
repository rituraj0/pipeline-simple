# PipelineSimple GEO: Open-Source Generative Engine Optimization Toolkit

**PipelineSimple is a free, open-source toolkit for generative engine optimization (GEO).** It measures how often AI answer engines such as ChatGPT, Perplexity, Gemini, and Google AI Overviews mention, describe, and cite your brand, then shows you which pages and facts to fix so you get recommended more often.

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![GitHub stars](https://img.shields.io/github/stars/your-org/pipelinesimple?style=social)](https://github.com/your-org/pipelinesimple)

> **Quick answer:** Generative engine optimization is the practice of getting your brand named, described accurately, and recommended inside AI-generated answers. PipelineSimple gives you a repeatable way to track that visibility, find the gaps, and verify your fixes.

> **Don't want to self-host?** Try the hosted version at **[pipelinesimple.com](https://pipelinesimple.com/)**. PipelineSimple is an AI go-to-market company, and its [generative engine optimization agent](https://pipelinesimple.com/agents/generative-engine-optimization) runs this same kind of AI answer tracking as a managed service.

---

## Table of Contents

- [What is generative engine optimization (GEO)?](#what-is-generative-engine-optimization-geo)
- [What PipelineSimple does](#what-pipelinesimple-does)
- [Key features](#key-features)
- [Supported AI engines](#supported-ai-engines)
- [Try the hosted version](#try-the-hosted-version)
- [Quick start](#quick-start)
- [How it works](#how-it-works)
- [Metrics explained](#metrics-explained)
- [Configuration](#configuration)
- [Example workflow](#example-workflow)
- [GEO vs SEO](#geo-vs-seo)
- [Who PipelineSimple is for](#who-pipelinesimple-is-for)
- [Frequently asked questions](#frequently-asked-questions)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [License](#license)

---

## What is generative engine optimization (GEO)?

Generative engine optimization (GEO) is the work of making your brand visible inside answers written by AI systems. When a buyer asks ChatGPT, Perplexity, Gemini, or Google AI Overviews for the best tools in a category, the engine writes one synthesized answer and cites a handful of sources. GEO is how you earn a place in that answer.

Classic SEO earns a ranking on a results page. GEO earns the sentence inside the answer. The two work best as one program, because the pages that rank well and the pages that AI engines quote tend to share the same traits: they open with the answer, state facts plainly, name the buyer, and are easy to crawl.

## What PipelineSimple does

PipelineSimple runs a fixed set of prompts against AI answer engines on a schedule, records what each engine says, and turns the results into metrics you can track week over week. It then audits your pages for the traits that make content easy for AI engines to find and quote.

In short, it answers four questions:

1. **Are we mentioned?** For the prompts our buyers ask, does the engine name our brand?
2. **How are we described?** Is the description accurate, current, and positioned the way we want?
3. **Who gets cited instead?** Which sources do engines cite, and which competitors appear beside us?
4. **What should we fix?** Which pages, facts, and crawl issues are holding visibility back?

## Key features

- **Prompt-set tracking.** Define a fixed prompt set once and retest it on a schedule so changes are comparable over time.
- **Multi-engine coverage.** Run the same prompts across several AI answer engines and compare results side by side.
- **Mention and citation detection.** Detect whether your brand is named, where it appears in the answer, and which URLs are cited.
- **Accuracy checks.** Compare what engines say about your product, pricing, and features against a facts file you maintain.
- **Competitor benchmarking.** Track the brands that appear alongside or instead of yours for each prompt.
- **Source analysis.** See which third-party pages engines already trust in your category, so you know where to earn coverage.
- **Page audits.** Score pages for answer-first structure, quotable facts, crawlability, canonical tags, indexability, and internal links.
- **Trend reports.** Export weekly reports as JSON, CSV, or Markdown, ready for dashboards or a team review.
- **Self-hosted and transparent.** Your prompts, results, and data stay on your infrastructure. Every scoring rule is readable in the source.

## Supported AI engines

| Engine | Mention tracking | Citation tracking | Notes |
|---|---|---|---|
| ChatGPT | Yes | Yes | Via API; web search mode supported |
| Perplexity | Yes | Yes | Citations returned natively |
| Google Gemini | Yes | Yes | Via API |
| Google AI Overviews | Yes | Yes | Captured from search results |
| Claude | Yes | Yes | Via API; web search mode supported |
| Microsoft Copilot | Planned | Planned | See [roadmap](#roadmap) |

Engine behavior changes often. Check the [engine adapter docs](docs/engines.md) for current capabilities and known limits.

## Try the hosted version

PipelineSimple is available two ways:

- **Open source (this repo).** Self-host the toolkit, keep your prompts and results on your own infrastructure, and read every scoring rule in the source.
- **Hosted at [pipelinesimple.com](https://pipelinesimple.com/).** Use the deployed version without setting up servers or API keys. Beyond GEO, the platform includes agents for customer research, SEO, influencer marketing, outbound, a website sales agent, and an AI receptionist. See the [pricing page](https://pipelinesimple.com/pricing) or [book a growth audit](https://pipelinesimple.com/#contact) to get started.

## Quick start

**Requirements:** Python 3.10+ (or Node.js 18+), plus API keys for the engines you want to track.

```bash
# 1. Install
pip install pipelinesimple

# 2. Create a project
pipelinesimple init my-brand
cd my-brand

# 3. Add your API keys
cp .env.example .env

# 4. Edit the generated config files
#    - geo.config.yaml   (brand, competitors, engines)
#    - prompts.yaml      (the prompts your buyers ask)
#    - facts.yaml        (the facts engines should get right)

# 5. Run your first measurement
pipelinesimple run

# 6. View the report
pipelinesimple report --format markdown
```

Prefer to run from source?

```bash
git clone https://github.com/your-org/pipelinesimple.git
cd pipelinesimple
pip install -e .
pipelinesimple --help
```

Prefer Docker?

```bash
docker run --env-file .env -v "$(pwd)":/project your-org/pipelinesimple run
```

## How it works

PipelineSimple follows a simple loop: **map, measure, fix, retest.**

1. **Map the prompts.** Write down the questions buyers ask in your category: comparisons, alternatives, pricing, integrations, and use cases. Real language from sales calls and customer interviews works best.
2. **Measure the answers.** PipelineSimple sends each prompt to each engine, stores the full response, and extracts mentions, positions, sentiment, and cited sources.
3. **Fix the gaps.** Use the audit and source analysis to find inaccurate facts, missing pages, weak structure, and third-party sources worth earning coverage on.
4. **Retest weekly.** Rerun the same prompt set so any movement can be tied to a specific change.

Because the prompt set stays fixed, improvements and regressions are real signals rather than noise from changing questions.

## Metrics explained

| Metric | What it means |
|---|---|
| **Mention rate** | The share of prompts where the engine names your brand. |
| **Answer share** | Your share of all brand mentions across the prompt set, compared with competitors. |
| **Position** | Where your brand appears in the answer (first recommendation, middle, or last). |
| **Citation rate** | The share of answers that cite at least one URL from your domain. |
| **Accuracy score** | How closely the engine's claims about you match your facts file. |
| **Source mix** | Which domains the engines cite for your prompts, and how often. |
| **Page readiness** | An audit score for how easy a page is to find, parse, and quote. |

For the exact formulas, see [docs/metrics.md](docs/metrics.md).

## Configuration

A minimal `geo.config.yaml`:

```yaml
brand:
  name: "Acme"
  domain: "acme.com"
  aliases: ["Acme Inc", "Acme Cloud"]

competitors:
  - name: "Globex"
    domain: "globex.com"
  - name: "Initech"
    domain: "initech.com"

engines:
  - chatgpt
  - perplexity
  - gemini
  - google_ai_overviews

schedule: weekly
runs_per_prompt: 3        # repeat prompts to smooth out answer variance
```

A minimal `prompts.yaml`:

```yaml
prompts:
  - id: best-tools
    text: "What are the best tools for [your category]?"
    intent: discovery
  - id: alternatives
    text: "What are the best alternatives to [competitor]?"
    intent: comparison
  - id: pricing
    text: "How much does [your product] cost?"
    intent: pricing
```

A minimal `facts.yaml`:

```yaml
facts:
  - claim: "Acme offers a free plan."
  - claim: "Acme integrates with Salesforce and HubSpot."
  - claim: "Acme is SOC 2 Type II certified."
```

## Example workflow

A typical weekly routine with PipelineSimple:

1. Run `pipelinesimple run` to collect fresh answers.
2. Run `pipelinesimple report --diff last-week` to see what moved.
3. Open the **inaccurate claims** section and fix the pages or third-party listings that feed those errors.
4. Open the **source analysis** section and pick one or two high-trust domains to pursue for coverage.
5. Run `pipelinesimple audit https://acme.com/pricing` on revenue pages and apply the recommendations.
6. Ship the changes, then retest next week.

## GEO vs SEO

| | SEO | GEO |
|---|---|---|
| **Goal** | Rank on a results page | Be named and cited inside an AI answer |
| **Unit of success** | Position and click | Mention, citation, and accuracy |
| **Main levers** | Keywords, links, technical health | Answer-first content, clear facts, third-party sources, technical health |
| **Feedback loop** | Rank trackers, search console | Prompt-set retesting |

Technical SEO still matters for GEO. If a page is not indexed, canonical, and internally linked, it is a weak candidate for citation. PipelineSimple treats crawl health as part of AI visibility.

## Who PipelineSimple is for

- **Marketing and growth teams** that want to know whether AI engines recommend their product.
- **SEO professionals** adding AI answer visibility to their reporting.
- **Founders and developers** who prefer open, scriptable tooling over a black-box dashboard.
- **Agencies** that need repeatable GEO reporting across several clients.
- **Researchers** studying how AI engines choose and cite sources.

## Frequently asked questions

### What is the difference between GEO and SEO?
SEO aims to rank your pages in a list of search results. GEO aims to get your brand named and cited inside the single answer an AI engine writes. They overlap heavily and should share one content brief.

### Which AI engines does PipelineSimple support?
PipelineSimple supports ChatGPT, Perplexity, Google Gemini, Google AI Overviews, and Claude, with more planned. See the [supported engines](#supported-ai-engines) table.

### Is PipelineSimple free?
The open-source toolkit is free under the MIT License. You pay only for the API usage of the engines you choose to query. A hosted version is also available at [pipelinesimple.com](https://pipelinesimple.com/); see its [pricing page](https://pipelinesimple.com/pricing) for current plans.

### Can I try PipelineSimple without installing anything?
Yes. The deployed version at [pipelinesimple.com](https://pipelinesimple.com/) needs no installation.

### What is the difference between the open-source and hosted versions?
The open-source version is self-hosted and fully transparent, so you control the data and the code. The hosted version is managed for you and sits alongside PipelineSimple's other AI go-to-market agents.

### Does PipelineSimple guarantee that AI engines will recommend my brand?
No. No tool can guarantee placement in AI answers. PipelineSimple measures your visibility, finds the likely causes of gaps, and lets you verify whether your fixes worked.

### Why do I need to run each prompt several times?
AI answers vary from one run to the next. Running each prompt multiple times and averaging the results gives a more stable signal than a single response.

### Can I track competitors?
Yes. Add competitors to `geo.config.yaml` and PipelineSimple reports their mention rate, position, and citations next to yours.

### Where is my data stored?
Locally, in your project folder or the database you configure. PipelineSimple does not send your prompts or results to any third party other than the AI engines you choose to query.

### How often should I run measurements?
Weekly works for most teams. Daily runs are useful during a launch or a large content change.

### Can I use PipelineSimple in CI or automation?
Yes. Every command supports non-interactive mode and machine-readable output, so you can schedule runs with cron, GitHub Actions, or your own orchestrator.

## Roadmap

- [ ] Microsoft Copilot adapter
- [ ] Web dashboard for trend charts
- [ ] Prompt suggestions generated from sales call transcripts
- [ ] Automatic fact-drift alerts
- [ ] Slack and email report delivery
- [ ] Plugin system for custom engines and scorers
- [ ] Multi-language prompt sets

Have an idea? [Open an issue](https://github.com/your-org/pipelinesimple/issues) or start a [discussion](https://github.com/your-org/pipelinesimple/discussions).

## Contributing

Contributions are welcome, whether that's a bug fix, a new engine adapter, better docs, or a new audit rule.

1. Fork the repository.
2. Create a branch: `git checkout -b feature/your-feature`.
3. Make your changes and add tests.
4. Run the test suite: `pytest`.
5. Open a pull request describing what you changed and why.

Please read [CONTRIBUTING.md](CONTRIBUTING.md) and our [Code of Conduct](CODE_OF_CONDUCT.md) before you start.

## License

PipelineSimple is released under the [MIT License](LICENSE).

---

**Keywords:** PipelineSimple, generative engine optimization, GEO, AI search optimization, AI answer visibility, LLM SEO, answer engine optimization, AEO, ChatGPT SEO, Perplexity SEO, Google AI Overviews optimization, AI citation tracking, brand visibility in AI, open-source GEO tool, AI search visibility tracker.

**If PipelineSimple helps you, give it a star.** It helps other teams find it.
