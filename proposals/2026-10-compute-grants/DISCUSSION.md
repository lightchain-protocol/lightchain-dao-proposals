Title: Compute grants to onboard independent AI power and decentralise the network (draft v4.1)

Lightchain runs a working verified-inference network, but almost all of it is the Foundation's own hardware: 9 of the 13 workers online and 66 of 69 validators, and 89% of the last six weeks' jobs. Four independent workers are online and none can cover a GPU on today's fees.

This proposal is a twelve-month grant programme to change that:

- Independent workers receive a monthly grant floor for the model class they actually serve: $150, $400, $1,000 or $3,000. Independent validators $70. The grant covers only the gap between the floor and the fees earned, so every paid job shrinks it. Half paid monthly, half locked six months then vesting.
- Qualify by working: 30 released jobs a month, a stake equal to one month's grant, 95% uptime, every replay passed. 17 slots to start.
- The Foundation's own workers, validators and agents get nothing. The Foundation funds it. The Treasury spends nothing.
- Fees move to a dollar-anchored, per-token function, raised in three steps from 1 December, so the grants are temporary by design.
- Every funded worker is verified: replay sampling to 100% on adoption, weekly probes, tiers payable only for models the disputer can replay.
- Demand is named: autonomous agents at agents.us.org, paying for inference through the protocol.
- Governance catches up: protocol contracts under the DAO Timelock by 30 November, the Foundation leaves the validator fee pool, the agents.us.org domain is owned by the DUNA.

Read the two-page summary first, then the full draft if you want every rule and source:

- Summary (PDF): https://github.com/lightchain-protocol/lightchain-dao-proposals/blob/main/proposals/2026-10-compute-grants/Lightchain-Compute-Grants-Community-Summary.pdf
- Full draft v4.1 (PDF): https://github.com/lightchain-protocol/lightchain-dao-proposals/blob/main/proposals/2026-10-compute-grants/Lightchain-Compute-Grants-Proposal-v4.1.pdf
- The script that decides who receives a grant, so anyone can reproduce the list: https://github.com/lightchain-protocol/lightchain-operator-program

Every number is measured on chain 9200 at block 3,058,217.

Discussion is open for seven days. Tell us where you disagree, especially if you run a GPU or are building on the API. After that we post what changed and the proposal goes to a Governor vote.
