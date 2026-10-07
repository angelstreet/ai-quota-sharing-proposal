# Quota Share — submission drafts

Prepared 7 October 2026. Drafts only; nothing published.

## OpenAI / Codex feature-request issue

**Title:** Opt-in community quota sharing with borrowing caps and reciprocal contribution

When I exhaust my included Codex allowance, my work stops even though other subscribers may have unused eligible capacity. Could OpenAI offer a provider-managed community quota pool across eligible Codex and ChatGPT surfaces?

Members would opt in under Settings → Usage, choose a contribution percentage such as 20%, and set a monthly borrowing cap. At allowance exhaustion, an eligible member could explicitly request a bounded allocation from compatible unused capacity.

The reciprocity rule is central: borrowing 100,000 units without existing contribution credit creates a 100,000-unit give-back obligation. The following month, borrowing stays paused until that amount has actually been contributed to the pool. Contributors earn redeemable credit to request capacity later, subject to supply. Merely offering quota does not earn credit.

Suggested UI: enable/pause toggle, contribution percentage, personal reserve, borrowing cap, contributed/borrowed balances, repayment progress, and explicit confirmation before borrowing. Attached concept images and the specification illustrate these states; they are not existing product functionality.

This needs provider-side entitlement transfers and settlement, not account or API-key sharing. Model-weighted units and existing safety/throughput controls must be respected. I recognize that the open-source CLI cannot implement ChatGPT billing or web settings by itself. I am submitting a feature request, consistent with the repository's current contribution policy, rather than a code PR.

A first pilot could stay within one compatible OpenAI allowance pool. Measure fill rates, repayment delays, donor exhaustion and compute cost before widening eligibility.

## Anthropic product proposal

**Title:** Community quota sharing for Claude and Claude Code

Could Claude offer an opt-in quota pool under Settings → Usage, shared across eligible Claude and Claude Code usage?

The proposal lets members contribute up to a chosen fraction of unused eligible allowance, such as 20%, and borrow within a monthly cap when their included allowance is exhausted. Borrowing 100,000 units creates an equal contribution requirement before borrowing again the next month. Actual settled contributions count, not unconsumed offers. Contributors earn credit to request capacity when they need it, subject to availability.

The attached design concepts show settings, borrowing consent and repayment progress. This would require an Anthropic-managed entitlement ledger, model-weighted accounting and server-enforced limits. No credential sharing or third-party account routing is proposed. A single-provider pilot would establish feasibility before any cross-provider federation.

## X — short post

Sharing is caring. What if AI quota worked that way?

Lend spare quota. Borrow when you hit your limit. Give back what you borrow before borrowing again next month.

An opt-in feature proposal for AI providers. Would you join?

https://github.com/angelstreet/ai-quota-sharing-proposal

## LinkedIn — approved post

Sharing is caring. What if AI quota worked that way?

You hit your AI usage limit halfway through a project. Another subscriber has spare allowance they won’t use.

I propose an opt-in quota-sharing feature for ChatGPT/Codex, Claude/Claude Code, and Mistral’s Le Chat.

Choose how much you lend—say 20%—and set a borrowing cap. Borrow 100,000 units this month? Contribute 100,000 before borrowing again next month.

Each provider would manage its own pool, keeping accounts and conversations private.

I’ve created concept mockups showing how this could look in settings.

Would you share your spare quota?

Proposal and mockups: https://github.com/angelstreet/ai-quota-sharing-proposal

## Posting notes

Attach the concept mockups and add the public proposal link when available. The X draft is 226 characters before adding a link. For a provider-specific post, name the relevant product and attach its mockup. Verify account tags before publishing. Nothing has been sent or published.
