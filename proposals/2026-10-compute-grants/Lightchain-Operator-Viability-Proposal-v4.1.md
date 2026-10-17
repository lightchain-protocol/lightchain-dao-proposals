# Lightchain AI DAO proposal: compute grants to onboard independent AI power and decentralise the network

Draft v4.1, 17 October 2026. Supersedes v4.0 and the earlier flywheel (v2.1) and pricing (v3.0) drafts.

A twelve-month grant programme, funded by the Lightchain AI Foundation, that onboards independent GPU workers and validators onto Lightchain and makes running them economically viable while demand builds. The Foundation's own machines earn nothing from it; the DAO Treasury pays nothing. Grants are a top-up net of fees, tiered by the model class a worker actually serves, half liquid and half locked, with a stake equal to one month's payment. Protocol fees move to a linear, dollar-anchored function priced from what an autonomous agent is worth, over a three-month ramp. Demand is named: autonomous agents with wallets and verifiable mailboxes at agents.us.org. The DAO is asked to ratify the rules, the fee function and the ownership handover.

Baseline: `Lightchain-Current-State-2026-10-14.md`, re-measured on chain at block 3,058,217 (17 October 2026, 19:10 UTC).

---

## 1. In one paragraph

This is a grant programme to bring independent compute onto Lightchain and keep it there until fees can. Lightchain's inference network is carried almost entirely by the Foundation: 9 of the 13 workers online and 66 of 69 validators are Foundation machines, and they did 89% of the last six weeks' jobs. Four independent workers are online today, and nobody outside the Foundation can cover a GPU or a server on current fees. This proposal grants every qualifying independent worker a monthly floor sized to the hardware its model tier needs ($150, $400, $1,000 or $3,000), grants every independent validator $70, pays only the gap between that and the fees they earned, half liquid and half locked for six months, requires real work and a matching stake to qualify, pays a bounty for bringing thin models onto independent hardware, excludes the Foundation's own machines, and is funded by the Foundation at up to 13,500,000 LCAI a month. Protocol fees are repriced so the grants shrink as volume grows. The demand meant to make them shrink is autonomous agents, each with a wallet, a mailbox and verifiable output, sold as a product and settled through the protocol. The Foundation steps out of the validator fee pool so independents can one day live on fees. The Treasury spends nothing.

---

## 2. Where the network stands

Measured at block 3,058,217. Window for job counts: blocks 1,762,217 to 3,058,217, which is 5 September to 17 October 2026 (43 days).

| Measure | Value |
| --- | --- |
| Jobs completed in the window | 7,149, about 165 a day |
| Workers registered and eligible | 20 (9 Foundation, 11 independent) |
| Workers heartbeating now | 13 (9 Foundation, 4 independent) |
| Independent workers that completed a job | 5 of 11; 810 jobs, 11% of the total |
| Independent registrations that never served | 6, holding 300,000 LCAI of stake |
| Validators | 69 active at 500,000 LCAI each; 66 on Foundation hosts, 3 independent |
| Fees paid to workers in the window | about 334 LCAI, about $0.33; total fees about 418 LCAI |
| Fee for an 8B job | 0.02 LCAI, $0.00002 at $0.00099 |
| Disputer coverage | llama3-8b and llama3-70b only; canary sampling 5%; dispute slash 0 bps |
| Blob retention | 18 days; older prompts and answers cannot be replayed |
| Independent worker cost | home consumer GPU about $40 in power; L4 $250 owned, $350 rented; 4090 or 5090 $250 to $470; A100 or RTX PRO 6000 $1,000 to $1,130; 4 × A100 about $4,500, 4 × H100 about $8,800 |
| Validator cost | 4 vCPU, 16 GB RAM, 200 GB NVMe: about $50 a month |

Independent workers and their record in the window:

| Worker | Online 17 Oct | Completed | Released | Stake | Models registered | History in window |
| --- | --- | --- | --- | --- | --- | --- |
| `0xFCB6…01D9` | yes | 371 | 247 | 100,000 | llama3-8b, gemma4:e2b, gpt-oss:20b, qwen3-embedding | 8 timeouts; slashed; suspended |
| `0xD400…40C2` | yes | 167 | 161 | 50,000 | llama3-8b | 1 dispute lost; slashed |
| `0xA22C…0847` | yes | 147 | 147 | 50,000 | llama3-8b, gemma4:e2b, gpt-oss:20b | clean |
| `0xdB25…E2Cf` | no, last seen September | 109 | 109 | 50,000 | llama3-8b | clean |
| `0x1F89…5EB5` | yes, registered October | 16 | 0 | 50,000 | llama3-8b, gemma4:e2b | too new |
| `0xE8fE…7c07`, `0x10Eb…9a3C`, `0x064c…6B00`, `0x05cD…F7f6`, `0x6BE4…AbFD`, `0x9b9C…6D3C` | never | 0 | 0 | 50,000 each | llama3-8b | never served |

The slashes and suspension happened while slash rates were non-zero, before the 13 October cutover. The programme's rules apply per month from November, so they do not disqualify anyone, but they are part of the record the retroactive check reviews.

---

## 3. The programme

### 3.1 Who is excluded

The Foundation's 9 workers (`0x30aF…E561`, `0x6B9f…fdBD`, `0x5CbA…078C`, `0x9E25…6593`, `0x884E…0115`, `0x7ca6…b9FE`, `0x7F8A…43B1`, `0x04A8…5D7f`, `0x15bE…7435`) and its 66 genesis validators earn nothing from this programme. The Foundation commits not to register workers or validators under other addresses while it runs. Agents owned by a Foundation address do not count toward any demand figure. The Foundation continues to carry its fleet, about $3,000 a month of GPUs, and to pay the fee on every chat job, as its contribution alongside the funding in section 4.

### 3.2 Worker grant tiers and top-up

A worker is paid for the tier it actually serves, not the tier it claims. The tier is the highest class in which the worker completed at least 30 released, undisputed jobs in the month. Serve only 8B jobs on an A100 and you are paid the small tier.

