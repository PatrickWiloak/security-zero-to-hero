<!--
  Site-only landing page. Rendered over the staged copy of README.md by
  .github/scripts/build-site.py; the repo's own README.md is never touched.

  The two pages have different jobs. README.md is a repo front page: badges,
  repository structure, contributing, "star this repo". This is a website
  landing page: what the site is, who it is for, and the four or five links a
  first-time visitor actually needs.

  Never hard-code a count here. Every number is a double-braced token filled from
  docs/certs.json and from check-readme-counts.py's gather(), which is the same
  counting code CI runs against the README - so a number on this page cannot
  drift away from the tree. Adding a new number means adding a token, not
  typing a figure.

  No `hide: toc` here. With toc.integrate the page's headings fold into the left
  sidebar, and hiding them would make Home the one page whose sections do not
  appear where every other page's do.
-->
<!-- markdownlint-disable MD030 -->
<!-- Material's card grids use `-   ` (three spaces) so the card body lines up at
     a four-space indent and stays part of the list item. MD030 wants one. -->


<div class="home-hero" markdown>

# Security, from zero to hero { .home-title }

<p class="home-intro">A plain-English path from zero to security engineer, plus study guides for the security certifications employers ask for - free, no signup, nothing gated.</p>

<p class="home-sub">Never thought about security before, or chasing your CISSP - both start here. Press <kbd>/</kbd> to search all {{words}} words.</p>

[Start Security from Scratch](learn/security-from-scratch.md){ .md-button .md-button--primary }
[Browse {{certifications}} certifications](STUDY-HUB.md){ .md-button }
[Compliance guides](resources/compliance-guides/){ .md-button }

<div class="stat-strip" markdown>

- **{{certifications}}** certifications
- **{{providers}}** providers
- **{{words}}** words
- **{{doc_links}}** vendor doc links
- **{{compliance_guides}}** compliance guides

</div>

</div>

<p class="home-kicker">The four pillars</p>

## Four ways in

<div class="grid cards" markdown>

-   :material-book-open-variant:{ .lg .middle } **Learn**

    ---

    Plain English, no exam scaffolding. [Security from Scratch](learn/security-from-scratch.md) takes you from zero to security engineer in seven phases, with {{concept_pages}} concept pages on identity and MFA, encryption, network and application security, threat modeling, detection and incident response.

    [:octicons-arrow-right-24: Start learning](learn/)

-   :material-hammer-wrench:{ .lg .middle } **Build**

    ---

    Defensive builds with inline commands: zero trust on AWS, Azure and GCP, centralized cloud audit logging with tested alerts, and a hardened Linux server. Plus the zero trust architecture pattern and a map of which lab backs which exam.

    [:octicons-arrow-right-24: Build something](resources/hands-on-projects/)

-   :material-certificate-outline:{ .lg .middle } **Certify**

    ---

    {{certifications}} security cert guides across {{providers}} providers - CISSP, Security+, CCSP, CySA+, CISM, OSCP and the cloud security exams - each with a fact sheet, practice plan, scenarios and a practice question bank.

    [:octicons-arrow-right-24: Find your cert](STUDY-HUB.md)

-   :material-book-search-outline:{ .lg .middle } **Reference**

    ---

    {{compliance_guides}} compliance guides (SOC 2, ISO 27001, NIST CSF, HIPAA, PCI DSS, GDPR, FedRAMP, NIS2, DORA, CMMC), {{service_comparisons}} security and identity service comparisons, the security engineer roadmap and interview prep.

    [:octicons-arrow-right-24: Browse reference](resources/)

</div>

<p class="home-kicker">Quick links</p>

## Jump to what you need

<div class="home-links" markdown>

