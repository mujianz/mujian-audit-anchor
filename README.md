# mujian-audit-anchor

External audit anchor for the Mujian delivery-error escape-rate system (policy v5.0).

## What this repository is

A write-once evidence anchor. Weekly automated audit results (receipts) and the
sampling manifest are proposed here as pull requests by a GitHub Action. A
receipt only becomes permanent after a human maintainer approves and merges it
into the protected `main` branch.

## What this repository contains

- `policy/policy.json` — audit rules, sampling parameters, capability switches.
- `audit/manifests/YYYY-Www.json` — which items were sampled that week.
- `audit/receipts/YYYY-Www.json` — the weekly audit result (sampled / escaped /
  blind_spot / audit_missing counts plus structural findings).
- `.github/workflows/audit.yml` — the external auditor. Changes require human
  approval like everything else.
- Temporary `audit-input/*` branches hold the weekly anonymized snapshot and
  are never merged into `main`.

## Content policy (strict)

This repository is public on purpose. It may contain **only**:

ISO week numbers, integer counts, SHA-256 hashes, rule identifiers, status
enums, timestamps.

It must never contain: real names, phone numbers, email addresses, client
names or contact details, money amounts, prices, job titles, business text,
internal file paths, IP addresses, tokens or API keys.

The audit workflow hard-fails if an input snapshot contains any field outside
the whitelist. The numbers here carry no business meaning on their own; their
value is the tamper-evident timestamp chain.

## Failure semantics

A missing weekly receipt is itself a signal: the Action opens an
`AUDIT_MISSING` pull request. "No report" is never treated as "all clear".