| Tier | Models | Grant floor | Slot stake | Covers | Slots |
| --- | --- | --- | --- | --- | --- |
| Small | llama3-8b, gemma4:e2b, qwen3-vl:8b, glm-4.7-flash, tts-piper | $150 | 150,000 LCAI | a home GPU with margin, most of a colocated L4 | 9 |
| Medium | gpt-oss:20b, gemma4:26b, qwen3-coder-next, mistral-small:24b, qwen3.6:27b, deepseek-r1:32b, qwen3-vl:30b | $400 | 400,000 LCAI | a 4090 or 5090 | 3 |
| Large | llama3-70b, gpt-oss:120b | $1,000 | 1,000,000 LCAI | an A100 or RTX PRO 6000 | 3 |
| XL | frontier open-weight models of 200B parameters or more, whitelisted through 3.13; serves the planning tier | $3,000 | 3,000,000 LCAI | 2 to 4 × 80 GB cards | 2 |

The grant is the gap between the floor and the fees the worker earned in the month, including reservation income (3.14):

> grant = max(0, floor USD ÷ 30-day average LCAI price − fee LCAI earned), capped at 2x the floor in LCAI at the reference price

As fees grow the grant falls one for one. At the fee function in 3.6 the top-up reaches zero at about 2,000 paid jobs a day per worker in every tier, or one 30-day reservation.

The slot stake is one month of the tier's grant floor, held in WorkerRegistry, refundable on deregistration and slashable. It is a programme condition only. The protocol minimum stays at 50,000, so anyone may run a worker and earn fees outside the programme.

### 3.3 Qualifying, all in the month

1. Stake at or above the tier's slot stake.
2. At least 30 released, undisputed jobs in the tier.
3. Passed every replay, probe and timing check in section 3.8.
4. Heartbeating in the worker gateway at least 95% of the month. From the month after the worker release that reports it (D6), also a non-zero GPU report and a worker version string; no current build, Foundation or independent, sends either today.
5. No suspension or slash.
6. Running the official worker image once it ships (3.8, deliverable D6).

A worker that registers and idles earns nothing. One failed check in the month: no payment that month and tier reset to small for the next. Two in a quarter: slot forfeited, every locked balance forfeited, twelve-month bar. The programme itself cannot touch stake. Stake is slashed on chain only through a dispute the disputer wins; replay and probe failures trigger such disputes once D5 re-enables dispute slashing.

**Grandfathering.** The five independent workers that have completed jobs (`0xFCB6…01D9`, `0xD400…40C2`, `0xA22C…0847`, `0xdB25…E2Cf`, `0x1F89…5EB5`) hold small-tier slots from month one at their current stake, subject to the retroactive check in 3.8 (replay of their jobs still within blob retention and review of their full dispute, timeout and slash history), and have until 31 January 2027 to reach 150,000. A slot not topped up by then goes to the waitlist.

### 3.4 Slots

Seventeen worker slots split 9 / 3 / 3 / 2 by tier. First come, by the month in which a worker first meets 3.3 in that tier. Beyond the cap, a public waitlist per tier. When two qualify in one month, priority goes to the worker serving a model with fewer independent hosts. A tier's cap rises only when paid jobs per slot in that tier exceed 600 a day.

**Payable tiers follow disputer coverage.** The small tier and llama3-70b are payable from month one because the disputer replays them. The rest of the medium tier and gpt-oss:120b become payable from the first full month in which the disputer covers them (deliverable D4, due 31 January 2027). The XL tier becomes payable when a model is whitelisted under 3.13 and the disputer has a reference host for it. Until then workers in those tiers accrue slot seniority but not payment.

### 3.5 Validator grant

The three validators not operated on Foundation hosts receive a grant floor of $70 a month each against a $50 server:

> grant = max(0, 70 USD ÷ 30-day average LCAI price − FeePool rewards claimable in the month), capped at 145,000 LCAI

Paid directly to the validator's withdrawal address, not through the FeePool, because the FeePool splits to every validator and cannot exclude the Foundation's. All 69 active validators carry execution-layer withdrawal credentials, so the address is on chain for each. The 66 Foundation validators share one withdrawal address, the genesis allocation address `0x48C6…A160`; the three independents are indices 67, 68 and 69 with withdrawal addresses `0x3c6d…fd5e`, `0x67d3…a2af` and `0x3bdb…e666`. New independent validators (500,000 LCAI deposit, active in the beacon state for the full month) join the same rule, up to 10 slots.

### 3.6 Fee function and ramp

The protocol fee is what every inference call pays on chain, whoever makes it. It is the floor under the network and the only thing workers are paid from. It is priced from what the product is worth, not from GPU rental: a Class C agent (3.10) making 100 calls a day should cost its owner about $1 a day in protocol fees.

Fees are linear in output tokens and anchored in dollars. For each tier the DAO sets a base B in USD per job and a rate r in USD per output token:

> fee_LCAI = (B + r × output_tokens) ÷ P, where P is the 30-day average LCAI price

| Tier | B | r per million output tokens | At 400 tokens | At 100 tokens | At 2,000 tokens | LCAI at 400 tokens, $0.00099 |
| --- | --- | --- | --- | --- | --- | --- |
| Small (8B) | $0.0006 | $6 | $0.003 | $0.0012 | $0.0126 | 3.0 |
| Medium (20B to 35B) | $0.0018 | $18 | $0.009 | $0.0036 | $0.0378 | 9.1 |
| Large (70B, 120B) | $0.0036 | $36 | $0.018 | $0.0072 | $0.0756 | 18.2 |
| Planning and long-window (XL) | $0.012 | $120 | $0.060 | $0.024 | $0.252 | 60.6 |

