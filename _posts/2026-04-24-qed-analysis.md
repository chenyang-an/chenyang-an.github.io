---
layout: post
title: "QED Solves Two Open Problems in Analysis"
date: 2026-04-24 12:00:00-0400
description: QED proved two research-level problems in fluid dynamics and transport equations, verified by domain experts
tags: AI math reasoning agents
categories: project
related_posts: false
---

QED has successfully proved two open research problems in applied analysis and fluid dynamics, contributed by Professor Xiaoqian Xu from Duke Kunshan University. Both proofs have been verified by domain experts.

## The Challenge

Professor Xu submitted four problems spanning fluid mixing, critical transport equations, and shear flow analysis. These are open research questions from his work on incompressible flow and turbulence, building on Prof. Charlie Doering's 2016 conjecture about the Batchelor length scale in advection-diffusion processes.

## Results

| Problem | Domain | Outcome |
|---------|--------|---------|
| P1 | — | Failed (9 iterations) |
| P2 | — | Failed (9 iterations) |
| **P3** | Critical transport equations | **Proved (Round 1)** |
| **P4** | Batchelor scale in shear flows | **Proved (Round 3)** |

### Problem 3: Nonexistence in Critical Transport Equations

QED proved this on the first attempt. The problem concerned fluid mixing and critical transport equations, specifically a construction question that Professor Xu expected might be possible.

The AI determined a negative answer—proving that the desired construction cannot exist. Professor Xu noted: *"AI just gives a very straightforward proof, which is not something we expected."*

### Problem 4: Equivalence for Batchelor Scale Conditions

QED solved this by round 3. The proof demonstrates that earlier research results already constitute an equivalent condition for Batchelor scale existence in shear flows.

Professor Xu: *"For P4, to my surprise, it shows that the result by Yupei and me is actually an equivalent condition"* rather than merely sufficient. He noted: *"We don't even need to go deeper into our argument; our result itself is equivalent to the existence of the Batchelor Scale."* This was unexpected because *"both of us agree that there may need some new tools"* to advance further—yet the AI showed no new tools were needed.

## Expert Assessment

Professor Xu, who works on applied analysis, fluid PDEs, and incompressible flow (Navier-Stokes/Euler equations), offered several observations:

**On proof quality:** Both proofs span 3-5 pages—typical for applied analysis papers. AI excelled at producing *"straightforward proof[s]"* where humans expected more complex approaches.

**On problem-solving approach:** *"It will not try to really follow the existing papers...but tries to find a solution all by itself."* This independence produced novel solutions.

**On automation:** *"All the prompt words are for general fields. The proofs were not obtained through guidance from experts."* QED solved these problems without domain-specific prompting or human steering during execution.

**On significance:** *"Knowing the correct answer is very important"* in applied analysis. For P3, the AI determined a construction was impossible; for P4, it revealed an existing result was stronger than the authors realized. Both answers advance understanding of the underlying mathematics.

## What This Demonstrates

**AI can generate novel ideas.** Professor Xu expected complex approaches; the AI found straightforward proofs he didn't anticipate. It solved problems by finding its own path rather than following existing literature.

**AI system has ability to verify its own proofs.** QED's verification pipeline correctly distinguished success from failure: it declared P1 and P2 unsolved after 9 iterations, while accepting P3 and P4 as valid proofs—which human experts subsequently confirmed.

**AI can contribute to math research in natural language.** These aren't formalized proofs in Lean or Coq. They're natural language proofs in applied analysis, the way mathematicians actually write. With the [Carleman weight function](/blog/2026/qed/) result, QED has now solved three expert-verified research problems across different areas of mathematics.

Full proofs, problem statements, and complete expert comments: [github.com/proofQED/QED/tree/main/proved_statements/analysis-Apr-24-2026](https://github.com/proofQED/QED/tree/main/proved_statements/analysis-Apr-24-2026)
