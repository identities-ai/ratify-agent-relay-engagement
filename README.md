# ratify-agent-relay-engagement

The stage for the [Agent Relay](https://agentrelay.com) x [Ratify](https://ratifyprotocol.com) Phase 2 engagement: a purpose-built public repository whose `/docs` path a contractor agent works in under bounded, revocable, provable authority.

What happens here during the engagement:

- Ratify Protocol delegates authority to Agent Relay's lead agent: scope `files:write`, cryptographically bound to `/docs` of this repository, short expiry, revocable.
- Agent Relay's implementation agent does real work in `/docs` and opens a pull request. Every commit carries a verifier-signed receipt.
- Mid-task, the upstream delegation is revoked. The agent's next handoff fails closed.

Nothing production-critical lives here, but everything is real: public history, real CI, a real pull request.

Every claim can be re-verified offline from the reproduction harness at [`identities-ai/ratify-agent-relay-harness`](https://github.com/identities-ai/ratify-agent-relay-harness), with any of the five Ratify SDKs.