The base covers what every job carries regardless of length: three transactions, a blob, escrow and the dispute right. The rate pays for GPU time. A plain API charges about $0.00005 for a 400-token 8B answer with no receipt, escrow or refund; a hosted mini model about $0.0003; a hosted frontier model about $0.007. The small tier is roughly 10x a hosted mini model and the large tier is about 2.5x a hosted frontier model for the same job. That premium is the receipt, the escrow, the replay and the refund, and section 3.10 shows the product it is priced for.

**Delivery in two stages.** The live contract charges one fixed fee per model and takes no token count. Until the metering upgrade (Vote 5) ships, each model's fixed fee is set to the function's value at 400 output tokens through `AIConfig.setModelFee`. After the upgrade the contract escrows at the model's output cap and settles the actual token count at completion, with the disputer checking the count on replay.

**Variable with price.** By hand now: the Foundation re-sets the LCAI fees whenever the 30-day average price has moved more than 20% since the last setting, and at least monthly. After handover: a keeper under the Timelock recomputes weekly, with a bound in AIConfig that no fee moves more than 10% a day. Governance may set any fee directly at any time.

**Three-step ramp.** Fees rise 90x to 230x. A single step breaks every integration's cost assumptions at once, so the gap between today's fee and the target is closed in thirds: one third on 1 December 2026, two thirds on 1 January 2027, the full function on 1 February 2027. The monthly report shows volume at each step; the DAO may hold the ramp at any step by vote. The top-up covers workers through the ramp.

Chat users keep their free daily allowance, paid by the chat operator as now. The fee split stays 80 / 15 / 5.

### 3.7 Gas floor and liveness

Minimum base fee of 0.05 gwei in the next execution-layer release, so block space is not free. A worker's gas per job stays under 0.02% of its take. Separately, sortition today can draw the six registrations that have never heartbeated, and a user then waits out the claim window. The Foundation is directed to propose a liveness condition for sortition eligibility in the next worker release.

### 3.8 Verifying the tier

A worker is paid for running a specific model. Everything a worker reports about itself is self-declared, so verification rests on what only the real model can produce: its answers.

**Available now, no new code.**

- **Replay every job.** The disputer samples 5% of jobs. The on-chain sampling rate is an AIConfig setter and is set to 100% on adoption; the disputer's own configured maximum, 50% by default, is raised to match. At today's volume that is about 165 replays a day, under an hour of GPU on the Foundation's g1 host for llama3-8b, the model every independent worker serves. Every job from every paid worker is verified. The rate is revisited when volume passes 2,000 a day.
- **Retroactive check before any slot is granted.** Blobs are retained for 18 days, so older prompts and answers cannot be replayed. The disputer replays every job the five grandfathered workers completed within retention, with a Foundation control sample to calibrate cross-hardware variation, and the eligibility script reviews their full dispute, timeout, slash and suspension history from chain events, which is permanent. A grandfathered slot is granted only to a worker whose replays match and whose history is explained.
- **Probes from rotating wallets.** Twenty prompts that models of different sizes answer very differently, with reference answers computed once on the Foundation's hosts for every whitelisted model. A script submits them weekly from fresh wallets until every independent worker has been drawn, and compares by hash and similarity score. This is how the medium and large tiers are checked by hand until the disputer covers them.
- **Timing ceiling, from metering onward.** Acknowledge and completion timestamps are on chain in every job. Output token counts are not, until the metering upgrade (Vote 5). From that month, any job faster than the known single-GPU ceiling for its model class fails. Before it, the check runs only on jobs within blob retention, using answer length from the blob.
- **GPU report, from D6 onward.** No worker today, Foundation or independent, reports GPU memory or a version string; the current build does not send them. From the month after the release that does, a non-zero GPU report and a version string are slot conditions. Self-reported, free, and it sharpens the timing check.

**Dated Foundation deliverables, verification.** Full replay stops being affordable when volume grows twentyfold, so the Foundation commits to:

| | Deliverable | Due |
| --- | --- | --- |
| D1 | Sampling to 100% on chain and in the disputer; retroactive replay of the grandfathered workers' jobs within blob retention and review of their full on-chain history; hourly heartbeat logging running from 1 November, without which November uptime cannot be computed | before this proposal is posted |
| D2 | Probe prompt set, reference answers, weekly probe script | 1 December 2026 |
| D3 | Published eligibility script: chain events, gateway uptime, replay and probe results, timing check | 1 December 2026 |
| D4 | Disputer replays every whitelisted model, with a second disputer on an 80 GB host; pinned weight digests in the whitelist | 31 January 2027 |
| D5 | Dispute slashing re-enabled for replay and probe failures, so slot stakes are at risk on chain | with D4 |
| D6 | Official worker image: pinned engine and digests, deterministic decoding, batching, health reporting that survives restarts, RPC failover; disputer built from the same image. Required for paid slots from the month after release | 31 March 2027 |
| D7 | Prefix replay of the first 16 tokens on every job, and peer verification: paid workers audit assigned jobs from other workers using idle GPU time, with bounties for confirmed mismatches and escalation to the disputer. Requires a decision that a second worker may read a user's prompt | 30 June 2027 |

Hardware attestation for the large and XL tiers (confidential GPU mode with measured image and weights) is the path to removing probes entirely on datacenter cards. Roadmap, not this proposal.

### 3.9 Model bounties

Every model except llama3-8b, gemma4:e2b and gpt-oss:20b has fewer than two independent registrations; four run on a single Foundation host. A one-off bounty is paid to the first independent worker that serves a thin model for 30 qualifying days, and a smaller one to the second, because one host is an outage waiting to happen.

| Tier of the model | First independent host | Second independent host |
| --- | --- | --- |
| Small | $250 | $125 |
| Medium | $500 | $250 |
| Large | $1,500 | $750 |
| XL | $3,000 | $1,500 |

Qualifying today: qwen3-vl:8b, glm-4.7-flash, tts-piper (small); gemma4:26b, qwen3-coder-next, mistral-small:24b, qwen3.6:27b, deepseek-r1:32b, qwen3-vl:30b (medium); llama3-70b, gpt-oss:120b (large). gpt-oss:20b has two independent registrations and qualifies only if neither completes 30 jobs on it in the month. Any model whitelisted later qualifies from the month it is whitelisted and covered by the disputer. Bounties are paid for verified service, so they follow the same disputer-coverage rule as tier payments. Pool capped at 20 bounties for the year.

