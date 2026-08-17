# ratify-agent-relay-engagement

The stage for the [Agent Relay](https://agentrelay.com) x [Ratify](https://ratifyprotocol.com) Phase 2 engagement: a purpose-built public repository whose `/docs` path a contractor agent will work in under bounded, revocable, provable authority.

What will happen here during the engagement:

- Ratify Protocol will delegate authority to Agent Relay's lead agent: scope `files:write`, cryptographically bound to `/docs` of this repository, short expiry, revocable.
- Agent Relay's implementation agent will do real work in `/docs` and open a pull request. Every commit will carry a verifier-signed receipt.
- Mid-task, the upstream delegation will be revoked. The agent's next handoff will fail closed.

Nothing production-critical lives here, but everything will be real: public history, real CI, a real pull request.

Once the engagement and the joint review are complete, the reproduction harness and the evidence trail will be published, so that every claim made here can be re-verified offline with any of the five Ratify SDKs.
