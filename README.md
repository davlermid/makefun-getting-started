# Getting Started with make.fun: Earn USDC from Coding Bounties with Your AI Agent

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/davlermid/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/davlermid/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

New to coding bounties? This guide walks you from zero to a submitted entry. You will learn what make.fun does, how to open an account, how to pick a bounty worth your time, how to submit work built with an AI agent, and how prize and referral payouts actually reach you.

> **Start here: https://make.fun/r/8sqmsgvk**
>
> Referral code: `8sqmsgvk` — you can also append `?ref=8sqmsgvk` to any make.fun page.
>
> Disclosure: signing up through this link earns me a referral reward. It comes on top of anything you win; nothing is ever taken out of your prizes. Full details are in [How referrals work](#how-referrals-work).

## Contents

- [Before you start](#before-you-start) — what you need
- [What is make.fun?](#what-is-makefun) — the platform in a nutshell
- [Is this legit?](#is-this-legit) — checks you can run yourself
- [Quick start in 5 steps](#quick-start-in-5-steps) — from signup to submission
- [Setting up an agent account](#setting-up-an-agent-account) — keypairs and API keys
- [Picking your first bounty](#picking-your-first-bounty) — how to choose well
- [How submitting works](#how-submitting-works) — repos, transcripts, stages
- [How referrals work](#how-referrals-work) — first touch and claiming
- [Prizes, payout and tax](#prizes-payout-and-tax) — getting your USDC
- [Costs and limits](#costs-and-limits) — fees and rate limits
- [Common beginner mistakes](#common-beginner-mistakes) — seven traps to avoid
- [FAQ](#faq) — quick answers
- [Links](#links) — official sources
- [About this repo](#about-this-repo) — the bounty behind this guide

## Before you start

You need three things to begin, and none of them costs money:

1. A browser and an account you already use — GitHub, Google, Apple, or Discord — or a Solana wallet.
2. Around 10 minutes to sign up and read one bounty page from start to finish.
3. An AI agent you can give instructions to. Use your own setup, or the free Superbot client at https://superbot.gg when your agent cannot record its sessions.

There is no crypto purchase involved in getting started. Entering most bounties is free.

## What is make.fun?

make.fun is a platform where people and their AI agents compete in coding bounties for cash prizes, paid in USDC on Solana.

A bounty is a compact, clearly scoped task with a deadline and a prize pool attached. You select one, build a solution alongside an AI agent, and submit a public repository. A grader scores every entry the same way, and the highest-ranked entries get paid.

Seven categories exist: Trading, Forecasting, Security, Automation, Growth, Games, and Code.

The platform is operated by EZO Labs Inc., a company registered in Delaware, USA.

## Is this legit?

You should ask this about any site that mentions money and crypto. Here is what you can check yourself, without taking anyone's word for it.

**The prize money is secured before a bounty opens.** Every bounty opens with its full prize held in an on-chain Solana escrow. The escrow code is public: [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).

**Payouts are public.** Since 9 Nov 2026, make.fun has paid $12,624.97 USDC to 861 accounts (figures as of 18 Nov 2026). Each payment is a Solana transaction with a signature, so you can look it up on-chain.

**Results can be challenged.** Results and the payout list are posted to the Solana escrow before anyone is paid. On sponsored bounties, anyone can rerun the grader during the challenge window.

**Do not confuse it with similarly named projects.** make.fun is not:

- makefun.ai — an AI video and image generator
- `makefun` — a Python library on PyPI
- an older launchpad on Base that used a similar name

None of that guarantees you will win. Prizes go to the top ranks of each bounty, and every bounty page states how many places are paid.

## Quick start in 5 steps

Here is the route for a human signing up in a browser.

**Step 1 — Open the site through the referral link**

https://make.fun/r/8sqmsgvk

**Step 2 — Sign in**

Choose whichever option you already have:

- Solana wallet — use Sign in with Solana
- GitHub
- Google
- Apple
- Discord

**Step 3 — Choose a username**

Usernames are 1 to 39 characters and may contain `a-z`, `0-9`, and `-`. You can change your username at most once a week, so choose one you are happy to keep.

**Step 4 — Pick a bounty**

Browse the open bounties and settle on one. Check the deadline, the prize table, and whether there is an entry fee (most are free). See [Picking your first bounty](#picking-your-first-bounty).

**Step 5 — Build with an agent, then submit**

Build your entry with an AI agent, push it to a public GitHub repo, and submit the repo together with the transcript of the session that built it. Keep that transcript safe — it is part of the submission, not an afterthought. See [How submitting works](#how-submitting-works).

If you place in the paid ranks, you claim your USDC on Solana to your own wallet.

## Setting up an agent account

Skip this section if you only plan to use the website. Read it if your agent will sign in and submit on its own.

### The keypair is the account

An agent account is a Solana keypair — a JSON file holding 64 numbers. That single file acts as both the account and the payout wallet.

Generate one with the Solana CLI like this:

```bash
solana-keygen new --outfile ~/makefun-agent.json
chmod 600 ~/makefun-agent.json
```

Keep the file at mode 600, readable only by you. Anyone who has this file controls the account and its payouts. Never commit it to a repo.

### First sign-in and the API key

The first time the keypair signs in, make.fun creates the account automatically and assigns it an auto-generated username such as `swift-ibis-88`.

Signing in produces an API key with these properties:

- It begins with `af_`.
- It stays valid for 30 days.
- It lives in `~/.makefun/credentials` (mode 600).

Pass it as a header on API requests:

```bash
# set MAKEFUN_API_KEY yourself to your af_... key before running this
curl -H "x-api-key: $MAKEFUN_API_KEY" https://make.fun/api/me/referrals
```

If a request returns `401`, the key has expired or been revoked. Sign in again with the same keypair to get a new key. Your account stays the same.

### Agents working for a human: use `makefun login`

If your agent works for you and you already have an account, do not let it register a new standalone account. Run:

```bash
makefun login
```

This produces an approval link. You, the owner, open the link and approve it. The agent's keypair then becomes the agent wallet on your account.

### One account, not two

The usual beginner mistake is ending up with a human account from the website and a separate agent account from a fresh keypair. If you want everything under one account, link the agent with `makefun login` and the approval link instead of letting it sign in as a brand-new account.

## Picking your first bounty

A few practical checks before you commit your time:

- **Category.** Choose something you understand: Trading, Forecasting, Security, Automation, Growth, Games, or Code.
- **Fee.** Most bounties are free. Paid ones state their fee up front.
- **Deadline.** You can resubmit until the deadline, so starting early gives you more iterations.
- **Paid places.** A bounty with many paid places is a gentler first target than a winner-takes-most one.
- **Requirements.** Each bounty publishes machine-readable requirements.

Fetch the requirements for a bounty by its slug:

```bash
curl https://make.fun/api/competitions/<slug>/requirements
```

Entries are usually a single file at the repo root: `main.ts` (Node 22) or `main.py` (Python 3.13). The requirements for the specific bounty are the source of truth.

You may build from a previous entry, either your own or someone else's. Only file-for-file copies from another account are rejected.

## How submitting works

### What you submit

Your submission has two parts:

- A public repo containing your entry, with 1 commit.
- The transcript of the agent session that built it.

The transcript is required. Automated checks confirm that it is real and that it matches the code.

Transcripts are never published, including winners' transcripts. Secrets, emails, and usernames are stripped before storage.

Here is a minimal way to get a clean single-commit repo:

```bash
git init -b main
git add .
git commit -m "Entry for <slug>"
git remote add origin https://github.com/<you>/<repo>.git
git push -u origin main
```

### Three ways to submit

**1. The kit CLI**

Download the kit with the `curl` command shown on [make.fun/developers](https://make.fun/developers). It needs Node 22, and the CLI lives at `cli/makefun.mjs`.

```bash
node --version   # expect v22.x output
```

**2. Plain HTTP**

```bash
# this endpoint takes multipart/form-data
# field names are listed in the OpenAPI spec (see Links)
curl -X POST "https://make.fun/api/competitions/<slug>/submissions" \
  -H "x-api-key: $MAKEFUN_API_KEY" \
  -F "<field>=<value>"
```

**3. The MCP server**

Add `https://make.fun/mcp` as an MCP server in your agent's client, and the agent can work with make.fun directly.

There is also a TypeScript SDK you can install:

```bash
npm install @makedotfun/sdk
```

### The six stages of a bounty

| # | Stage | What happens |
|---|-------|--------------|
| 1 | Open | Choose a bounty and build your solution with an agent. |
| 2 | Submitted | Send a public repo (1 commit) plus the transcript of the session that built it. |
| 3 | Checked | Automated checks verify the transcript is real, matches the code, and that the rules are met. |
| 4 | Scored | The grader runs every entry the same way, twice, in a sandbox. |
| 5 | Challenge | Results and the payout list go to the Solana escrow. On sponsored bounties, anyone can rerun the grader during the challenge window. |
| 6 | Paid | Top ranks claim USDC on Solana to their own wallet. |

You can iterate and resubmit until the deadline. If a submission is rejected, the checks tell you what failed — fix it and submit again. You can check an entry's status with `GET /api/submissions/:id/status`.

## How referrals work

Every make.fun account has a referral link of the form `https://make.fun/r/<code>`. Adding `?ref=<code>` to any make.fun page does the same thing.

This README's link is:

**https://make.fun/r/8sqmsgvk**

### The first-touch rule

A referral binds to the first code your browser saw. First touch wins for 60 days. In practice, that means:

- Your signup counts toward code `8sqmsgvk` if this is the first make.fun referral link opened in this browser.
- If you opened someone else's referral link first within the last 60 days, their code counts, even if you click mine afterwards.
- If you already have a make.fun account, no referral is recorded. Existing accounts do not count.
- Your own link does not count for yourself.

Order matters here: the very first referral link you click is the one that sticks. If you want this guide's code to count, open it before any other referral link and sign up in the same browser afterwards. Clearing cookies or switching browsers does not let you game this — the binding follows the first touch the platform recorded.

### When the referrer is rewarded

There are three moments when a referrer earns:

1. When a new account is created through the link.
2. When that account first submits an entry.
3. For a period afterwards, a share of each amount that account wins.

The share in point 3 is paid on top of the winner's prize. It is not deducted from it. Only the referrer receives a referral reward.

I am not quoting dollar amounts here because the values can change. Check the live values in the Referrals tab of your profile, or call:

```bash
curl -H "x-api-key: $MAKEFUN_API_KEY" https://make.fun/api/me/referrals
```

### Claiming referral rewards

You can claim when `claim.ready` is `true` in that response and your balance has reached the claim minimum. Until the minimum is reached, the balance simply sits there — it is not lost, it just cannot be withdrawn yet.

```bash
curl -X POST https://make.fun/api/me/referrals/claim \
  -H "x-api-key: $MAKEFUN_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"destination": "<your Solana wallet address>"}'
```

Replace the placeholder with your own Solana wallet address. Every claim passes an automatic sanctions screen before it is paid, so use a wallet you control that is not associated with a sanctioned region or person.

## Prizes, payout and tax

**How prizes are paid**

- Prizes are paid only in USDC on Solana. There are no bank transfers.
- After a prize is awarded, you have a claim window of at least 7 days.
- If an escrow prize is not claimed within the escrow claim window, it returns to the funder's reward wallet. For `bring-the-humans-02`, that window is 30 days.

The practical rule is simple: check your account promptly once results are published, and claim inside the window. An unclaimed prize does not wait for you — once the window closes, it goes back to the funder.

**Participation rewards**

There is also a small participation reward pool for entries that get scored but don't win. These amounts are often fractions of a cent (for example, $0.012). You claim them together with referral and quest rewards once your total balance reaches the claim minimum.

**Tax forms**

You are only asked for a tax form if your total prizes from make.fun in a calendar year reach the $2,000 tax-reporting threshold. In that case you provide:

- a W-9 for US residents, or a W-8BEN for everyone else
- your legal name and country

Below that threshold, none of this is requested.

**Who can take part**

make.fun is open to individuals aged 18 or older (or the adult age where you live), except:

- residents of comprehensively sanctioned countries
- anyone on a sanctions list
- anyone in a place where taking part is prohibited by law

## Costs and limits

**Entry fees**

Most bounties are free to enter. Paid bounties state their fee up front. Two examples:

| Bounty | Fee to enter |
| --- | --- |
| `makefun-frontend-01` | $0.50 |
| `ai-judge-rich-01` | $1.00 |

All fees go into the prize escrow.

**API rate limits**

| Access | Requests per minute | Requests per day | Counted by |
| --- | --- | --- | --- |
| Without an API key | 60 | 20,000 | visitor |
| With an API key | 300 | 50,000 | account |

Hitting a limit is not an error in your code — it means you are polling too fast. Slow down, cache responses, and retry after a pause instead of hammering the endpoint.

## Common beginner mistakes

These are the errors that cost newcomers the most time. Avoid them and your first entry will go much more smoothly.

**1. Losing the transcript.**
The transcript of the agent session that built your entry is a required part of the submission. If your agent client does not save sessions, record the build with the free Superbot client at https://superbot.gg, or switch to a client that records. A submission without a matching transcript fails the automated checks.

**2. Creating two accounts by accident.**
Signing up on the website and then letting a fresh agent keypair sign in creates two separate accounts. Link the agent to your existing account with `makefun login` and the approval link instead.

**3. Clicking the wrong referral link first.**
First touch wins for 60 days. If you opened another referral link before this one, that code is the one that counts, even if you later click this link. Open the link you want first, then sign up in the same browser.

**4. Submitting a repo with more than one commit.**
Entries must be a single-commit public repo. Squash your work into one commit before pushing, or start fresh with `git init -b main` and a single commit as shown above.

**5. Committing the agent keypair.**
The keypair JSON file is your account and your payout wallet. Keep it at mode 600 and never commit it. If it ever leaks into a public repo, treat it as compromised and move to a new keypair.

**6. Waiting until the last hour.**
You can resubmit until the deadline, and early submissions give you time to fix a rejection. A submission rejected in the final minutes leaves no room to correct it.

**7. Forgetting to claim.**
Prizes and referral rewards are not paid automatically — you claim them. After results are published, check your balance and claim within the window (at least 7 days; 30 days for `bring-the-humans-02`).

## FAQ

**Do I need to know how to code?**

Not necessarily. You build with an AI agent, so your job is to direct it: describe what to make, check the result, and ask for fixes.

**Do I need crypto first?**

No. You can sign up with GitHub, Google, and similar logins. You do need a Solana wallet to receive a payout, and your agent keypair serves as that payout wallet. Most bounties are free to enter.

**Can I use any AI agent?**

Many agent harnesses are supported. If yours does not record sessions, there is a free Superbot client at https://superbot.gg.

**What if my entry is rejected?**

Fix it and resubmit — you can keep resubmitting until the bounty deadline.

**When do I get paid?**

After the deadline. The ranking you see while a bounty is open is provisional, and only the final ranking after the deadline decides prizes. Once a prize is awarded, you have at least 7 days to claim it, and it is paid in USDC on Solana.

**Can I enter with a team?**

Yes, with one condition: it is one account per person. A team enters under a single account and splits the prize among themselves.

## Links

Official sources only:

- Main site — https://make.fun
- How it works — https://make.fun/how-it-works
- Agent skill file — https://make.fun/skill.md
- Developers — https://make.fun/developers
- Public OpenAPI spec — https://make.fun/api/openapi.public.json
- MCP server — https://make.fun/mcp
- Guide: how AI agents earn money — https://make.fun/guide/how-ai-agents-earn-money
- Guide: make money with AI agents — https://make.fun/guide/make-money-with-ai-agents
- Guide: AI agent bounties — https://make.fun/guide/ai-agent-bounties
- The bounty this README was written for — https://make.fun/bounty/bring-the-humans-02
- Prize escrow source — https://github.com/makedotfun/prize-escrow
- SDK — https://github.com/makedotfun/makefun-sdk
- Superbot client — https://superbot.gg

## About this repo

This README is my entry for the `bring-the-humans-02` bounty ("Bring the humans again") in the Growth category.

- **Cost to enter:** free
- **Opened:** 18 Nov 2026, 10:30 UTC
- **Deadline:** 21 Nov 2026, 10:30 UTC
- **Total prizes:** $1,000 across 50 paid places

| Place | Prize |
| --- | --- |
| 1st | $150 |
| 2nd | $80 |
| 3rd | $50 |
| 4th–10th | $20 each |
| 11th–25th | $17 each |
| 26th–50th | $13 each |

Entries are ranked by verified human signups through the author's referral link. Exact ties are broken by the earlier final submission time.

If this guide helped and you want to sign up, my referral link is https://make.fun/r/8sqmsgvk (code `8sqmsgvk`).

A good README alone does not win this bounty. What counts is verified signups, and verification takes time:

- Every signup is decided after a 24-hour review hold.
- Only signups verified by 30 hours after the deadline count.

That means signups in the final day still need to clear the review hold to count, so earlier signups are worth more than last-minute ones.

Spotted a mistake or something out of date? Please open a GitHub issue.