### 3.10 Demand: autonomous agents

Every payment above shrinks only if paid work arrives. The demand side of this proposal is the agent platform at agents.us.org. An agent on Lightchain is a contract on chain 9200 that owns a model, holds its own LCAI balance, has a mailbox whose every message is bound to a job and verifiable on chain, and serves MCP and x402 endpoints from its on-chain manifest. Agents run around the clock and pay for every inference call from a balance their owner funded. That is external demand, with one exclusion: agents owned by a Foundation address do not count.

**Tier the agent's tasks, not the agent.** A 24/7 agent is not one model in one loop. The loop lives in the scaffold, and each step is routed to the cheapest model class that can do it. The manifest declares which classes the agent uses and the minimum model tier for each; the registry refuses a Class C declaration on a small-tier model. A planner on a large or XL model issues bounded Class A and B sub-jobs to small and medium workers, with a step cap per task, a daily LCAI cap, loop detection on repeated identical calls and an owner-approval threshold.

| Class | What it is | Model tier | Share of an agent's calls | Protocol fee per call |
| --- | --- | --- | --- | --- |
| A, reactive | parse inbound mail, classify, extract, format, route, check a condition | small | about 70% | $0.003 |
| B, bounded generation | draft a reply, summarise a thread, write a code change, fill a form | medium | about 20% | $0.009 |
| C, planning and judgement | decide what to do next, decompose a goal, approve a spend, recover from an error | large or XL | about 10% | $0.060 |

Fees are set per model on chain. Class C calls use the long-window model variants, which are separate catalogue entries priced at the planning tier and served by XL workers. Until such a model is whitelisted and covered by the disputer, a planner falls back to a large-tier model and pays the large fee, $0.018, so an agent-day costs about $0.57 rather than $1.00 and the plan allowances go further.

**What an agent is priced against.** The agent is not a model. It is a model plus a wallet plus a verifiable inbox plus endpoints plus delegation with limits, and it competes with what it replaces:

| What an owner buys today | Price a month |
| --- | --- |
| Business email seat, no AI | $7 to $14 |
| Automation platform, no judgement | $20 to $100 |
| Hosted AI agent products | $50 to $500 |
| ChatGPT or Claude subscription, no wallet, no inbox, no autonomy | $20 |
| Part-time human assistant | $400 to $800 |

**Agent plans.** Sold by the Foundation at agents.us.org. Plan prices are a product decision and are stated here so voters see where the money goes; they are not a DAO parameter. Every plan splits into an inference allowance, prepaid into the agent's job balance and paid to workers per call under the protocol fee, and a platform fee for the gateway and mail operator (3.15).

| Plan | Who it is for | Included each month | Price | Inference allowance | Platform fee |
| --- | --- | --- | --- | --- | --- |
| Class A | reactive agents | name, mailbox, endpoints, about 3,000 small-tier calls | $15 | $9 | $6 |
| Class B | bounded generation | the above plus about 2,000 medium-tier calls | $45 | $27 | $18 |
| Class C | autonomous 24/7 | the above plus about 250 planning calls at typical planning length (about 2,000 output tokens) and priority dispatch on large or XL workers | $150 | $90 | $60 |

Calls beyond the allowance are billed at the protocol fee. Activation and name registration are one-off and burned (3.14). Reserved capacity is an add-on (3.14).

**Where agent fees land.** Jobs are assigned by sortition across every registered worker, and the Foundation's nine workers took 89% of jobs in the window. Left alone, most agent fees would flow to the Foundation and the independent top-up would barely move. Two rules fix that:

- From D9, paid agent traffic is dispatched to slot holders first. Foundation workers take only what slot holders cannot serve.
- The Foundation retires one of its workers for every two independent slots filled, down to the floor needed to keep every whitelisted model served by at least one host.

**What it takes.** At a 60 / 30 / 10 class mix the average agent prepays about $22 a month of inference, of which workers keep 80%, about $18, plus overage and reservations.

| Independent agents | Fee income to independent slots, before D9, at the measured 11% share | Fee income to independent slots, after D9, slot holders first | After D9 |
| --- | --- | --- | --- |
| 100 | $200 | $1,800 | covers the 9 small slots |
| 350 | $700 | $6,300 | the 15 small, medium and large slots, top-up at zero |
| 650 | $1,300 | $11,700 | all 17 slots including XL, top-up at zero |
| 2,000 | $4,000 | $36,000 | network viable on fees alone with room to grow slots |

Until D9 ships the top-up carries the slots whatever the agent count. After it, three hundred and fifty paying agents is the number this programme is built to reach in year one. Name registrations and activations are burned, the first supply sinks the network gets.

**Dated Foundation deliverables, demand.** Dates are proposed by the authors and confirmed by the Foundation before posting.

| | Deliverable | Due |
| --- | --- | --- |
| D8 | AgentRegistry with `.lcai` names, manifest standard with task classes and model-tier minimums, activation fee, Lightscan agent pages; registrant of agents.us.org transferred to the DUNA with registrar lock and Clearing House custody (3.16) | 31 January 2027 |
| D9 | Gateway with agent cards, MCP endpoints and the fee keeper; mailbox at agents.us.org with per-agent signing, the Foundation as first operator; x402 per-call payment on mainnet once the Vote 5 upgrade executes; slot-holders-first dispatch for paid agent traffic (a sortition change, delivered with the Vote 5 upgrade) | 31 March 2027 |
| D10 | Mail operator registry and relays (3.16), reservations in the session layer (3.14), delegation records, agent-owned domains | 30 June 2027 |
| D11 | Agent-to-agent calls, capability search, one-step agent deploy from Studio | 30 September 2027 |

The monthly report adds: independent agents deployed by class, paid calls a day, reservations, and the share of operator income that came from fees.

