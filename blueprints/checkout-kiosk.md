---
title: "Edge Checkout Kiosk"
slug: checkout-kiosk
category: integration-blueprint
status: published
published_at: 2025-10-28
summary: "Run a resilient self-service checkout kiosk at edge locations, tolerating intermittent connectivity and delayed payment capture."
tags:
  - retail
  - edge
  - offline-first
  - payments
---

## Overview

Edge Checkout Kiosk packages a self-service checkout flow that keeps working
when the store's WAN link drops. Orders are committed locally and synchronised
with the commerce platform when connectivity returns.

## Design highlights

- **Offline order queue** — every basket is written to a local durable queue
  before the customer is asked to pay.
- **Deferred payment capture** — card authorisations are captured immediately
  when possible, and re-driven from the queue when the gateway is reachable.
- **At-most-once fulfilment** — order identifiers are generated on the device,
  so replayed sync batches cannot duplicate fulfilment jobs.
- **Store-and-forward telemetry** — kiosk health metrics are buffered and
  forwarded on reconnect.

## Operational notes

The reference runtime is packaged as a container for store controllers and
exposes a small health endpoint for the store monitoring system.
