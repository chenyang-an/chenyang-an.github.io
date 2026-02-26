---
layout: post
title: "Proofread: A 5-Phase Agent Pipeline for LaTeX"
date: 2026-02-26 10:00:00-0400
description: What my Proofread agent is, what it does, and how the 5-phase LaTeX proofreading pipeline works.
tags: AI agents latex proofreading claude-code
categories: tools
related_posts: false
---

I built [`proofread`](https://github.com/chenyang-an/proofread), an automated proofreading pipeline for LaTeX papers and textbooks.

It is not just a single prompt. It is a multi-phase agent workflow that splits documents into sections, proofreads each section, verifies report quality, and then produces an aggregate summary.

## What It Is

`proofread` is a Claude Code based proofreading system for LaTeX source.

The pipeline is designed for long technical writing where errors are distributed across many sections: typos, grammar issues, LaTeX issues, notation inconsistencies, and mathematical mistakes.

## What It Does

The system runs in 5 phases:

1. **Split (Phase 0):** split each `ch<N>.txt` chapter into section-level files using `\section` boundaries.
2. **Context Builder (Phase 1):** build a chapter context index (definitions, notation, conventions).
3. **Proofreader (Phase 2):** review each section for language, LaTeX, and math issues.
4. **Verification (Phase 3):** audit the proofreading report for false positives, missed issues, and format quality.
5. **Verdict + Summary (Phases 4-5):** either accept the section report (`DONE`) or retry (`CONTINUE`, up to 3 iterations), then generate a global summary report.

This verification loop is the key design choice: the system does not trust the first draft of its own report.

## Inputs and Outputs

Input format is simple but strict:

1. You provide files named `ch1.txt`, `ch2.txt`, ...
2. Each chapter file must contain `\section{...}` or `\section*{...}` markers.
3. Content before the first `\section` is ignored.

Main outputs:

1. Per-section reports in `result/proofread/ch<N>/...`
2. Verification files in `result/verification/ch<N>/...`
3. Final aggregate summary in `result/summary/proofread_summary.md`

## Why I Built It

I built `proofread` because I believe current frontier models are already strong enough to save a large chunk of proofreading labor.

The goal of this pipeline is to automate as much of that repetitive work as possible while keeping final decisions in human hands.

## Scope and Limits

This tool is a proofreading and review assistant, not a replacement for author judgment.

I still treat theorem validity, final mathematical correctness, and editorial decisions as human-owned.

Also, because the pipeline uses Claude Code with `--dangerously-skip-permissions`, it should be run carefully (ideally in a sandboxed environment), and API cost should be monitored for large books.

## Repository

- [`chenyang-an/proofread`](https://github.com/chenyang-an/proofread)

If you are writing in LaTeX and want agentic quality control, this project is a practical starting point.
