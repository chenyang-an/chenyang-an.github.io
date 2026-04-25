---
layout: post
title: "QED Solves Two Open Problems in Analysis"
date: 2026-04-24 12:00:00-0400
description: QED proved two research-level problems in fluid dynamics and transport equations, verified by domain experts
tags: AI math reasoning agents
categories: project
related_posts: false
---

Recently, in the realm of LLM-based mathematical reasoning, a common refrain has emerged: although state-of-the-art models achieve strong performance on benchmarks—and occasionally appear to contribute to research—they still cannot generate truly original, nontrivial ideas. When results attributed to AI look impressive, critics point out that solutions to Erdős-type problems are actually rediscoveries of existing results, or that the LLM-assisted math papers are really about computation rather than genuine proof.

I disagree. I believe state-of-the-art models are already capable of generating original proofs that solve nontrivial open problems. Here is the latest evidence.

## Two Open Problems, Solved Autonomously

[QED](/blog/2026/qed/), developed by we researchers at UC San Diego and Caltech, has proved two open research problems in applied analysis and fluid dynamics, contributed by **Professor Xiaoqian Xu**, Assistant Professor of Mathematics at Duke Kunshan University. Both proofs have been verified by Professor Xu.

These problems come directly from Professor Xu's active research on fluid mixing and energy cascade in turbulence—specifically, a line of investigation tracing back to **Prof. Charlie Doering's 2016 conjecture** about the Batchelor length scale in advection-diffusion processes. As Professor Xu explains:

> The research project is about fluid mixing, or about the energy cascade in the study of turbulence. Charlie Doering in his paper in 2018 with Christopher Miles predicts that there should be some mode, which is similar to the Batchelor length scale in turbulence, so that the advection-diffusion process will get stuck on these modes.

The problems were submitted to me, a PhD candidate at UCSD with no background in applied analysis or fluid PDEs. I ran QED with no domain-specific prompting, no expert guidance during execution, and no human intervention at any point.

## Results

| Problem | Domain | Outcome |
|---------|--------|---------|
| P1 | Numerical analysis of Bessel functions | Failed (9 iterations) |
| P2 | Replicating paper methodology | Failed (9 iterations) |
| **P3** | Critical transport equations | **Proved (Round 1)** |
| **P4** | Batchelor scale in shear flows | **Proved (Round 3)** |

QED self-rejected its own proofs for P1 and P2 across all 9 rounds, and independently solved P3 and P4. The system's verification pipeline correctly distinguished valid proofs from flawed ones—a fact subsequently confirmed by human expert review.

## Problem 3: A Negative Answer Nobody Expected

Problem 3 concerns a critical case of the transport equation in fluid mixing. The question: can one construct a smooth, mean-zero function and a bounded shear velocity such that solutions to the transport equation exhibit exponential decay in the homogeneous Sobolev norm $$\dot{H}^{-1}$$?

Professor Xu expected the answer to be yes—that a construction was possible through manipulation of Fourier modes and special functions. **QED proved the opposite on its first attempt.** The construction is impossible.

The proof proceeds by showing a fundamental tension: conserved $$L^2$$ mass and controlled derivative growth force a portion of the solution's mass to remain at moderate Fourier frequencies, producing a polynomial lower bound on the $$\dot{H}^{-1}$$ norm that contradicts any exponential decay.

Professor Xu:

> For P3, it's about a critical case of the transport equation; usually people would expect some harder tools to deal with it, but AI just gives a very straightforward proof, which is not something we expected. What I expected is that such a construction is possible—it seems like some playing around with the Fourier modes with some special functions. However, AI gives me a negative answer.

## Problem 4: An Existing Result Was Stronger Than Its Authors Realized

Problem 4 asks whether a `limsup` condition in a recent result by Professor Xu and his collaborator Yupei can be strengthened to a `liminf`—a question about whether the Batchelor scale truly exists for shear flows in the advection-diffusion equation.

Professor Xu and his collaborator had proved the first result showing the Batchelor scale exists for advection-diffusion in shear flows. But they believed their result was only a sufficient condition, and that proving the full equivalence would require fundamentally new tools.

