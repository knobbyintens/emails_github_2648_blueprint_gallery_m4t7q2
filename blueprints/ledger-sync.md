---
title: "Real-Time Ledger Sync"
slug: ledger-sync
category: integration-blueprint
status: published
published_at: 2025-10-14
summary: "Stream billing journal entries into the ERP ledger in near real time with exactly-once delivery and replay-safe recovery."
tags:
  - billing
  - ledger
  - exactly-once
  - event-streaming
repo_url: "https://github.com/knobbyintens/emails_github_2648_ledger_sync_m4t7q2"
---

## Overview

Real-Time Ledger Sync bridges the billing service and the finance ERP. Every
posted invoice, credit note and refund is emitted as an immutable ledger event
and applied to the ERP journal exactly once.

## Design highlights

- **Outbox ingestion** — the billing service writes ledger events to a durable
  outbox before acknowledging the transaction.
- **Idempotent posting** — each event carries a deterministic posting key, so a
  retry after a timeout cannot create a duplicate journal line.
- **Replay-safe checkpoints** — consumers persist their position and can replay
  a bounded window without double-posting.
- **Reconciliation** — a nightly reconciliation job compares the billing
  sub-ledger against the ERP control account and raises discrepancies.

## Operational notes

The reference implementation runs as a small worker fleet. Throughput is
controlled by the ERP posting adapter; back-pressure is propagated to the
outbox when the ERP is unavailable.
