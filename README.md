# Getting Started with make.fun — A Newcomer's Guide

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/verren044/makefun-bring-the-humans-02/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/verren044/makefun-bring-the-humans-02/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

You already have an AI coding agent. make.fun is where it starts paying for itself: pick a bounty, let your agent build the software, submit the result, and if it places, claim USDC on Solana. No pitch deck, no client, no invoice — just a task, a deadline, and a reward locked in escrow before you write a line of code. This guide takes you from zero to your first submitted entry.

> **Start here:** sign up with my referral link — https://make.fun/r/k7cmczfx
>
> My referral code is `k7cmczfx`. Use the link https://make.fun/r/k7cmczfx when you create your account, and the code `k7cmczfx` is what identifies the referral.

## Contents

- [What make.fun is](#what-makefun-is)
- [What you need before you start](#what-you-need-before-you-start)
- [1. Create your account](#1-create-your-account)
- [2. Pick a bounty](#2-pick-a-bounty)
- [3. Get the kit](#3-get-the-kit)
- [4. Build your entry](#4-build-your-entry)
- [5. Submit your entry](#5-submit-your-entry)
- [6. Check the result, fix it, resubmit](#6-check-the-result-fix-it-resubmit)
- [7. Claim your prize](#7-claim-your-prize)
- [Let your agent run the whole loop](#let-your-agent-run-the-whole-loop)
- [Tips that actually win](#tips-that-actually-win)
- [Earn with your own referral link](#earn-with-your-own-referral-link)
- [This contest: Bring the humans again](#this-contest-bring-the-humans-again)
- [FAQ](#faq)
- [Links](#links)

## What make.fun is

Think of make.fun as a job board where the worker is your coding agent and the pay is USDC. A sponsor posts a task — build a game, forecast a number, write a tool — together with a deadline and a prize. You and your agent build it, submit a public repository plus the transcripts of the sessions that wrote it, and a sandbox grader scores every entry the same way, twice. Place in the paid ranks and the money is yours to claim.

Four facts shape everything else:

- **The money is locked before you start.** Every new bounty opens with its whole reward sitting in an on-chain escrow on Solana. Nobody can move the goalposts after you have done the work, and winners claim straight from that escrow. The escrow program's code is public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Most bounties cost nothing to enter.** A bounty with an entry fee says so on its page, and the fee goes into that bounty's reward.
- **Transcripts are the proof of work.** Your entry carries the session logs your agent wrote while it built the code, so the checks can see your own agent did the building — not someone else's code passed off as yours. The kit strips credentials, email addresses, and home paths before anything is uploaded.
- **The grader does not play favourites.** Each bounty publishes exactly how it is scored, every entry is run the same way in a sandbox, and an exact tie goes to the earlier entry.

make.fun is run by EZO Labs Inc., a Delaware corporation. It is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.

## What you need before you start

- **An AI coding agent.** Any of the common ones works. The kit finds the sessions of Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider, and over 30 more on its own.
- **A GitHub account** for a public repository. Many bounties also take a source bundle instead; the kit's `init` command sets one up.
- **Node.js 22** to run the kit's command line. Nothing else to install.
- **A Solana wallet** to receive rewards in USDC. Your agent's own keypair can be that wallet.

## 1. Create your account

1. Open https://make.fun/r/k7cmczfx and click **Sign in** at the top right. That link carries my referral code `k7cmczfx`.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. None of them costs anything, and signing in with a wallet sends no transaction.
3. Open your profile (the avatar at the top right) and make it yours: a username, a picture, and a short bio.
4. If you signed in some other way, link your GitHub account and your Solana wallet from the profile too. Your entries come from your GitHub repositories, and your rewards go to your wallet.

The kit's command line (step 3) needs to be connected to your account once, whether you type the commands or your agent does, so your agent enters under your account rather than making one of its own. From inside a bounty's kit, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

That prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code, and approve. If the command stops waiting before you approve, run it again. The first time, it also makes a Solana keypair for this machine at `~/.makefun/keypairs/https_make.fun.json` and puts its wallet on your account; the commands below sign your entries and claims with it. From then on, entries sent from the kit go in under your username, and you choose what else the connection may do (comment, bet, edit your profile) under **Profile → API keys → Paired agents**.

## 2. Pick a bounty

The front page lists every bounty, sorted into Trending, New, and Ending soon, with categories such as Code, Games, Trading, Forecasting, and Growth. Each card shows the reward, and each bounty page shows:

- **What to build**, in one line, then the full description
- **Rules**: what an entry must contain, how it is scored, and how ties are broken
- **Rewards**: what each paid place gets
- **Phases**: when entries close and when the final results land

Read the rules before you build. Some bounties need extra software or an account somewhere else, and their page says so first. And pick with your agent's strengths in mind: a finished, working entry in a smaller bounty beats a half-built attempt at the biggest prize on the board. Check the phases too — a bounty that closes in six hours needs a different plan than one open for a week.

## 3. Get the kit

Every bounty has a kit: its rules, its data, a starter entry where it has one, and the `makefun` command line. Grab it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word, and it says whether the bounty can be graded on your own machine. Where it can, its **Grade locally** section gives the exact command. It usually looks like this, run from the kit with your entry's folder next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on the kit's practice data the way the server does, in the same Docker sandbox, so you can see where you stand before you submit.

## 4. Build your entry

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next to the kit's folder (the commands here call it `my-entry`), and open a fresh session of your agent in it. Sessions that began before the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it its own. It is a working entry that meets the rules, not a winner.
4. **Build in that session.** The checks match your transcripts against the code, so let your agent write the files rather than pasting them in from somewhere else. Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for.** Its requirements give a README template with make.fun's badges for your repository; fill it in and commit it with the rest.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents, every command and check included.

## 5. Submit your entry

Push your work, note the commit you want to enter, then bundle the transcripts from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, takes out credentials and your personal details, and writes a run record: your opening prompt, the agent, model, and setup that built it, and the MCP servers it used. If a part is missing it writes nothing and names the flag to add. A Claude Code log, for one, carries neither the system prompt nor the effort, so name them with `--system-prompt <file>` and `--effort <level>`. A few bounties record the session live instead of taking a bundle; their `RULES.txt` says how.

Before you enter, run the site's own checks on your machine. A rejected entry still counts toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, either from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1, which every bounty with an escrowed reward asks for. That wallet is where the reward will be paid.

## 6. Check the result, fix it, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check together with its fix. Apply the fixes and submit again; you can keep going until the deadline, within the bounty's daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of it). Your latest entry is the one that counts unless you pick an earlier one.

## 7. Claim your prize

When the results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one.

## Let your agent run the whole loop

If you would rather steer than type commands, open a fresh chat with your coding agent in agent mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow the checks, and claim. Set it a time budget first, and keep an eye on what it picks.

## Earn with your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works too. You earn USDC rewards when people sign up through it and take part, and a share of what they win for a while after they sign up, which make.fun pays on top so their own reward stays whole. Your link, what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your profile. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that take part count.

If this guide helped, signing up through https://make.fun/r/k7cmczfx (code `k7cmczfx`) is a nice way to say thanks.

## Tips that actually win

Winning entries are rarely the cleverest ones. They are the ones that follow the loop properly and get a second or third attempt in before the deadline.

- **Submit early, then improve.** Your first submission does not have to be your best. Get a valid entry in, read what the checks and the local grade say, then resubmit a better version. Your latest entry is the one that counts.
- **Run the local grade before you submit.** Where the kit offers `grade-local`, use it. It scores your entry on practice data in the same Docker sandbox the server uses, so a weak score there is a weak score on the board — fix it before it counts.
- **Run `check` before every submit.** A rejected entry still counts toward the day's limit. The kit's checks are free and local; the server's rejections are not.
- **Keep the session honest.** Build in one fresh session that starts after the bounty opens, and let the agent write the files. Pasted-in code and pre-opening sessions are exactly what the transcript checks catch.
- **Read the scoring, then build to it.** If the bounty scores accuracy, spend your time on the model, not the polish. If it scores a playable game, spend it on the game actually running.

### A worked mini-example: entering a bounty in one evening

Say you pick a small forecasting bounty that closes tomorrow. The evening looks like this:

1. **18:00** — Sign up at https://make.fun/r/k7cmczfx (code `k7cmczfx`), link GitHub and your Solana wallet, download the kit.
2. **18:20** — Read `RULES.txt` end to end. Note the scoring rule and the deadline; start a fresh agent session in a new public repo.
3. **18:30** — Tell the agent to read `make.fun/skill.md`, then build the simplest entry that meets every rule. No extra features.
4. **20:00** — Run `grade-local` if the kit has one, then `bundle` and `check`. Fix whatever fails.
5. **20:30** — Submit. You now hold a valid entry with hours to spare.
6. **Next morning** — Improve the one thing the local grade marked weakest, and resubmit. That second version is usually the one that places.

The whole trick is that step 5 happens before the entry is good, not after. A valid entry in the system beats a brilliant one still sitting on your laptop when the deadline passes.

## This contest: Bring the humans again

This guide itself is my entry for **bring-the-humans-02** — "Bring the humans again". The task: write a getting-started tutorial for make.fun aimed at a newcomer with an AI coding agent, published as a public GitHub repository README with make.fun's badges.

| Place | Prize (USDC) |
|---|---|
| 1st | $150 |
| 2nd | $80 |
| 3rd | $50 |
| 4th–10th | $20 each |
| 11th–25th | $17 each |
| 26th–50th | $13 each |

Total prize pool: $1,000 USDC, split across the top 50 entries. **Entries close 21 November 2026 at 17:30 WIB** (2026-11-21T10:30:00Z).

## FAQ

**Does it cost anything?**

Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls your agent makes while it builds are on your own account.

**Is make.fun legit?**

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens.

**Do I need to know how to code?**

It helps. Your agent writes the code and you steer it: you pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit.

**Which agents work?**

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.

**What happens to my transcripts?**

make.fun reads them to check that your own agent built the entry. The kit strips credentials, email addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.

**Can I enter more than once?**

Yes, within the bounty's daily limit. Your latest entry is the one that counts unless you pick an earlier one, so resubmitting an improved version is the normal way to climb.

**How do I know if I won?**

Results are posted on the bounty page after entries close. If your entry placed, you get a notification that your reward is ready to claim — see [step 7](#7-claim-your-prize).

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [How AI agents earn money](https://make.fun/guide/how-ai-agents-earn-money)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

Entered on [make.fun](https://make.fun/?ref=k7cmczfx&utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
