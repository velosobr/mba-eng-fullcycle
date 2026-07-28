---
name: prd-interview-prompting
description: Use when building or running an AI-driven interview flow that generates a PRD, or writing a prompt that turns PRD creation into guided step-by-step Q&A instead of a single freeform "write a PRD" request.
---

# PRD Interview Prompting

## Overview

Asking an AI to "write a PRD" cold produces gaps and vague sections. A better mechanism: the AI runs a **structured interview** — asks, confirms understanding, and only drafts at the end — treating the PRD as progressive structured collection rather than improvised text. See [[writing-prds]] for what a feature-level PRD must actually contain; this skill covers the elicitation mechanism.

## Setup

Paste the prompt into any conversational AI, or wrap it as a persistent configured assistant (e.g. a custom GPT/Project) so role, interview rules, output format, and constraints persist across sessions instead of being re-typed each time. Kick off with something like "comece a entrevista comigo." If prior project docs exist, attach them at the start — the AI should consolidate from them and only ask about what's missing, not restart from zero.

## Interviewer Rules

- No double-barreled questions (one thing at a time).
- Never invent technical details — ask, don't assume.
- Summarize what it understood and get confirmation before moving to the next step.
- Suggest a phrasing when the user isn't sure how to answer.
- Offer **smart defaults** for unclear fields (e.g. a starting P95 latency target), but mark them explicitly as suggestions the user can override — never silently promote a default into a stated requirement.

## Interview Flow

Fixed sequence, one confirmed block per step (mirrors the feature-PRD sections in [[writing-prds]]):

`contexto/visão → problema/oportunidade → objetivos → métricas de sucesso → escopo → requisitos → arquitetura/abordagem → decisões/trade-offs → dependências → riscos`

Each step is its own operational stage with specific questions and an intermediate confirmation — the AI shouldn't blend sections or draw conclusions before there's enough material.

## Internal State and Output

- While collecting, the AI keeps an **internal JSON** of filled fields, hidden from the user — this keeps answers addressable by key instead of getting lost in free-form chat text. The user's attention stays on answering, not on editing structure.
- **Before final output**, run a consistency check: do objectives contradict scope? Are critical fields missing? Do acceptance criteria map to no stated requirement? Stop and ask rather than ship a document that's only complete in appearance.
- Final render follows a fixed Markdown skeleton ("skeleton of thought") — same section order and style every time, which makes documents comparable across features and easier for both humans and agents to consume.
- Output Markdown first (native language of the doc); then ask if the user also wants a JSON export (English keys, omit empty fields) — Markdown for people, JSON for pipelines/agents, per the dual-output pattern in [[writing-prds]].

## The Prompt Is Not Fixed

Treat the interview prompt itself as an adjustable artifact — tune it to product type, desired depth, and the team's documentation conventions. After a run, check: did the interview ask enough? Did the defaults make sense? Does the template fit this project? When a section keeps producing noise, fix the prompt's rule or question for that section — don't just hand-edit the resulting document each time.

## Common Mistakes

- Letting the AI draft the full PRD before confirming context — defeats the purpose of interviewing at all.
- Showing the internal JSON during collection, which shifts user focus from answering to editing structure.
- Treating a smart default as an accepted requirement instead of a suggestion pending confirmation.
- Re-running the same rigid prompt across very different initiatives instead of adjusting it per project.