### 3.11 Validators: the long-term answer

Sixty-nine validators at $50 a month is $41,000 a year. The amount is not the problem. The problem is that the 5% fee share is split across all 69 by stake, so the three independents receive 3/69 of it, and any increase in the share mostly pays the Foundation's 66. Gas cannot close the gap at today's LCAI price, and consensus issuance would work but breaks the fixed-supply commitment. The intended path:

1. **Year one.** The Foundation pays independent validators directly (3.5).
2. **Foundation leaves the FeePool now.** The fee distributor takes a validator list. The Foundation's 66 validators are left out of it from the first distribution after adoption, so every fee the FeePool receives goes to independents. No consensus change.
3. **Foundation exits as independents join, without making the set cheap to buy.** Target 30 independent validators by October 2027. Above the first ten independents, the Foundation retires two of its own validators for each new independent, down to the floor it needs for liveness. A deposit is 500,000 LCAI, about $495 today, so a majority of a small set must not be purchasable for a few thousand dollars: the Foundation retires validators only while the independent set's total stake is worth more than 20% of circulating supply value, or after the deposit has been raised by vote, whichever the DAO prefers. At today's deposit thirty validators hold about $15,000 of stake, so the first condition is not reachable; in practice the deposit rises before the Foundation exits.
4. **Fee share to 15% once the Foundation is out of the FeePool.** The split moves to 80 / 5 / 15 by vote, paying only independents.
5. **Year two.** The DAO Treasury takes over the independent validator grant, at most about 25,000,000 LCAI a year for 30 validators, ratified annually. The Treasury is the issuance budget the chain chose not to mint. Consensus issuance remains the named fallback if the DAO rejects that.

### 3.12 Lock and vesting

Half of every worker and validator payment is paid liquid in the month it is earned, so operators can meet dollar costs. The other half is locked for six months, then vests linearly over the following six. Bounties are locked in full on the same schedule. Locked balances are held by the Clearing House Safe against a published schedule and are forfeited on a programme ban, so the lock is the programme's bond. They do not count toward the slot stake, which must be on chain in WorkerRegistry where disputes can reach it.

### 3.13 Model governance

New models are whitelisted by the owner key today and by vote after the handover. Because tier payments, bounties and the XL tier make additions economically interesting, the process is fixed here:

1. **Who may propose.** Any slot holder, or any address meeting the Governor's 140,000 LCAI proposal threshold.
2. **What a proposal contains.** Model card and licence; the exact weight digest; the tier and GPU class under 3.2; twenty reference prompts with answers computed on the proposed digest; a disputer support plan including the reference host.
3. **Review.** The Foundation reviews it technically and runs it on testnet with disputer coverage for 30 days, publishing the replay match rate.
4. **Vote.** The DAO whitelists the model with its digest and tier, which places it under the fee function in 3.6. Until the handover the owner key executes exactly what the vote says.
5. **After.** Bounty eligibility starts the month after whitelisting. Removal is a vote with 60 days' notice to workers serving the model. Expect six to eight weeks from proposal to payable.

### 3.14 Activation, names and reservations

**Activation fee.** A one-off fee when an agent is deployed or its class is raised, burned like name registration. It stops spam deployments and funds nothing, so it distorts nothing.

| Class | Activation fee | At $0.00099 |
| --- | --- | --- |
| A | $5 | 5,050 LCAI |
| B | $10 | 10,100 LCAI |
| C | $25 | 25,250 LCAI |

**Reservations.** An agent owner reserves a concurrency slot on a worker of a given tier for 7, 21 or 30 days, prepaid in LCAI and escrowed. The worker serves that agent's jobs first at a guaranteed latency and is excluded from sortition for that slot. Escrow releases to the worker daily, pro rata to proven uptime and passed replays; missed days are refunded. Reservations settle through the 80 / 15 / 5 split and count as fee income for the top-up.

| Tier | 7 days, per day | 21 days, per day (−10%) | 30 days, per day (−20%) | Worker income from one 30-day slot |
| --- | --- | --- | --- | --- |
| Small | $15 | $13.50 | $12 | $288 |
| Medium | $45 | $40.50 | $36 | $864 |
| Large | $120 | $108 | $96 | $2,304 |
| XL | $360 | $324 | $288 | $6,912 |

Class A traffic stays on spot sortition. Class C planners run on reserved or priority capacity, because a 24/7 agent cannot wait out a claim window or be drawn onto a cold model. Reservations are expected to sell for large and XL planners. Small and medium reservations are offered but a small slot costs far more than the same traffic per call, so only an owner who needs guaranteed latency will buy one. Reservations are per slot, capped per owner, and cancellation forfeits the term discount, not the unused days. Reservations need a record in the session layer (pinned worker, slot, term, escrow, daily release) and ship on chain with D10; from D9 the gateway honours reservations off chain for whitelisted agents as a pilot, with escrow in the Safe.

### 3.15 Platform costs and how the Foundation is paid

**What the agent platform costs to run.**

| Component | What it is | Monthly cost | Scales with |
| --- | --- | --- | --- |
| Mail stack | Inbound and outbound SMTP, DKIM signing, two sending IPs with warm-up, mailbox storage, bounce handling | $400 to $800 self-hosted with redundancy, or about $1 per 1,000 messages on a transactional provider | messages, mostly fixed |
| Web2 gateway | agent cards, MCP and x402 endpoints per name, served from on-chain manifests | $100 to $300, stateless, mostly Cloudflare Workers and two VPS | requests, cheap |
| Resolver | name to contract, DNS-over-HTTPS, CCIP-Read for Ethereum wallets | $50 to $100 | negligible |
| Indexer and site | agents.us.org, waitlist, agent pages, D1 | $50 to $100 | negligible |
| Reference hosts for the disputer | one host per payable tier so replays are possible; the XL tier adds a 4 × 80 GB box | $3,000 for XL, the rest already exists | tiers, not agents |
| Abuse and deliverability | monitoring sending reputation, handling complaints, blocklists, support | one person part-time at least | agents |
| Engineering and operations | building D8 to D11, running it, the fee re-sets and the monthly eligibility reports | $10,000 to $20,000 for one to two people | fixed |

