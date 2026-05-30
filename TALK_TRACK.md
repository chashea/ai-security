# AI Security Architecture — Customer Talk Track

A guided walkthrough of the **AI Security Architecture** site
(<https://chashea.github.io/ai-security/>) for customer conversations.
Designed for a 20–30 minute briefing with a technical-ish audience
(CISO, security architect, AI platform owner). Adjust depth as needed.

---

## 0. Pre-flight (30 seconds, before sharing screen)

> "Before I open this up — quick context. What we're about to look at isn't
> a product pitch. It's a **reference architecture** for how Microsoft's
> existing security stack — Defender, Purview, Entra, Defender for Cloud,
> and Microsoft Agent 365 governance capabilities where available —
> combine to secure AI workloads, agents, and the data flowing through them.
>
> My goal is that by the end of this, you can point at any AI risk on your
> roadmap — Copilot, custom agents, third-party models, shadow AI — and
> know exactly which products own which part of the answer."

---

## 1. The opening frame — "Securing the AI Attack Surface" (2 min)

**Land on the hero.**

> "AI didn't introduce a new security category — it stretched every
> existing one. Identity now includes non-human agent identities. Data
> protection now has to follow prompts, grounding sources, and model
> outputs. Posture management now covers model endpoints and training
> data. And detection has to correlate signals that originate in a chat
> box, a SharePoint site, and a service principal — often within the
> same incident.
>
> What this page does is show that **you don't need a new AI security
> product** for most of these problems. You need the products you likely
> already own, configured for AI workloads, and connected so signals flow
> between them."

**Key message:** *defense in depth, not a new silo.*

---

## 2. The hub-and-spoke diagram (3 min)

**Click into the diagram.** Walk the five pillars in this order — it
mirrors the logical flow of an AI request.

| Pillar | One-line pitch for customers |
|---|---|
| **Entra** | "Who — and what — is allowed to talk to the model." Identity for humans *and* agents, Conditional Access for AI apps, CIEM to right-size service principals. |
| **Defender for Cloud** | "Is the AI infrastructure itself safe?" Posture (CSPM) for AOAI / Foundry, attack-path analysis, runtime threat protection, Content Safety. |
| **Purview** | "What data is going in and coming out?" DSPM for AI, DLP for Copilot and supported AI apps, sensitivity labels and permission-trimmed grounding, insider risk. |
| **Defender XDR** | "When something happens, who sees the whole picture?" Unified incident graph, MDCA for shadow AI discovery, AIR, Security Copilot. |
| **Agent 365** | "Governance for supported agents themselves." Inventory, ownership, access review, topology context, and connector-dependent security signals. |

> "Notice what's in the middle — **AI Workloads**. Every pillar contributes
> a different kind of signal about that workload, and they all land in
> the same incident graph. That's the architectural point."

---

## 3. Make it real — the threat scenarios (8–10 min)

This is the most persuasive part of the deck. Pick **two scenarios** that
match the customer's anxiety. Suggested pairings:

| If the customer is worried about… | Walk through… |
|---|---|
| Employees using ChatGPT / Claude with company data | **Shadow AI Data Leak** |
| Their custom agents on Foundry or Copilot Studio | **Prompt Injection** + **Rogue Agent** |
| Copilot rollout and oversharing | **Overshared Data via Copilot** |
| Cloud identity / service principal sprawl | **Compromised AI Agent Identity** |

**For each scenario, narrate the 4 steps using this pattern:**

1. **What happened** (the user / attacker action)
2. **Which product caught it** (and *why* that product is positioned to)
3. **What signal it produced**
4. **How the next product in the chain acted on that signal**

### Example narration — Prompt Injection

> "An attacker hides instructions inside a document that a Foundry agent
> ingests through a grounding connector. Four things happen as the signal
> chain develops:
>
> 1. **Azure AI Content Safety** sees the injection pattern at the model
>    boundary — that's prevention where Prompt Shields are enabled.
> 2. **Defender for Cloud** can raise a supported AI-service alert, such as
>    a Prompt Shields jailbreak alert for Foundry agents — that's detection.
> 3. **Defender XDR** joins that alert to sign-in logs and prior
>    reconnaissance signals where those logs are available — that's correlation.
> 4. **Entra Conditional Access and Continuous Access Evaluation** can revoke
>    sessions or require stronger authentication based on configured policy —
>    that's response.
>
> Four products, one incident, no analyst pivoting between consoles."

**Repeat the pattern for the second scenario.** The customer should walk
away able to say *"detect → correlate → contain"* in their own words.

---

## 4. The implementation roadmap (3 min)

**Click into the roadmap.** This is where you take the conversation from
"interesting architecture" to "what would we actually do Monday."

> "We don't recommend boiling the ocean. The phased rollout looks like
> this:"

- **Phase 1 — Weeks 1–2: Discover & Assess.** Turn on Purview DSPM for AI,
  run Defender for Cloud CSPM against your AI resources, audit
  permissions with CIEM, and inventory supported agents in Agent 365 or
  the appropriate admin center. *Outcome: you have a baseline.*
- **Phase 2 — Weeks 3–4: Classify & Protect.** Deploy DLP for Copilot,
  Conditional Access policies for AI apps, sensitivity labels on
  grounding data, and least-privilege access for supported agent identities.
  *Outcome: the easy wins are live.*
- **Phase 3 — Month 2: Detect & Respond.** Detection rules in XDR, DfC AI
  threat protection, automated investigation, Security Copilot. *Outcome:
  the SOC is in the loop.*
- **Phase 4 — Ongoing: Harden & Govern.** CIEM right-sizing, attack-path
  remediation, insider risk tuning, supported agent topology reviews,
  workload identity federation. *Outcome: this becomes operational, not a project.*

> "Most customers see meaningful posture improvement by the end of
> Phase 2 — typically inside a month."

---

## 5. The close (2 min)

Pick the close that matches the audience.

**For the CISO / executive:**
> "The takeaway I'd leave you with: AI security isn't a product purchase
> decision, it's a configuration and integration decision against tools
> you likely already license. The biggest risk isn't that any single one
> of these capabilities is missing — it's that they're not turned on or
> not connected. This architecture is the connection map."

**For the architect / platform owner:**
> "If you want, the next step is a 60-minute working session where we map
> your specific AI estate — your Copilot deployment, your Foundry
> agents, your shadow AI exposure — onto these five pillars and identify
> which of the four phases you're actually in for each one. That gives
> you a prioritized backlog instead of a vendor checklist."

**For the AI platform team:**
> "The fastest concrete win is usually Purview DSPM for AI plus an agent
> inventory from Agent 365 or the relevant admin center. That gives you a
> defensible view of supported AI apps and agents, the data they can reach,
> and which ones need access scoping first."

---

## Appendix — Objection handling

| Objection | Response |
|---|---|
| *"We're multi-cloud, not Azure-only."* | Entra CIEM and Defender for Cloud are multi-cloud (AWS, GCP). MDCA discovers shadow AI regardless of where it runs. The architecture isn't Azure-locked. |
| *"We already use \<third-party DLP / CSPM / SIEM\>."* | Great — the signal model still applies. Many Purview, Defender, and Entra signals can be exported or integrated through Microsoft Graph Security API, Sentinel connectors, or product-specific APIs. The value is the AI-specific signal, not lock-in. |
| *"How is this different from just buying Security Copilot?"* | Security Copilot is the **analyst experience** on top of this stack. The architecture underneath is what produces the signals it reasons over. You need the foundation first. |
| *"Prompt injection feels unsolvable."* | It is, in the general case. The architecture treats it as a **detect-and-contain** problem, not a prevent-it-100% problem — Content Safety reduces volume, DfC + XDR catch what gets through, CAE limits blast radius. |
| *"Our agents are built in \<non-Microsoft framework\>."* | Treat governance as connector-dependent. Microsoft is moving toward standards-based agent interoperability, including MCP and agent-to-agent patterns, but coverage depends on the platform, identity model, and available integrations. Data-plane controls such as Purview DLP, Defender for Cloud, and Entra still apply where traffic, resources, identities, or data sources are in scope. |

---

## Timing cheat sheet

| Section | Time | Cumulative |
|---|---|---|
| Pre-flight + opening | 2 min | 2 |
| Hub-and-spoke diagram | 3 min | 5 |
| Two threat scenarios | 10 min | 15 |
| Roadmap | 3 min | 18 |
| Close + Q&A buffer | 5–10 min | 25–30 |