- [Security from Scratch](learn/security-from-scratch.md) - the path from zero to security engineer
- [Concepts](learn/concepts/) - five-minute explainers, one idea each
- [Topic indexes](topics/) - security and identity, tied across all four pillars
- [Glossary](learn/glossary.md) - the vocabulary, defined once
- [Security Engineer roadmap](resources/certification-roadmap-security-engineer.md) - which certs, in which order
- [Compliance guides](resources/compliance-guides/) - SOC 2, ISO 27001, NIST CSF, HIPAA, PCI DSS, GDPR, FedRAMP, NIS2, DORA, CMMC
- [Zero trust, hands-on](resources/hands-on-projects/implement-zero-trust.md) - identity, MFA and per-request access
- [Practice questions](resources/practice-questions/) - scenario banks with explained answers
- [Interview prep](resources/interview-prep/security-engineer-interview.md) - the security engineer interview
- [Freshness ledger](docs/freshness.md) - what was last verified, and when

</div>

<p class="home-kicker">The library</p>

## Certifications by provider

<div class="provider-grid" markdown>

{{provider_chips}}

</div>

[Full per-provider breakdown](STUDY-HUB.md#-certifications-by-provider){ .md-button }

## What's new

{{whats_new}}

<p class="home-kicker">The family</p>

## More Zero to Hero

<div class="grid cards" markdown>

-   :material-cloud-outline:{ .lg .middle } **Cloud Zero to Hero**

    ---

    Cloud from the first terminal command: AWS, Azure, GCP, Kubernetes, Terraform and DevOps.

    [:octicons-arrow-right-24: cloud.noblerworks.com](https://cloud.noblerworks.com/)

-   :material-database-outline:{ .lg .middle } **Data Zero to Hero**

    ---

    Databases, pipelines, warehouses, lakehouses and streaming, plus the data certifications.

    [:octicons-arrow-right-24: data.noblerworks.com](https://data.noblerworks.com/)

-   :material-robot-outline:{ .lg .middle } **AI Zero to Hero**

    ---

    Learn AI, use it at work, build with it, and secure and govern it - including prompt injection and agent security.

    [:octicons-arrow-right-24: ai.noblerworks.com](https://ai.noblerworks.com/)

</div>

All four are free, by Nobler Works.

## Who made this

Built by **[Patrick Wiloak](https://patricklukewilson.com)** - ex-AWS Solutions Architect, 10 years in tech, multi-cloud certified.
[YouTube](https://youtube.com/@patrickwiloak) · [LinkedIn](https://www.linkedin.com/in/patricklukewilson/) · [Website](https://patricklukewilson.com) · [Source on GitHub](https://github.com/PatrickWiloak/security-zero-to-hero)

We build custom software and products at **[Nobler Works](https://noblerworks.com/)**. Open-source training like this is how we give back - we are nothing without the community that supports us. If you need software built, [get in touch](https://noblerworks.com/).

!!! tip "Want the reps as well as the material?"

    [![gitGood.dev - practice questions, coding challenges, system design and cloud certification practice exams for engineers, data, security, DevOps and product technologists](assets/brand/gitgood-banner.png){ width="300" }](https://gitgood.dev)

    This site gives you the material. **[gitGood](https://gitgood.dev)** gives you the reps, and tells you whether you actually know it. Built for every kind of technologist across 21 role-targeted learning paths - engineering, SRE and DevOps, cloud architecture, security, ML and AI, data science, analytics and engineering, QA, product and TPM, and new grads breaking in.

    1,950+ practice questions across 34 categories · certification practice exams for AWS CLF-C02, SAA-C03 and DVA-C02, Azure AZ-900, AZ-104, AZ-305 and AI-900, Google Cloud Digital Leader and Associate Cloud Engineer, Kubernetes CKA and CKAD, CompTIA Security+ and HashiCorp Terraform Associate - original scenario questions, never brain dumps, with per-domain scoring and a timed simulator · coding challenges · SQL playground · system design walkthroughs · AI mock interviews · AI resume reviews · salary coaching · live job-market pulse.

    A 7-day free trial, then $8/month or $64/year. The free tier needs no card.

## Fine print

Free for educational use with attribution. Every technical claim links to the vendor's own documentation - {{doc_links}} links across the site.

This is an independent educational resource. It is not affiliated with, endorsed by, or sponsored by ISC2, ISACA, CompTIA, AWS, Microsoft, Google, or any other vendor referenced. All trademarks belong to their respective owners.

Found something wrong or out of date? [Contributions welcome](CONTRIBUTING.md).
