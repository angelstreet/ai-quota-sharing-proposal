# Community Quota Sharing

Product proposal · 7 October 2026 · Working name: Quota Share

## Idea

Let subscribers opt into a provider-managed pool of unused AI allowance. Members choose how much they can contribute, for example 20%, and a monthly borrowing cap. When they exhaust an eligible included allowance, they can request capacity from the pool. Contributors earn the right to request capacity later; borrowers must give back before repeatedly borrowing.

Start with two independent implementations: OpenAI for Codex and eligible ChatGPT surfaces, and Anthropic for Claude Code and Claude. Use the same product pattern across providers. Cross-provider exchange is a later option requiring agreements and explicit conversion rates, not a capability of this initial proposal.

## What exists and what is proposed

Codex CLI is Apache-2.0 licensed. Its contribution guide currently rejects external code PRs and welcomes feature requests through issues. This repository is not the source for the ChatGPT web interface or its billing service. Claude Code's public repository license reserves all rights and points to Anthropic commercial terms; a public repository does not establish an open-source application.

Current official documentation describes allowances, resets and additional paid usage. The sources reviewed do not document person-to-person subscription quota transfers. This proposal needs new provider-side entitlement and billing support; it cannot be enabled by swapping accounts, sharing API keys or modifying a client alone.

## Units and scope

The user's example uses 100,000 tokens. For a pilot with one model and token class, that can be a literal amount. For a general product, use provider-defined quota units and show token estimates separately. Different models, input/output tokens, cached tokens and tools have different costs. A raw token in one provider is not interchangeable with a token in another.

Each balance is scoped to provider, eligible allowance pool, model class and applicable reset window. Sharing addresses exhaustion of transferable included allowance, not context length, safety limits, requests-per-minute controls or a platform-wide capacity outage. Billing settlement can be monthly even where available capacity expires within shorter windows. Unused capacity still expires; earned contribution credit and outstanding obligation are separate ledger entries.

## Proposed rules

1. Sharing is off by default. Members explicitly enable it and choose a percentage from 0–20% in the initial pilot. Twenty percent is a proposed pilot ceiling, not a current provider policy.
2. The percentage applies to the provider's measurable eligible allowance in each reset window. Never pretend a dynamically metered plan has a fixed token allowance. The provider must expose a safe transferable amount before launching that plan.
3. A member's own usage has priority over unallocated quota. A request may reserve only currently unused eligible units within the member's cap. Already settled transfers cannot be reclaimed. Clearly display capacity already lent and remaining personal capacity.
4. Offering capacity is not contributing it. Only units actually consumed and settled by the pool earn credit or discharge an obligation. Unused reservations are released.
5. A verified new member receives one bounded initial borrowing opportunity, subject to their cap and pool availability. This bootstrap rule is an assumption needed to make a first borrow possible without prior contributions.
6. Existing positive contribution credit can be redeemed for borrowing. After credit is exhausted, bounded borrowing may create a give-back obligation. Credit used for a borrow is retired, so it cannot be reused to repay the same borrow.
7. At the next billing month, any unpaid obligation blocks new borrowing until an equal amount of contribution has actually settled. The obligation persists across months; resetting the calendar does not erase it. A contribution first reduces obligation, then earns new redeemable credit.
8. Lending grants eligibility to request later, not guaranteed immediate supply. All requests are subject to available units, account eligibility and capacity constraints.
9. Members can pause or disable future sharing at any time. This stops new allocations. Already consumed transfers and unpaid obligations remain recorded; disabling does not create a cash charge or cancel the subscription.
10. Borrowing requires an explicit confirmation by default. No automatic purchase or paid fallback. A separate opt-in automatic borrowing option could follow after a pilot.

## The 100,000-unit example

Alice enables 20% sharing and a 100,000-unit monthly borrowing cap. In October, she borrows and consumes 100,000 units without existing contribution credit. Her obligation becomes 100,000. In November, she cannot borrow again until 100,000 units of her own eligible quota have been used by the pool. At 60,000 contributed, the screen shows 40,000 remaining. At 100,000, the obligation is cleared and she may request another capped allocation if supply exists.

Bob lends those units in October and receives 100,000 contribution credits. When Bob later hits his limit, he may request up to that credit balance within his borrowing cap. Another member can supply it; Alice does not repay Bob directly. Bob's credits are retired as he consumes the borrowed quota.

If Alice offers 100,000 but nobody uses it, her obligation is unchanged. This can keep her blocked during low demand. The pilot should make this limitation clear and measure it; changing repayment to count offers would weaken the reciprocity rule and needs a separate product decision.

## Settings and screens

### Claude desktop — integrated concept

![Claude desktop Usage settings with community quota sharing](mockups/claude-sharing-settings.png)

This version follows the supplied Claude desktop dark-mode screenshot. It adds sharing controls beneath the existing usage bars, a 20% contribution setting, a 100,000-unit monthly borrowing cap, and a 60,000/100,000 repayment example. Generated interface copy is illustrative: the authoritative contribution percentage applies to each eligible reset window, even though the image mentions monthly quota. The remaining personal allowance is reduced by settled lending, and borrowing remains subject to compatible supply.

The included Claude mockup is a design exploration, not a screenshot of shipped functionality.