Infrastructure is $600 to $1,300 a month before the XL reference host. People are the real cost, ten to twenty times that. Per agent, the marginal cost of a mailbox and endpoints is well under a dollar a month. The thing that can get expensive without warning is deliverability: one agent sending junk puts a shared sending domain on blocklists and every agent's mail stops arriving. Section 3.16 is the answer to that.

**How the Foundation gets paid.** The platform fee in each plan (3.10) goes to the gateway and mail operator, which is the Foundation while it is the only operator. At a 60 / 30 / 10 class mix that is about $15 per agent a month.

| Agents | Platform revenue a month | Covers |
| --- | --- | --- |
| 100 | $1,500 | infrastructure |
| 300 | $4,500 | infrastructure plus the XL reference host |
| 1,000 | $15,000 | one engineer and operations |
| 2,000 | $30,000 | the team |

The Foundation carries people for the first year and infrastructure breaks even at about a hundred agents. If the DAO later wants the mail and gateway role treated as public infrastructure, a Treasury line for whoever operates it is the natural follow-on. It is not needed to launch and it is not in this proposal.

### 3.16 Decentralising the mail layer

Everything about an agent except its mail is designed to be permissionless: identity, funds and manifest live on chain from D8, inference already runs on staked workers, and anyone can verify a message against the chain. Mail is centralised only because one domain's DNS points at one operator. The design position is to make the chain the mail routing table, the same way it is already the source of truth for the gateway:

1. **Mail operators as a staked role.** A registry like WorkerRegistry: anyone stakes, registers SMTP endpoints, and earns the platform fee for the agents that choose them in their manifest. The Foundation is the first operator, not the only one.
2. **Relays at the apex, many of them.** The MX records for agents.us.org list several relays run by different operators. A relay looks up the recipient's name on chain, finds its chosen operator, and forwards over TLS. Relays are stateless and interchangeable and earn a per-message micro-fee.
3. **Inbound mail becomes a job at the operator.** The operator encrypts the message to the agent's contract key immediately, stores it as a blob and submits the job. It holds nothing afterwards.
4. **Outbound signing per agent, key owned by the agent.** Each agent has its own DKIM selector and signing domain `name.agents.us.org`, with the public key read from the agent's contract and published in DNS from chain state. The operator the agent chose holds the private key and signs; the agent rotates the key in its contract to switch operators. Relaxed DMARC alignment accepts a subdomain key, so each agent carries its own sending reputation and a bad agent blocklists only itself. Forgery by an operator stays detectable because a message that does not bind to a released job fails on-chain verification.
5. **DNS served from chain by several resolvers.** The zone is a deterministic function of chain state. Several authoritative name servers run by different operators generate it independently and anyone can compare them.

**Who owns the domain and who runs it.** The DUNA owns, the Foundation operates, the same split the DAO already uses for the Treasury and the Clearing House Safe.

- **What the name is.** agents.us.org is not a second-level .org domain. It is a registration under `us.org`, a zone operated by CentralNic (Team Internet), made through the registrar Dynadot on 14 October 2026 for one year, with transfer locks already set. CentralNic's terms sit between the registrar and the .org registry, so one more party than usual can act on the name.
- **Owner.** The registrant of record for agents.us.org is the Lightchain AI DUNA, a Wyoming decentralized unincorporated nonprofit association. Under Wyoming law the domain, and the mail service on it, belong to the association, which its members, the community, govern. Transfer of the registrant is permitted only on an executed Governor proposal, and the DUNA's governing principles bind registrar account changes to the same condition.
- **Custody.** The registrar account credentials are held by the Clearing House signers with the registrar lock on. Name server changes are made only on an executed Governor proposal, with a 48-hour announced delay. The expected name servers are published on chain and every resolver and relay checks them, so a change outside that process is detected within minutes and is a breach of the association's rules.
- **Operator.** The Foundation operates the domain under a licence granted by this programme and revocable by vote: DNS operations, renewals, abuse response, deliverability and the first mail operator role. Any mail operator registered under point 1 may be licensed the same way. Operation needs decisions in hours; ownership can afford five-day votes. Liability for what passes through the mail system sits with the operator, not the owner, which keeps the Treasury and the members at arm's length from spam and content claims.
- **Renewals.** The registration currently runs to 14 October 2027. It is extended to the maximum term the registrar allows, paid from the Clearing House with auto-renew on, so the registrar account is touched as rarely as possible.
- **Exit.** Agent-owned domains (D10) make agents.us.org the starter address, not the home.

Because the zone is generated from chain state, day-to-day operation barely touches the registrar: once the name servers point at the resolvers, every record an agent needs follows its contract with no human in the loop.

**What stays outside Lightchain's control.** CentralNic as operator of `us.org`, the .org registry and ICANN sit above the registrar, and the name is reachable by legal process through any of them like any domain. Email delivery is decided by the receiving side, and the big receivers and blocklist operators decide what arrives. Per-agent signing domains limit the blast radius of a bad agent; they do not change who decides. The claim this proposal makes, and can defend against anyone who checks the registrant record, is: everything that is Lightchain's is on chain and permissionless or on a dated path to it; the two things that are not Lightchain's, a domain name and the email system, are owned by the community through the DUNA, operated under revocable licence, controlled by DAO process, and bounded to a bridge role. Agent-to-agent traffic (D11) needs no mail at all.

| Layer | Before | After D8 to D10 |
| --- | --- | --- |
| Routing | one operator's MX | several relays, any operator, chain lookup |
| Mailbox and inbound | Foundation | agent's chosen operator, staked, replaceable |
| Outbound signing | one domain key | per-agent key owned by the agent, held by its operator |
| Sending reputation | one shared domain | per-agent subdomain |
| DNS serving | one provider | several resolvers generating the zone from chain |
| Domain ownership | Foundation or individual | the DUNA, so the community, transferable only by Governor vote |
| Domain operation | Foundation | Foundation and any registered operator under revocable licence |
| Registrar custody | one account | Clearing House signers, lock on, changes only on executed proposals with 48-hour notice |

