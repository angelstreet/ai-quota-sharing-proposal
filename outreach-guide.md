# Quota Share: step-by-step outreach

Prepared 7 October 2026. Nothing has been sent or published.

## Recommended order

1. Create one public home for the proposal: a GitHub repository under your account, for example `ai-quota-sharing-proposal`. Upload the proposal, the Claude mockup, and outreach drafts. Keep their filenames together so the image renders. State prominently that this is an independent concept requiring provider support.
2. Submit one provider-specific feature request per provider through the routes below. Search for existing requests first and add evidence to a matching request rather than duplicating it.
3. Publish one X post per provider, with its relevant mockup and a link to the public proposal. Publish a broader LinkedIn post once, or use the provider-specific drafts for separate posts.
4. Ask one relevant public contact per provider where to route it. Link the existing proposal; do not send the whole specification as a cold message.
5. After 7–10 business days, make at most one follow-up with new evidence or a concise routing question. Track links, dates, replies and requested next steps.

## GitHub

### OpenAI / Codex

1. Open https://github.com/openai/codex/issues.
2. Search `quota sharing`, `usage sharing`, `token sharing` and `community quota`.
3. If there is a matching request, comment with your concrete use case and mockup. Otherwise choose New issue and the available feature-request option; follow the displayed template.
4. Use the OpenAI issue draft in `submission-drafts.md`. Link the full specification and attach the Codex concept image if desired.
5. Explain that the billing service and ChatGPT settings are provider-owned dependencies. Ask whether a pilot is worth exploring.
6. Copy the issue URL into your public post. Do not open a PR: the current Codex contribution guide explicitly excludes external PRs.

### Anthropic / Claude Code

1. Open https://github.com/anthropics/claude-code/issues.
2. Search the same terms and inspect the current issue templates.
3. If a feature-request template is offered, use it and adapt the Anthropic draft. Make clear that this concerns Claude Code continuation plus account-level Claude Usage settings.
4. Attach `claude-sharing-settings.png` and link the full proposal.
5. If the template or scope does not fit an account/billing proposal, use Claude support or the developer Discord linked in the repository instead. A proprietary license does not prevent asking for a feature.

### Mistral / Le Chat

Use Mistral's official feedback community or support route first. Do not file a Le Chat subscription-billing request in an unrelated model or SDK repository. No appropriate Le Chat billing-source repository was established during this research.

## X / Twitter

1. Open your account and compose a new post.
2. Paste the short X draft from `submission-drafts.md`; adapt the product name if targeting one provider.
3. Attach the relevant concept screenshot. Keep its concept label visible. For Mistral, use the Claude screenshot only as an explicitly labeled example of the general idea, not a Mistral UI; better to post text until a Mistral-specific mockup exists.
4. Add your public proposal link. Review the final composer length after adding the link.
5. Mention only the relevant company account after confirming its identity through the company's website. Optionally mention one relevant product contact after checking their public profile.
6. Publish and copy the post URL to your tracker.

For Mistral, use the same short opening and name Le Chat when adapting the draft.

## LinkedIn

1. Choose Start a post on your profile.
2. Paste the approved LinkedIn post from `submission-drafts.md`.
3. Attach the Claude concept image for a Claude-specific post, or the provider-specific concepts for the wider proposal.
4. Link the public proposal and the relevant issue where one exists.
5. Ask one useful question: 'Would you contribute 20% of unused eligible allowance, and what borrowing cap would feel fair?'
6. Tag the verified company page. Tag a person only when their product role is relevant.
7. Publish, save the link, and turn substantive feedback into an updated proposal rather than repeatedly reposting it.

For a wider post, say: 'I am exploring the same opt-in quota-sharing pattern for OpenAI, Anthropic and Mistral, with separate provider-managed pools initially.' Do not imply cross-provider transfers exist.

## Support, email and community routes