| Screen | Proposed location | Controls and feedback |
| --- | --- | --- |
| Codex sharing settings | Codex / Settings / Usage / Quota sharing | Enable toggle, share percentage, personal reserve, monthly borrowing cap, contribution and borrowing balances |
| Claude sharing settings | Claude / Settings / Usage | Same controls; obligation progress and borrowing-paused state; settings also govern eligible Claude Code usage |
| Borrow confirmation | Eligible allowance exhaustion notice | Available pool, remaining cap, requested amount, give-back requirement, explicit consent, borrow or wait |

For a CLI, propose `/quota status`, `/quota sharing on`, `/quota sharing off`, and `/quota borrow <units>` only after backend support. These commands are proposed, not existing commands. Account-wide controls should remain consistent across supported interfaces.

Additional states: off; enabled without available supply; eligible to borrow; repayment required; cap reached; request partially filled; reservation expired; provider unavailable; account/admin ineligible. Each state should explain the next available action. A zero-supply screen must not promise a continuation.

## Provider-side implementation

Keep prompts, code, conversations, account credentials and inference routing inside the normal provider account. Contributors see deidentified quota transactions, never another member's content. Request routing remains under the borrower's identity; billing entitlement is transferred by the provider.

The authoritative service needs enrollment/preferences, eligible-allowance introspection, contribution offers, atomic reservations, consumption settlement and an append-only reciprocity ledger. Reserve at most the minimum of available donor quota, donor share cap, recipient remaining monthly cap, recipient credit/approved bootstrap allowance, and available compatible pool capacity. Debt-bearing follow-on borrowing must also satisfy the previous-month repayment gate.

Use idempotency keys and transactional settlement to prevent double spending. Streamed and interrupted tasks settle actual metered consumption and release unused reservations. At window expiration, revoke unused reserved capacity without generating credit. Apply model-specific conversion rules before both sides of a transaction are committed. Provider-side controls must enforce all caps even if a modified client submits a larger request.

Pilot within one provider and one compatible allowance class first. Restrict enterprise participation to explicit admin enablement and contractual eligibility. Prevent repeated bootstrap access through account abuse. Define audit retention, dispute handling and the treatment of earned credit on subscription cancellation before launch. No cash redemption is proposed.

## Acceptance checks

- A disabled account cannot donate or borrow.
- A donor configured at 20% cannot transfer more than the eligible-window share cap, including concurrent requests.
- A request cannot exceed the recipient's remaining monthly cap or compatible supply.
- Offering unused quota does not earn contribution credit.
- Borrowing 100,000 in October blocks November borrowing until 100,000 of repayment contribution is settled.
- Pausing sharing stops new reservations while preserving settled balances.
- Cancelled tasks release unused units and settle consumed units once.
- Switching devices cannot bypass caps; models with different weights cannot create artificial credit through conversion.
- Contributors cannot access borrowers' data or credentials.
- No available pool produces a truthful waiting state with normal reset options.

## Rollout and evaluation

Run an opt-in pilot with a small bootstrap cap, a 20% maximum contribution and explicit borrowing confirmation. Track request fill rate, time to repay, blocked borrowers despite offered quota, donor limit exhaustion, abandoned reservations, complaints and incremental compute cost. Set stop criteria before launch. Pooling increases actual utilization; it does not create extra compute or guarantee relief during peak demand.

## Submission route

Mistral / Le Chat: include as a third independent provider proposal. Start with Le Chat subscription allowance; developer-tool support can follow if Mistral exposes a compatible entitlement pool. Mistral's official help page invites public feedback through its Discord and documents the authenticated help-widget route. Open-weight models do not make Le Chat's billing service open source or subscription capacity transferable. No Mistral implementation, quota-transfer support or cross-provider exchange has been verified. See the outreach guide for submission steps.

OpenAI: submit a product feature-request issue to `openai/codex`, clearly noting that billing and ChatGPT UI work are provider-owned. No upstream PR is prepared because the current contribution policy excludes external PRs. A client-only patch would not deliver this feature.

Anthropic: use a product proposal or social post. Do not treat the Claude Code public repository as permission to modify or publish a derivative of its proprietary implementation. The social drafts are prepared separately. Provider submissions and social posts are managed separately from this repository.

## Sources checked on 7 October 2026

- https://github.com/openai/codex — public client repository and Apache-2.0 license.
- https://github.com/openai/codex/blob/main/docs/contributing.md — issues accepted; external code PRs not accepted.
- https://github.com/anthropics/claude-code/blob/main/LICENSE.md — all rights reserved; commercial terms.
- https://help.openai.com/en/articles/11369540-using-codex-with-your-chatgpt-plan — current allowance and continuation options.
- https://support.claude.com/en/articles/12429409-manage-usage-credits-for-paid-claude-plans — Claude/Claude Code usage-credit behavior and usage settings.

## Mockup generation brief

Three AI-generated desktop UI concepts: dark Codex settings with 20% contribution and 100,000-unit borrowing cap; warm Claude usage settings with 60,000/100,000 repayment progress; dark borrowing confirmation for 25,000 units. Every image is instructed to show a concept badge and an illustrative-unit/provider-support footer. Exact behavior is governed by this document, not generated image typography.