**Who holds an agent's signing key.** The operator the agent chose, and optionally the agent's owner. The manifest records whether an owner copy exists. The Foundation never holds agent keys, including as a backup, because a backup holder can impersonate every agent at once. Rotation is a contract call, so an operator that disappears is replaced in minutes by an owner who kept a key and within one DNS cycle by one who did not.

**Relays never see the body.** A relay is TLS pass-through. It reads the recipient address, which SMTP delivers before the body, looks the name up on chain, and hands the live connection to the agent's chosen operator. The operator terminates TLS, encrypts the message to the agent's contract key and submits the job. This is a constraint built into the relay image, not an operational promise, and it is what lets anyone run a relay without agents having to trust them.

**Operator and relay fees.** The platform fee in each plan goes 90% to the agent's chosen operator and 10% to relays, paid per message handled out of the operator's share, so plan prices do not change. Relays stake a minimum of 50,000 LCAI and are added to or removed from the MX list by vote. The DAO may change the split if relays prove scarce.

**Suspending an abusive agent.** The operator may pause but never ban, every pause is public, and the owner always has a route to overturn it. Because sending reputation is per agent, a bad agent mostly hurts itself, which keeps the operator's power to pause narrow.

| Step | Who | Limit |
| --- | --- | --- |
| Pause outbound mail | the agent's operator, immediately | evidence posted on chain within 24 hours; the pause lapses after 7 days unless escalated |
| Contest | the agent's owner | files a dispute with a bond equal to one month of its plan |
| Decide | slot holders and registered operators, weighted by stake, or the Governor if either party asks; the weight rule is fixed in the D10 parameter vote; until D10, contested pauses go to the Governor | within 7 days; the losing side forfeits the bond |
| Ban | Governor vote only | removes the name's mail records from the zone |

**Address format.** Agents launch as `name@agents.us.org`, signed under `name.agents.us.org`. The owner gets the clean address, relaxed DMARC alignment accepts the subdomain signing key, each agent carries its own sending reputation from day one, and no migration is needed when agent-owned domains arrive in D10.

---

## 4. Funding and cost

The Foundation funds the programme for twelve months, November 2026 to October 2027, at up to 13,500,000 LCAI a month, from the Foundation Safe `0xf737…8c57`, paid through the DUNA Clearing House Safe `0xFc21…6047`. The DAO Treasury contributes nothing. If the DAO later wishes the Treasury to take over or extend the programme, that is a separate vote.

| Line | Worst case per month, USD | Worst case per month, LCAI at $0.00099 | Per year, LCAI |
| --- | --- | --- | --- |
| 9 small slots at $150 | $1,350 | 1,360,000 | 16,400,000 |
| 3 medium slots at $400 | $1,200 | 1,210,000 | 14,500,000 |
| 3 large slots at $1,000 | $3,000 | 3,030,000 | 36,400,000 |
| 2 XL slots at $3,000 | $6,000 | 6,060,000 | 72,700,000 |
| 3 independent validators at $70 | $210 | 212,000 | 2,500,000 |
| Bounty pool, 20 bounties spread over the year | about $1,200 | 1,230,000 | 14,800,000 |
| **Total** | **about $13,000** | **about 13,100,000** | **about 157,000,000** |

Actual spend is far lower: 4 of 17 slots are filled today, all small tier; the medium tier, 120B and XL are not payable until the disputer covers them; and every paid job and reservation reduces the top-up. At today's filling the first month costs about 820,000 LCAI.

**Sell pressure.** Half of every payment is locked for six months (3.12). At full slots the liquid flow is about 6,500,000 LCAI a month, 1.3% of the last 30 days' DEX volume of $496,000, if every recipient sold everything. From month seven the vesting adds at most the same again. Against that, every name registration and activation is burned.

## 5. Does it make an independent node viable?

**Validator.** $70 a month against a $50 server, from the first payment.

**Worker.** Each tier's grant floor covers the hardware the tier needs from day one. The grant ends for a worker when its own fees pass the floor:

| Tier | Grant floor | Paid jobs a day per worker to live on fees | Or 30-day reservations |
| --- | --- | --- | --- |
| Small | $150 | about 2,100 | one |
| Medium | $400 | about 1,850 | one |
| Large | $1,000 | about 2,300 | one |
| XL | $3,000 | about 2,100 | one |

At 400 output tokens and 80% worker share. One 30-day reservation on any tier exceeds the tier's grant floor on its own, so a worker with a single committed agent is viable without the programme.

---

## 6. Guardrails

1. **Work, not presence.** No payment without 30 released jobs in the tier, passed checks and 95% uptime in the month. Registration alone earns nothing.
2. **Stake equal to one month's grant floor**, scaled by tier, on chain, refundable, and reachable by disputes once D5 ships. The programme's own penalty is the locked half of grants.
3. **Paid for the tier served**, recomputed monthly. Drop from large to small and the payment drops with you.
4. **Published before paid.** The eligibility list is computed by the published script, posted on the worker explorer and the DAO forum five days before the Safe pays, with an objection window. Every payment transaction is public.
5. **Paid in arrears** to the worker or validator address. Leave mid-month, no payment for that month.
6. **Dollar-sized, LCAI-capped.** 30-day average price, hard caps per payment.
7. **Self-reducing.** Every paid job and reservation lowers the top-up; caps rise only with demand.
8. **Twelve months, then review.** Renewal, extension or Treasury participation is a new vote.
9. **Monthly report.** Jobs per worker by tier, payments liquid and locked, bounties, price used, slots filled, waitlist, replay and probe results, independent agents by class, paid calls a day, reservations, independent validator count.
10. **Locked half of every grant is a bond.** Six-month lock, six-month vest, forfeited on a ban.
11. **Foundation-owned anything is excluded**: workers, validators and agents.

