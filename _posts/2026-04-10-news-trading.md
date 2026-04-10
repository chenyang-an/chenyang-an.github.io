---
layout: post
title: "Building a Low-Latency News Trading Agent"
date: 2026-04-10 10:00:00-0400
description: An open-source AI agent for real-time financial decision-making that processes news and executes trades within 1.5-2 seconds
tags: AI trading agents finance
categories: project
related_posts: false
---

I'm open-sourcing [news_trading_agent](https://github.com/chenyang-an/news_trading), a system that combines real-time news analysis with algorithmic trading. The agent processes live headlines, extracts trading signals using LLMs, and executes trades through Interactive Brokers within 1.5-2 seconds.

## Why Low-Latency Matters

News-driven trading operates on a simple premise: markets react to information, and faster reaction means better prices. When a headline breaks, the window for profitable action is measured in seconds. This requires:

- Continuous monitoring for new information
- Fast signal extraction from unstructured text
- Immediate order execution
- Mechanical position management under time pressure

The system prioritizes speed and simplicity over sophisticated forecasting.

## Architecture

The codebase organizes into four modules:

- **common/** — Shared database initialization and helpers
- **trading/** — Asynchronous polling loop, LLM-based headline interpretation, and position lifecycle management
- **model_testing/** — Batch inference harness supporting multiple LLM providers

## Trading Workflow

The trading engine implements this sequence:

1. Connect to IBKR at `127.0.0.1:2048`
2. Continuously poll the SQLite news table for new entries
3. Apply rule-based filtering to reject obvious non-trades
4. Query the LLM for ticker identification and directional scoring (1-5 scale)
5. Convert extreme scores (5 for BUY, 1 for SELL) into market orders
6. Manage positions via mechanical exits based on hold time and threshold percentages

The design prioritizes fast interpretation plus simple execution over sophisticated optimization. Positions exit mechanically rather than through dynamic optimization, keeping the system transparent and debuggable.

## Hybrid Filtering

Not every headline needs LLM evaluation. Simple keyword rules reject obvious non-tradable headlines cheaply (earnings reports, routine filings, etc.), while ambiguous cases proceed to LLM evaluation. This reduces latency and API costs for the majority of headlines that don't contain actionable signals.

## Design Philosophy

The system embodies several deliberate choices:

**Simplicity over sophistication:** Mechanical exits trade long-term optimality for immediate understandability. When something goes wrong at 2am, you need to debug it fast.

**Conservative feature boundaries:** No portfolio-wide optimization, no scaling logic, no sophisticated hedging. Each position is independent.

**Transparency over black-box optimization:** Every decision is logged and traceable.

**Localized runtime:** All artifacts (databases, logs, screening outputs) remain within the repository structure.

## What's Not Included

The repository intentionally omits:
- News ingestion/scraping infrastructure (you supply your own headline source)
- Historical datasets or backtests
- Embedded credentials
- Production risk controls

This keeps the repository focused and forces users to understand what they're connecting it to.

## Operational Reality

This is not a turnkey production system. Running it requires:
- Interactive Brokers TWS/Gateway
- A working news-insertion process
- Substantial operational oversight
- Understanding that LLM-based classification errors will occur

The documentation explicitly warns that live trading code can result in losses, unintended orders, or operational failures. This is a research tool, not financial advice.

Check out the code: [github.com/chenyang-an/news_trading](https://github.com/chenyang-an/news_trading)
