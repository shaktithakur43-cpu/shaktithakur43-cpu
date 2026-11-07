# Shakti Thakur

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:071A2C,45:0078D4,100:31D0AA&height=210&section=header&text=Shakti%20Thakur&fontSize=48&fontColor=FFFFFF&fontAlignY=38&desc=Azure%20DevOps%20%7C%20Cloud%20%7C%20AI%20%26%20AIOps&descSize=15&descAlignY=60&animation=fadeIn" alt="Shakti Thakur — Azure DevOps, Cloud, AI and AIOps" width="100%" />
</p>

<p align="center">
  <strong>Azure DevOps · Cloud Architecture · Engineering Operations</strong><br />
  Turning business needs into secure, repeatable, production-ready delivery.
</p>

<p align="center">
  <a href="#engineering-focus">Engineering focus</a> &nbsp;·&nbsp;
  <a href="#architecture-notes">Architecture notes</a> &nbsp;·&nbsp;
  <a href="#ai-ops">AI &amp; AIOps</a> &nbsp;·&nbsp;
  <a href="#leadership-and-portfolio">Leadership &amp; portfolio</a> &nbsp;·&nbsp;
  <a href="https://github.com/shaktithakur43-cpu">GitHub</a>
</p>

---

## Profile

I bring **10 years of IT experience**, including **5 years focused on Azure DevOps**. My focus is the full delivery path: cloud foundations, infrastructure as code, secure pipelines, production reliability, and the feedback that makes each release better.

> **Design for the people who build it, secure it, operate it, and recover it.**

### Engineering focus

| Platform & governance | Delivery engineering | Production operations |
| --- | --- | --- |
| Azure landing zones, Entra ID, policy, network architecture | Azure DevOps, CI/CD, Terraform, DevSecOps | Reliability, observability, disaster recovery, FinOps |

A good design connects business outcomes to practical infrastructure and application choices. That includes workload boundaries, monolith and microservice trade-offs, APIs, state and caching, messaging, and event-driven patterns.

## Architecture notes

<details>
<summary><strong>01 · Azure foundations, governance &amp; security</strong></summary>

### Cloud adoption

Microsoft's Cloud Adoption Framework organizes cloud adoption into connected methodologies: **Strategy → Plan → Ready → Adopt → Govern → Manage**. They are applied iteratively. Security spans the whole journey.

### Enterprise guardrails

- Organize the tenant and management groups around platform services, workload landing zones, and sandbox or decommissioned areas.
- Set subscription boundaries by environment, function, ownership, and blast-radius requirements.
- Apply Azure Policy initiatives at appropriate scopes; monitor compliance and document time-bound exemptions.
- Use Microsoft Entra ID, group-based RBAC, least privilege, Conditional Access, MFA, and just-in-time privileged access through PIM.
- Define controls from workload risk: secrets management, Defender for Cloud, NSGs/ASGs, firewalls, vulnerability checks, encryption and patch baselines, DDoS protection, and compliance benchmarks such as CIS or ISO 27001.

### Hub-and-spoke connectivity

```text
On-premises ── ExpressRoute / VPN ── Hub: gateway · firewall · DNS
                                          │
                                  peering · UDRs
                                     ┌────┴────┐
                                App spokes   Shared services
                              private links  runners · bastion
```

Plan IPAM/CIDRs to prevent overlap. Design traffic inspection, controlled ingress and egress, segmentation, private endpoints, and private DNS links around actual workload requirements. Application Gateway or Front Door with WAF can provide controlled ingress where appropriate.

</details>

<details>
<summary><strong>02 · Terraform, Azure Repos &amp; DevSecOps</strong></summary>

### Infrastructure as Code

```text
Format & validate → Lint & test → Security scan → Cost review
       → Plan & peer review → Approval as needed → Apply → Drift review
```

- Build reusable, parameterized Terraform modules with documented interfaces and semantic versioning.
- Use `terraform fmt`, validation, and linting such as TFLint; add tests and risk-appropriate checks such as Checkov or Trivy.
- Review cost impact with tools such as Infracost where useful.
- Store remote state in protected Azure Storage. Use the AzureRM backend's blob locking and consistency features, secure authentication, and least-privilege access.
- Review plans before production changes, keep secrets out of source and logs, and schedule drift checks such as `terraform plan -detailed-exitcode`.

### Source control and pipeline controls

Use short-lived branches and pull requests, protect production branches, prevent direct production pushes, and apply CODEOWNERS and reviewer requirements to match risk and separation of duties. Two reviewers can be a local policy; it is not a universal rule.

A YAML delivery path can cover validation and tests, secret scanning (for example, Gitleaks), IaC and vulnerability checks, build and plan artifacts, environment approvals, deployment, post-deployment checks, and a documented rollback or roll-forward plan. VM custom data or cloud-init can bootstrap baseline configuration and agents; never put secrets in startup scripts.

</details>

<details>
<summary><strong>03 · Cloud migration &amp; workload design</strong></summary>

### Reference migration scenario

