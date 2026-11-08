---
title: "Omnichannel Notify Hub"
slug: notify-hub
category: integration-blueprint
status: published
published_at: 2025-09-30
summary: "Fan out transactional notifications across email, SMS, push and partner webhooks with a single preference-aware API."
tags:
  - notifications
  - omnichannel
  - webhooks
  - preferences
repo_url: "https://github.com/legacy-integrations/notify-hub-core"
---

## Overview

Omnichannel Notify Hub gives product teams one API for transactional
notifications and hides the details of channel providers, retries, and
per-user preferences.

## Design highlights

- **Preference-aware routing** — a user's channel preferences and quiet hours
  are applied before any provider call is made.
- **Provider fan-out** — a single request can fan out to email, SMS, mobile
  push and partner webhooks.
- **Template versioning** — message templates are versioned and resolved at
  send time.
- **Delivery receipts** — provider receipts are normalised into a common status
  stream for support tooling.

## Operational notes

The reference implementation exposes a thin HTTP API and a worker pool that
isolates provider latency from the request path.
