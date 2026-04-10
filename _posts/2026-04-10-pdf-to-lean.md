---
layout: post
title: "pdf-to-Lean: Automatically Formalizing Mathematics from Textbooks"
date: 2026-04-10 11:00:00-0400
description: An open-source pipeline that converts mathematical PDFs and LaTeX into verified Lean 4 formalizations
tags: AI math formal-verification Lean
categories: project
related_posts: false
---

I'm releasing [pdf-to-Lean](https://github.com/chenyang-an/pdf_to_lean), a pipeline that automatically converts mathematical textbooks and research papers into verified Lean 4 formalizations. The system orchestrates multiple Claude agents to transform PDF or LaTeX source materials into machine-checked proofs.

## The Problem

Formalizing mathematics in proof assistants like Lean is valuable but tedious. Converting a textbook chapter into verified Lean code requires:
- Extracting mathematical content from PDFs
- Identifying theorems, definitions, and lemmas
- Translating informal mathematics into Lean's type theory
- Proving each statement while ensuring faithfulness to the original

This process is slow and requires expertise in both mathematics and formal verification. pdf-to-Lean automates this pipeline end-to-end.

## How It Works

The pipeline performs three conversions in sequence:

**1. PDF-to-LaTeX Extraction:** Splits PDFs into manageable chunks and reconstructs mathematical content using Claude's vision capabilities.

**2. Theorem/Definition Isolation:** Extracts only formal mathematical statements while preserving section structure.

**3. Lean Formalization:** Converts extracted content into verified Lean 4 code through iterative refinement loops.

The formalization proceeds through two main phases:

**Statement Formalization** (up to 9 rounds):
- Write Lean type signatures with embedded LaTeX quotes
- Self-verify three-way semantic equivalence (LaTeX ↔ natural language ↔ Lean)
- Independent verification by a separate agent
- Verdict determines whether to continue or conclude

**Proof Search** (up to 3 rounds):
- Replace `sorry` placeholders with actual proofs
- Use Loogle to discover relevant Mathlib lemmas
- Detect unfaithful statements and escalate rather than silently modify

## Faithfulness Verification

The core challenge in automated formalization is ensuring the Lean code actually says what the original mathematics says. pdf-to-Lean implements 11 layers of faithfulness verification:

- Embedded LaTeX quotes in Lean comments
- Automated coverage checking via regex and parsing
- Independent verification by separate agents
- Specs snapshots capturing frozen baselines
- Explicit prohibitions against agent modification of theorems
- Character-level drift detection during proofs

This prevents a common failure mode where AI systems "prove" theorems by subtly weakening them until they become trivial.

## Loogle Integration

The system includes a custom tool enabling agents to search Mathlib4 by type pattern, returning up to 15 matching lemmas with signatures and documentation. This helps agents discover existing library lemmas rather than reproving known results.

## Resume Support

Like [QED](/blog/2026/qed/), the pipeline supports resumption. It automatically detects completed rounds and skips them on re-run, accumulating token usage across sessions. This is important because formalizing a full textbook may consume millions of tokens.

## Output

The system produces a complete Lean project with:
- Formalized chapters importing from a root file
- Per-chapter utility files containing original text for reference
- Versioned specs snapshots tracking statement evolution
- Detailed logs of agent reasoning for every formalization attempt
- Final validation report with sorry/axiom counts and coverage metrics

Check out the code: [github.com/chenyang-an/pdf_to_lean](https://github.com/chenyang-an/pdf_to_lean)
