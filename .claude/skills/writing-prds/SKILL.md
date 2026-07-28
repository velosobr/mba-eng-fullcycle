---
name: writing-prds
description: Use when deciding whether an initiative deserves a PRD, distinguishing a product requirements doc from a technical design doc, or drafting/reviewing a PRD's vision, scope, personas, objectives, metrics, and requirements before architecture or implementation work starts.
---

# Writing PRDs

## Overview

A PRD is a **product** document: it states what is being built and why it exists, not how it will be implemented. It comes *before* technical design docs — see [[documentation-taxonomy]] for the full category map — because the AI (and the team) need product intent as context before interpreting architecture requests. Registering what feels "obvious" internally is not wasted effort: it's information the AI doesn't have.

## When a PRD Is Warranted

**Rule:** a PRD exists when there's perceptible value delivered to the user or the business — not for every functional requirement.

**Practical test:** can the implementation follow an already-known pattern, with essentially technical decisions (framework, config, standard flow)? → it's a functional requirement, folded into a larger PRD. Does it concentrate its *own* perceived value, measurable objectives, experience impact, specific business rules, and trade-offs that need to be settled before technical design? → it earns its own PRD.

**Worked example — same feature name, different granularity:**

| | Login (commodity) | Login (strategic) |
|---|---|---|
| Context | Standard auth to access the app, default framework flow | Multi-tenant platform, corporate security requirements |
| Signals | Predictable experience, no product-level decisions | SSO, 2FA, centralized logout, per-tenant access policies |
| Decisions involved | Technology/framework/config only | Who uses it, which policies apply, which integrations, which risks |
| Verdict | Functional requirement inside the macro PRD | Own PRD — has product-scale objectives (reduce login friction, cut unauthorized access, enable enterprise integrations) |

Compliance and multi-tenancy are strong signals a feature stopped being commodity: they introduce restrictions and decisions that don't fit in a single requirement line. The decision never depends on the technology used — it depends on how much product decision-density is concentrated in that one delivery.

**Exception — feature-as-subproduct:** a feature can deserve its own PRD even inside a larger product if it has its own objective, metrics, and scope, and high enough impact to justify separate context. Don't bury it as a line item in a bigger document.

## Granularity

| Level | Scope | Detail |
|---|---|---|
| Produto | whole product | broad, less detailed |
| Módulo / EPIC | a significant slice | intermediate |
| Feature | one specific delivery | narrow, more detailed |

Pick the level that matches the initiative's size and conceptual autonomy — too broad reads as generic, too granular fragments context across too many docs. A product can have one macro PRD plus feature/module PRDs for the parts that concentrate value or complexity.

### Macro PRD: the strategic questions it must answer

A high-level (product-wide) PRD isn't feature detail — it's the widest cut of product documentation, and can be read as a fixed set of questions the product must answer: why it exists, what it aims to achieve, what's in/out of scope, who it's for, what problem it solves, how objectives will be pursued, what general capabilities it needs, how success will be recognized, what could go wrong, what roadmap guides its evolution, who's involved, and how it connects to company strategy.

Many of these are strategic rather than technical — several originate top-down (leadership, company strategy) rather than in the dev team. That doesn't make the doc less useful for developers: it makes explicit premises that would otherwise arrive only implicitly. Roadmap here means a staged evolution view, not a detailed execution schedule; roles mean who influences/decides/validates/executes, not a technical org chart. **If these questions can't be answered, the gap isn't documentation — it's missing clarity about the project itself**, and that gap degrades every design doc and AI-assisted decision built on top of it.

## Structure: Macro PRD (Not a Rigid Template)

Sections vary by size and granularity — small initiatives can drop several sections; larger ones lose clarity without them. The goal is covering enough context to tell the product's story, not filling every field.

| Section | Answers |
|---|---|
| Visão e propósito | Core idea, why it exists — no implementation detail yet |
| Contexto e oportunidade | What scenario/benefit justifies it (market or internal) |
| Público e personas | Who's affected, concrete usage profiles |
| Objetivos e métricas | What it aims for + how success is *measured* (unmeasurable = doesn't guide prioritization) |
| Escopo | What's in / out — undeclared limits let teams assume different versions of the same project |
| Requisitos de alto nível | Macro capabilities, not technical flows (e.g. "sell shirts", "checkout" — not implementation) |
| Estratégia e fases | How it moves from intent to execution — phases/milestones, not a monolithic delivery |
| Riscos | What could compromise timeline, value, adoption, viability |
| KPIs | Observable indicators of progress/success, trackable during and after delivery |
| Stakeholders | Who has a stake, who validates, who must be consulted |

## Structure: Feature-Level PRD

Leaner than the macro structure — it's execution-level detail, not strategic framing. Frequent sections:

| Section | Answers |
|---|---|
| Resumo & contexto do problema | What's being built and what problem it solves — not just "implement X" |
| Objetivos e métricas | Expected result + how to verify it was reached, at feature scale |
| Escopo | What's in/out for *this* delivery specifically |
| Requisitos funcionais | Concrete capabilities/behaviors the feature must offer |
| Requisitos não funcionais | Quality/operating constraints: latency, availability, max downtime |
| Fluxo do usuário | Interaction sequence — surfaces gaps between a listed requirement and real usage |
| Dependências | Other systems/services/decisions this feature needs to exist or work |
| Arquitetura & trade-offs (optional, high-level) | Names the structural choices (language, storage, protocol) without replacing the design doc |
| Critérios de aceitação | Checklist that turns "done" from subjective judgment into verifiable conditions |
| Riscos & considerações gerais | Execution-level uncertainties, plus anything relevant that doesn't fit elsewhere |

**Worked example — centralized rate limiter:** objetivos mensuráveis ("indisponibilidade < 1min", "P95 < 150ms"); escopo inclui limite por chave/IP + janela deslizante + resposta 429, exclui fila de prioridade e API admin; arquitetura/trade-offs registra Go + Redis + REST em uma frase, sem duplicar o design doc; risco documentado explicitamente: Redis indisponível pode falhar ou bloquear a política incorretamente.

**Markdown + JSON, not either/or:** a feature PRD can also be exported as JSON alongside its Markdown — Markdown for human review/discussion, JSON (predictable keys, empty fields omitted) for pipelines, validation, and agent consumption. JSON doesn't replace the doc; it's a structured contract of the same content, useful whenever the PRD needs to feed prompts, automations, or downstream artifact generation.

## Common Mistakes

- Writing PRD content that's actually a design doc — architecture, infra, or provisioning detail belongs elsewhere (see [[documentation-taxonomy]]).
- Setting objectives with no measurable metric attached, making success unverifiable.
- Creating a formal PRD for every small functional requirement instead of reserving it for perceptible value or cross-team alignment needs.
- Forcing every section into a small initiative's PRD when several don't apply at that granularity.

## Who Writes It

Not exclusive to PMs — developers can and should draft/contribute to a PRD when they need more clarity on a high-impact or sensitive-scope feature, especially to make implicit team knowledge explicit for an AI that has no history with the project.

## Related

To have an AI elicit a feature PRD through a guided Q&A flow instead of a single freeform prompt, see [[prd-interview-prompting]].