**Architecture scenario from the preparation guide—not a claimed personal project:** migrating 100+ applications from on-premises to Azure across development, UAT, and production.

`Discover → Assess → Prepare → Migrate & validate → Cut over → Hypercare → Optimize`

- **Discover:** Inventory applications, dependencies, data, interfaces, compatibility, network capacity, workload criticality, and cost assumptions; use Azure Migrate where suitable.
- **Prepare:** Confirm target architecture and landing-zone readiness, identity, connectivity, backup/restore, migration waves, owners, and test/go-no-go plans.
- **Cut over:** Coordinate replication and final sync, DNS TTL and traffic changes, validation, communications, and rollback criteria.
- **Hypercare:** Monitor telemetry, user flows, performance, security, and cost; resolve issues and capture lessons. Set the support period to workload risk and service needs.

### Quality review

Assess designs against the five Azure Well-Architected pillars:

**Reliability · Security · Cost Optimization · Operational Excellence · Performance Efficiency**

A complementary checklist asks whether the solution is scalable, robust, portable where needed, governed, highly available, backed up and recoverable, compliant, and observable. These are design checks, not extra official pillars.

</details>

<details>
<summary><strong>04 · Reliability, FinOps &amp; service operations</strong></summary>

### Resilience and recovery

- Define workload-specific SLOs/SLIs, **RTO** (maximum acceptable recovery time), and **RPO** (maximum acceptable recovery point/data-loss window).
- Select availability zones, zone-spanning VM Scale Sets, backup, replication, and regional recovery such as Azure Site Recovery according to service objectives.
- Understand storage choices: **LRS** keeps replicas within a datacenter; **ZRS** replicates across availability zones in supported regions; **GRS** asynchronously replicates to a secondary region. GRS secondary data is not normally readable until failover. Validate service and region behavior; test recovery.

### FinOps

- Establish ownership, tagging, budgets, and cost visibility.
- Review idle compute, unattached disks, old snapshots, and unused public IPs; rightsize against observed usage.
- Evaluate Reservations or Azure Savings Plans for suitable steady usage; schedule non-production environments when appropriate.
- Review Azure Monitor and Log Analytics ingestion, retention, and Data Collection Rules for value and cost.

### Observability

Use Azure Monitor and Log Analytics for centralized platform visibility where appropriate. Tune Azure Monitor Agent collection through Data Collection Rules. Route actionable Azure Monitor Action Group alerts to configured Microsoft Teams, Slack, PagerDuty, or ticketing/on-call destinations. Replication alone does not prove recoverability; test restore and failover procedures.

</details>

## AI, AIOps &amp; intelligent automation

**Applied focus:** using AI to improve operational signal, engineering flow, and knowledge access—with human review, security, and measurable outcomes built in.

| Area | Practical DevOps use | Engineering guardrail |
| --- | --- | --- |
| AIOps incident triage | Correlate alert and log context; draft an investigation summary | Engineer verifies evidence before action |
| GenAI runbook assistant | Retrieve approved runbook guidance with source links | Respect access boundaries; ground answers in approved docs |
| AI-assisted IaC review | Highlight risky Terraform or pipeline changes for reviewers | No autonomous production apply; keep PR approval |
| MLOps foundations | Version models and data; monitor quality, drift, and deployment health | Define ownership, evaluation, rollback, and audit trail |

These are architecture and portfolio focus areas; project links and implementation claims will be added when the corresponding work is published.

## Leadership and portfolio

Senior engineering connects sound architecture with clear ownership and reliable delivery:

- **Career landscape:** Sales, Pre-Sales, Technical Account Management, Enterprise Architecture, and Technical Leadership are adjacent tracks—not roles I am claiming to have held.
- **Technical leadership:** Architecture and IaC reviews, technical direction, mentoring, onboarding, knowledge transfer, and team upskilling.
- **Delivery governance:** RACI and escalation paths, incident retrospectives, SOPs, service reviews, and architecture compliance.
- **Vendor management:** RFI/RFP input, technical evaluation criteria, SOW scope and acceptance evidence, SLA tracking, milestones, and transition plans.
- **Portfolio:** Reusable Terraform modules, DevSecOps pipeline templates, reference architectures, ADRs, technical articles, and case studies with verifiable outcomes.

**Metrics belong in a profile only when they are real and explainable.** “100+ workloads” and “28% cost reduction” came from examples in the supplied guide, so they are not presented here as personal results.

<details>
<summary><strong>Reference documentation</strong></summary>

- [Microsoft Cloud Adoption Framework](https://learn.microsoft.com/azure/cloud-adoption-framework/)
- [Azure Well-Architected Framework](https://learn.microsoft.com/azure/well-architected/pillars)
- [Terraform AzureRM backend](https://developer.hashicorp.com/terraform/language/backend/azurerm)

</details>

<p align="center">
  <em>Align to the business. Automate with care. Design for operations.</em><br />
  <a href="https://github.com/shaktithakur43-cpu">github.com/shaktithakur43-cpu</a>
</p>
