# Federation note — Ratify run, 2026-08-19

Written by Agent Relay's implementation agent under a Ratify delegation issued by
Ratify Protocol's root, sub-delegated by the contractor lead, and constrained to
this repository under `/docs`. It records the second session, which existed to
close three gaps the first one left.

## The federation beat, run live

Two certificates were issued under the same root, naming the **same channel
identifier** under two different deployment authorities:

| certificate | authority | deployment | reason |
| --- | --- | --- | --- |
| `relay-run-1787160417` | `ratify.agentrelay.com` | served | — |
| `relay-run-1787160430` | `relay.ratifyprotocol.com` | refused | `unserved_authority` |

The load-bearing half is what the refusal did **not** do. The core chain result
for the refused presentation is `authorized_agent`, and the receipt records it as
such: the delegation is valid and this deployment declined to act on it, because
the resource names an authority it does not serve. A refusal that also broke the
chain result would make policy indistinguishable from a bad delegation.

Receipt hashes, as written by the driver and as published by the deployment:

```text
served    gwDnZE8NcTSsJz2PSKSwDVZuqBa8HPJ7UbX8keJWdeo=
unserved  0rYU5tBGF51ZIRZbKwxZ8s2vzQ+6OUGqWxMexC/rzME=
```

Until this session these cases had only ever run in-process, against a verifier
generated locally. They had never touched the deployed adapter or this root.

## What the deployment says about itself

Each `ratify_present` and `ratify_task` verdict is published to the adapter's
agent metadata as `ratify_last_presentation`, carrying the `receipt_hash`. A
counterparty holding the workspace key can therefore confirm that a receipt we
publish is the one the deployment actually decided on, rather than taking our
account of it. It is a single overwritten key describing the most recent call —
a current verdict, not a log. `ratify_turn` is excluded deliberately: it is
per-message, and a metadata write per message trades a diagnostic for a latency
problem.

## This write

Verified before this commit landed, in this order:

- the delegation chain verifies against an issuer established out of band, and
  against Ratify Protocol's real root rather than a stand-in this side minted
- the same chain is **refused** for a path outside `/docs`, checked before any
  bytes were written
- the receipt and the separately signed deployment decision were persisted for
  both the control and the authorized write; the receipt hash for this commit is
  in the pull request body

A receipt carries no identifier of its own. It is named by its hash, `prev_hash`
chains it to the one before, and the deployment decision binds to it by
`receipt_hash`. That is the per-commit handle.

## Two properties of the hop, kept separate

Sub-delegation narrows authority in scope, and it also narrows it in duration:
the child's lifetime is `min(requested, parent_remaining)` **at issuance**. That
is one mechanism. A parent cut short *after* a child is issued is a second and
different one — the verifier checks each certificate's own window, and
revocation is checked separately. "A child cannot outlive its parent" is a fair
description of neither on its own, so this note does not make that claim.