| Provider | Verified route | What to do |
| --- | --- | --- |
| OpenAI | https://help.openai.com/ | Open the bottom-right chat bubble, identify this as product feedback, paste the short proposal and ask whether it can be routed to the Codex/usage product team. |
| Anthropic | https://support.claude.com/en/articles/9015913-how-to-get-support | Follow the current account-support instructions and submit the proposal as product feedback. The developer Discord is also linked at https://github.com/anthropics/claude-code. |
| Mistral | https://help.mistral.ai/en/articles/347458-how-do-i-contact-support | Sign in, open the help widget, choose Messages → Send us a message. For public feedback, join the official Discord through the link on this page and follow its channel rules. |

No verified personal email address or product-feedback email inbox was found for the named people. Use these official routes, an existing contact, or an address explicitly published for this purpose. The email below also works as a support-ticket message. Support can route feedback; it does not promise a response from the product team.

## Relevant public contacts

| Contact | Evidence of relevance | Suggested first approach |
| --- | --- | --- |
| Boris Cherny | Anthropic's official webinar identifies him as Head of Claude Code. https://claude.com/resources/webinars/claude-code-service-delivery | A concise reply to a relevant public feedback post; public X profile: https://x.com/bcherny. Ask whether GitHub or the account-product team is the right destination. |
| Alexander Embiricos | His public OpenAI LinkedIn profile shares Codex/ChatGPT product discussion. https://www.linkedin.com/in/embirico | A brief LinkedIn message if messaging is available, or a comment on a relevant product post. Verify the current profile before sending. |
| Mistral community/support team | Mistral explicitly invites public feedback in its official Discord. | Post to the designated feedback channel and ask for the appropriate Le Chat product contact. No individual has been verified as the appropriate recipient. |

These are relevant contacts, not a claim that they read every message or accept unsolicited pitches. Do not guess email addresses or imply a prior relationship.

## Direct-message draft

Hi [Name], I've drafted an opt-in quota-sharing idea for [product]: users lend a capped portion of spare allowance and can borrow when they hit their limit. Borrowing creates an equal give-back requirement before borrowing again next month. I made a settings mockup and documented the provider-side billing dependency. Is [GitHub issue / support feedback] the right route for this? Proposal: [public link].

## Email / support-message draft

**Subject:** Product proposal: capped, reciprocal quota sharing for [product]

Hello [team/name],

I would like to propose an opt-in pool for unused eligible [product] allowance. Members would choose a contribution percentage, such as 20%, and a monthly borrowing cap. When their included allowance runs out, they could request compatible capacity from the pool.

The rule is reciprocal: borrowing 100,000 units creates a requirement to contribute 100,000 before borrowing again the following month. Contributors earn credit to request capacity later, subject to supply.

I've prepared a concept settings screen and a specification covering model-weighted accounting, repayment, caps and privacy. This would require provider-side entitlement support; no account or API-key sharing is proposed.

Could you route this to the team responsible for usage and subscription experience, or point me to the preferred feedback channel?

Proposal: [public link]

Thank you,
Joachim

## Should Mistral be included?

Yes: add Mistral's Le Chat as a third independent proposal. Ask whether they would consider a capped reciprocal-sharing pilot, rather than assuming their current subscription allowance is transferable. The common specification can be reused, but a Mistral-specific interface mockup remains future work. Open-weight model releases and open-source developer tools do not establish that the hosted Le Chat interface or billing backend is open source.

## References

- https://github.com/openai/codex/blob/main/docs/contributing.md
- https://github.com/anthropics/claude-code — feedback, issues and developer Discord.
- https://help.openai.com/en/articles/6614161-how-can-i-contact-support
- https://support.claude.com/en/articles/9015913-how-to-get-support
- https://help.mistral.ai/en/articles/347458-how-do-i-contact-support
- https://claude.com/resources/webinars/claude-code-service-delivery
- https://www.linkedin.com/in/embirico