**QED showed they were wrong—in the best possible way.** Their existing result is already an equivalent condition.

> For P4, to my surprise, it shows that the result by Yupei and me is actually an equivalent condition for shear flow—that the Batchelor Scale exists.

> This is really impressive because both of us agree that there may need some new tools, not just by our argument, to prove that the Batchelor Scale really exists. So this is the next thing we are planning to do. But AI told us that we don't even need to go deeper into our argument; our result itself is equivalent to the existence of the Batchelor Scale.

> The proof is relatively straightforward, but it is still nontrivial, and if we don't know the definite answer, we will probably never try it.

This last point is worth emphasizing. The proof is straightforward *once you know the answer is true*. But no one tried it, because the experts in the field assumed it would require new machinery. The AI's contribution was not just the proof itself—it was revealing that the proof was within reach.

## Expert Assessment

Professor Xu offered extensive commentary on the results. Several observations stand out.

**On proof quality and length:**

> I think both proofs are not hard. However, they are also not trivial, about 3-5 pages long. This is a tricky length; in a field like applied analysis, this is a length for the proofs in most of the acceptable papers, especially in the papers involving physics.

**On AI and analysis—breaking a misconception:**

> Usually we may think AI can only work for algebraic, combinatorial, or other problems that could be formalized—usually it may need Lean. Few people, especially in the field of analysis or PDE, think that it can really work for analysis problems. These proofs show that AI can really help, even with LLM.

**On knowing the answer:**

> In my field, usually knowing the correct answer is very important. Now these proofs show that AI is very good at attempting.

For P3, the AI determined the expected construction was impossible. For P4, it revealed an existing result was stronger than its authors believed. In both cases, knowing the correct answer changed the direction of the research.

**On full autonomy—no expert steering required:**

> In the whole process, I only provided the problem description. Chenyang, who is not an analyst, did all the prompt work, which means that all the prompt words are for general fields. The proofs were not obtained through guidance from experts. To be honest, I myself don't know how to solve the problems at all.


## What Failed—and Why That's Informative

The failures are as instructive as the successes. P1 involved a complicated function with Bessel functions where numerical simulation suggested certain properties but manual proof was elusive. P2 asked the system to replicate a paper's methodology with a slightly different differential equation—a standard task for a graduate student.

Professor Xu's diagnosis:

> When AI thinks about a problem, it seems that it will not try to really follow the existing papers, even if I mentioned the papers, but tries to find a solution all by itself. And also, the solution of P2, if it exists, should be longer, like 10-20 pages.

The AI's strength and weakness are two sides of the same coin: it does not follow existing approaches. When a novel path exists (P3, P4), it finds one. When the problem demands faithfully replicating established methodology or handling lengthy arguments (P1, P2), it struggles.

## What This Means

**AI can generate original mathematical ideas.** The experts expected complex approaches; the AI found straightforward proofs they didn't anticipate. It determined P3 was impossible when the expert expected it was possible. It showed P4's answer was already implied by existing work when the experts planned to develop new tools. These are not pattern-matched solutions—they are genuinely novel contributions.

**Natural-language proof in analysis is viable.** These aren't formalized proofs in Lean or Coq. They are natural-language proofs in applied analysis and fluid PDEs, written the way mathematicians actually write. The widespread assumption that AI math reasoning requires formal verification systems does not hold.

**Self-verification works.** QED's verification pipeline correctly rejected P1 and P2 while accepting P3 and P4—matching the subsequent human expert assessment exactly. The system knows when it has failed and when it has succeeded.

As of April 2026, AI systems are capable of generating original, nontrivial proofs for open research problems—and their capabilities are rapidly improving. With the [Carleman weight function](/blog/2026/qed/) result, QED has now solved three expert-verified research problems across different areas of mathematics.

Full proofs, problem statements, and complete expert comments: [github.com/proofQED/QED/tree/main/proved_statements/analysis-Apr-24-2026](https://github.com/proofQED/QED/tree/main/proved_statements/analysis-Apr-24-2026)