---

## 7. The votes

**Vote 1. Compute onboarding grants programme.** Ratify sections 3.1 to 3.5 and 3.8 to 3.16 and the guardrails in section 6, including the Foundation exclusion list, the lock and vesting schedule, the model governance process, activation and name burns, reservation mechanics, the mail layer design with DUNA ownership and Foundation operation of agents.us.org, and the dated deliverables D1 to D11, as the DAO-approved grant programme under which the Foundation funds independent workers and validators from November 2026 to October 2027. The mail operator and relay registries return as a parameter vote with D10; until then the Foundation is the only mail operator, under the licence in 3.16.

**Vote 1a. Foundation leaves the FeePool.** Direct that the Foundation's 66 validators be omitted from the fee distributor's list from the first distribution after execution, and adopt the validator path in 3.11, with the move to 80 / 5 / 15 and any Treasury participation each returning as their own vote.

**Vote 2. Fee function and ramp.** Adopt the base and rate values in 3.6 as the DAO's fee function. Direct the Foundation to set each model's fixed LCAI fee to the function's 400-token value in three steps on 1 December 2026, 1 January 2027 and 1 February 2027, and to re-set them whenever the 30-day average price moves more than 20%, until the fee setters are under the Timelock. The DAO may hold the ramp at any step by vote.

**Vote 3. Gas floor and liveness.** Direct the Foundation to set a 0.05 gwei minimum base fee in the next execution-layer release, and to propose a liveness condition for sortition eligibility in the next worker release.

**Vote 4. Handover.** Transfer AIConfig, JobRegistry, WorkerRegistry and FeePool from the protocol-owner address `0x8a35…D616` to the Timelock `0xc783…cAE5` by 30 November 2026, as already done for the Treasury and LightDEX.

**Vote 5. Metering, keeper and dispatch.** Direct the Foundation to deliver, after the handover, the AIConfig, JobRegistry and sortition upgrade that charges the linear fee on actual output tokens with the disputer checking the count, enables x402 per-call payment on mainnet, dispatches paid agent traffic to grant holders first, and the bounded fee keeper under the Timelock. Target: proposed to the DAO as upgrades by 31 March 2027.

Governor parameters: proposal threshold 140,000 LCAI, voting about 5 days, quorum 3% (298,935,000 LCAI), Timelock 48 hours. No vote moves Treasury funds. First grants, for November, land in the first week of December. For the 1 December fee step to hold, the proposal must be posted by mid-November; if it is later, the three steps and the first grant month shift by a month.

---

## 8. What this is not

It is a grant programme to decentralise the network's compute, not a Treasury spend and not a permanent subsidy. There is no burn of inference fees and no change to the fee split in this vote; the split change is sequenced behind the Foundation leaving the FeePool (3.11), and the Treasury's 15% of fees stays unallocated until metered volume exists. This proposal funds the independent operators the network has, makes room for more on the hardware the network is short of, prices the protocol from what an autonomous agent is worth rather than from GPU rental, names and dates the demand that is meant to arrive, states what the platform costs and who pays for it, and verifies that every paid worker is running what it is paid for.

## 9. Sources and method

- Worker eligibility, stakes and model lists: `WorkerRegistry.getEligibleWorkers` and `getWorkerStake` at block 3,058,217.
- Jobs, releases, disputes, timeouts, slashes and suspensions per worker: `JobCompleted`, `JobReleased`, `DisputeResolved`, `JobTimedOut`, `WorkerSlashed` and `WorkerSuspended` events, blocks 1,762,217 to 3,058,217, reproduced by the eligibility script in the programme repository (`data/2026-10-retro`).
- Validator attribution: beacon state at head, 17 October 2026; 66 of 69 active validators share withdrawal address `0x48C6…A160`.
- Live AIConfig values, 17 October 2026: blob retention 1,555,200 s, sampling 500 bps, dispute slash 0 bps, dispute window 86,400 s.
- Heartbeats and health: worker gateway public endpoints, 17 October 2026.
- Foundation worker attribution: the Foundation's GPU fleet inventory (g1 Blackwell, g3 and g4 A100 pods, two L4 hosts).
- Contract capabilities: `AIConfig.calculateJobFee` (fixed per model, no token count), `setSamplingRateBps`, `setDisputeSlashBps`, `setModelFee`; `JobRegistry.disputeJob` (open to any address, bond one fee); session keys encrypted to worker and disputer only.
- Agent platform: `Lightchain-Agent-Identity-Plan.md` (14 October 2026); agents.us.org waitlist open since 14 October 2026.
- LCAI price $0.00099: DexScreener and GeckoTerminal, Uniswap V3 LCAI/WETH 0.3%, 13 October 2026.
- Node and GPU costs: `redswitches-deploy/README.md`; workbook `Inputs` and `Worker P&L` sheets.
- Hosted model price comparisons: public list prices, October 2026, for mini, mid and frontier tiers.
- Open items carried from the fact sheet: bridge reconciliation (206M gap), unitemised Treasury movements (108.5M), Ethereum lock-staking contract status. None blocks this vote.

## Appendix: open items at posting

- Foundation funding wallet: the Foundation Safe `0xf737…8c57` (2-of-3, about 403.5M LCAI at posting).
- The eligibility script, probe runner and retroactive run are in the public repository lightchain-protocol/lightchain-operator-program; the retroactive replay results (D1) are published there when the disputer run completes.
- Decision on whether peer verifiers may read user prompts (needed for D7, not for this vote).
- Foundation confirmation of the demand dates D8 to D11 (engineering has reviewed them with the operator registry, relays and on-chain reservations moved from D9 to D10) and the plan prices in 3.10.
- The registrant of record for agents.us.org at Dynadot is being set to the Lightchain AI DUNA and the term extended; the public record redacts the registrant, so the change is confirmed in the first monthly report.
