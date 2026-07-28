---
name: documentation-taxonomy
description: Use when deciding what kind of document a project needs — product doc (PRD) vs design/architecture doc vs infra doc vs operational doc vs reference doc — before picking a template, or when setting up a workflow to keep docs synced with an AI-assisted codebase.
---

# Documentation Taxonomy

## Overview

In the AI era, documentation is operational context, not just a preparatory artifact — models read it to implement, maintain, and plan, the same way tests preserve knowledge and reduce error in future changes. Each new chat/session starts like a new hire: no domain knowledge, no constraints, no local conventions. Explicit docs cut that ramp-up time.

**Core principle:** pick the type of document *before* the template. A document that tries to answer every question at once (what, why, how, where, how to keep it running) becomes generic, redundant, and hard to maintain — for humans and for AI context alike.

## When to Use

- Before writing any doc, when it's unclear whether it should be a PRD, a design doc, an infra doc, a runbook, or a reference guide.
- When a document is trying to do too much (mixing product intent with architecture, or architecture with provisioning).
- When designing a workflow where AI both consumes docs as context and updates them after code changes.

## Quick Reference

| Category | Question it answers | Typical artifact |
|---|---|---|
| Product | O quê / por quê (what / why) | PRD |
| Design & Architecture | Como (how) | Design doc, ADR |
| Infrastructure | Onde / com quê (where / with what) | IaC docs, provisioning notes |
| Operational | Como manter (how to keep running) | Runbooks, incident playbooks |
| Knowledge & Reference | Como trabalhar (how to work in this codebase) | Onboarding guides, internal references |

"Design docs" is not one document — it's the umbrella term for the four technical categories (design/architecture, infra, operational, reference). Calling everything a "design doc" erases real differences in audience, depth, and lifecycle.

## Living-Doc Workflow with AI

Treat documentation as both input and output of the delivery workflow:

1. **Input** — before implementing, feed the AI the relevant doc(s) for context (product intent from the PRD, technical constraints from the design doc).
2. **Output** — after a feature ships or code changes, task the AI with reviewing and updating the docs it touched, the same way updating tests is a required step, not an afterthought.

This is what keeps a doc from decaying: staleness is the main reason documentation loses value, and an explicit "update docs" step in the workflow is the fix — not manual discipline alone.

## Common Mistakes

- Asking for "a design doc" with no category — vague prompts produce vague docs. Ask for the specific category (architecture doc, infra doc, ops runbook) since the category itself bounds the expected content.
- Writing a product doc that sneaks in architecture/infra detail, or a technical doc that re-justifies the product case from scratch.
- Skipping the doc-update step after a change ships, letting the artifact drift from the system it describes.

## Related

Deciding *whether* an initiative even needs a product doc, and how to structure one, is covered in [[writing-prds]].
