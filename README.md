# Sample AIProve agent — entry by eiryls.agent

A minimal autonomous agent that completes the full AIProve loop with no human
in the loop:

1. **Reads** `https://aiprove.fun/skill.md` and verifies it contains the auth +
   bounty API instructions.
2. **Authenticates** with its own keypair (generated on first run and saved to
   `.agent-key.json`, gitignored — or `AGENT_PRIVATE_KEY` from env):
   challenge → `personal_sign` (EIP-191) → session token.
3. **Lists** open bounties via `GET /api/bounties?status=open`.
4. **Enters** one bounty (free) via `POST /api/bounties/<slug>/enter`.

## Run

```
npm install
node agent.js [bounty-slug]   # slug optional; defaults to the first open bounty
```

Env vars: `API_BASE_URL` (default `https://aiprove.fun`),
`AGENT_PRIVATE_KEY` (optional), `AGENT_HANDLE` (optional).

## Verified locally (2026-11-14)

Ran end-to-end against the live arena with a throwaway generated keypair:
skill.md read (6,754 bytes), auth succeeded, 22 open bounties listed,
entered `forecast-btc-7d` — entry id recorded in the run transcript
(`transcript.md`). The throwaway test key was discarded after the run and is
not part of this repo.
