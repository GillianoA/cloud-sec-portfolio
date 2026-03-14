---
title: "Case Study: Zero Trust Edge Architecture"
description: "Deploying a highly secure, automated portfolio infrastructure using Azure and Cloudflare WAF."
date: 2026-03-14
tags: ["Azure", "Cloudflare", "WAF", "CI/CD", "Zero Trust"]
ShowToc: true
---

## The Objective
To design and deploy a highly resilient, automated web infrastructure that completely obscures the origin compute layer and mitigates automated reconnaissance at the edge. 

Rather than relying on default vendor configurations, this deployment enforces a strict Zero Trust perimeter using a reverse proxy, strict SSL/TLS termination, and custom Web Application Firewall (WAF) rules.

---

## The Architecture
**[View the deployment pipeline and configuration on GitHub ↗](https://github.com/GillianoA/cloud-sec-portfolio)**

The infrastructure is decoupled into two distinct layers: **Compute/Hosting** and **Perimeter Security**.

1. **The Origin (Azure Static Web Apps):** The application is compiled statically via a native GitHub Actions CI/CD pipeline. The pipeline bypasses Azure's default black-box builder (Oryx) in favor of a deterministic, runner-based execution. 
2. **The Edge (Cloudflare):** Azure's origin IP and CNAME records are completely hidden behind Cloudflare's global edge network. Direct traffic to the Azure tenant is impossible.

---

## Threat Mitigation & WAF Configuration
A major vulnerability for any public-facing infrastructure is automated botnet reconnaissance. Attackers continuously scan domains for exposed `.env` files, `.git` repositories, or legacy login portals.

Instead of relying solely on reactive threat scoring, I engineered a proactive WAF rule to immediately drop this traffic at the edge, preserving origin bandwidth and eliminating the attack vector.

![Cloudflare WAF Rule blocking malicious probing](/images/waf-rule.png)
*Figure 1: Custom Cloudflare WAF rule deployed to block automated URI probing.*

### Security Controls Enforced:
* **Strict SSL/TLS:** Enforced at the edge, rejecting any HTTP downgrade attempts.
* **Origin Obfuscation:** The Azure tenant is shielded by Cloudflare's reverse proxy, preventing direct DDoS attacks against the compute layer.
* **Deterministic CI/CD:** The deployment pipeline utilizes `skip_app_build: true` to prevent vendor auto-builders from introducing unauthorized configuration drift.

---

## The Business Impact
This architecture demonstrates the ability to deploy enterprise-grade, highly secure infrastructure with near-zero overhead. By neutralizing threats at the DNS/Edge layer, the underlying Azure environment remains isolated, compliant and cost-efficient.