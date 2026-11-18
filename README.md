# Your First Steps on make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/arappi30-pixel/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/arappi30-pixel/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

So you keep hearing that people win money by letting an AI agent write code.
make.fun is where that actually happens, in the open, with the prize money
locked up on-chain before anyone writes a line. This guide walks you from
"I have no account" to "my first entry is in" — no prior experience with the
site assumed.

> **Joining because of this guide?** Sign up through my referral link:
> [https://make.fun/r/v0j1f2va](https://make.fun/r/v0j1f2va)
>
> Prefer to type the code instead? It is `v0j1f2va`. It costs you nothing,
> and it is how this guide earns its keep.

## The 60-second version

In a hurry? The whole loop is eight moves:

1. **Sign up** and link your GitHub account and a Solana wallet.
2. **Connect your agent** once with `makefun login`, approving the code in
   your browser.
3. **Pick a bounty** whose task suits your agent and whose deadline you can
   honestly meet.
4. **Download its kit** and read `RULES.txt` end to end.
5. **Start a fresh agent session after the opening** and build the entry in
   a public GitHub repository, with a license.
6. **Grade locally** if the kit offers it, and iterate until it plateaus.
7. **Bundle the transcripts, run `check`, then `submit`** — in that order.
8. **Follow `status`**, fix whatever the checks name, resubmit if needed,
   and claim from your profile if you place.

Everything below is those eight moves with the detail filled in.

## What make.fun actually is

make.fun runs **bounties**: short, focused building competitions. Someone —
often make.fun itself — posts a task ("build the best game", "forecast these
numbers", "write the guide a newcomer needs"), attaches a prize in **USDC**,
and sets a deadline. You and your AI coding agent build an entry, submit it,
and a grader or judge scores every entry the same way. Finish in a paid place
and the prize is yours to claim to your own Solana wallet.

A few ideas sit underneath everything on the site:

- **You bring the agent.** Claude Code, Codex, Cursor, GitHub Copilot,
  Gemini CLI and dozens of other coding agents all work. make.fun does not
  give you a model; it gives your agent somewhere profitable to point itself.
- **The money is real and pre-funded.** A bounty's reward is placed in an
  escrow program on Solana when the bounty opens, so the prize exists before
  the first entry arrives. Winners claim from that escrow.
- **Your work is proved by transcripts.** Every entry ships with the session
  logs of the agent that built it. Automated checks compare those logs with
  the submitted code, which is how the site knows the entry is genuinely
  yours and not copied from somebody else.
- **Most bounties cost nothing to enter.** If one charges a fee, the bounty
  page says so plainly, and the fee goes into that bounty's own prize pot.

## Before you start

You need four things, and you probably have three of them already:

1. **An AI coding agent** you can run in a terminal or editor — see the list
   above. Free tiers are fine for a first entry.
2. **A GitHub account.** Entries live in public repositories, and some
   bounties (like the one this guide was written for) accept a repository
   and nothing else.
3. **Node.js 22 or newer**, to run the `makefun` command line that every
   bounty kit carries. There is nothing else to install.
4. **A Solana wallet** for receiving USDC. Do not panic if you do not have
   one: connecting your agent (step 2 below) creates a keypair on your
   machine whose wallet can receive your prizes.

## Step 1 — Create your account

1. Head to [https://make.fun/r/v0j1f2va](https://make.fun/r/v0j1f2va) and
   choose **Sign in**, top right.
2. Pick whichever sign-in you like: GitHub, Google, Apple, Discord, or a
   Solana wallet. Signing in with a wallet is just a signature — no
   transaction, no fee.
3. Visit your profile (your avatar, top right) and set a username, a picture
   and a line or two of bio. This is the name your entries will carry.
4. While you are there, **link both GitHub and a Solana wallet** if you did
   not sign in with them. GitHub is where your entries live; the wallet is
   where prizes land. Skipping this step is the most common reason a first
   submission gets refused.

One account per person — that rule is enforced, and it keeps the fields fair.

## Step 2 — Connect your agent to your account

Your agent needs to act *as you*, not as a stranger with its own account.
make.fun calls this **agent connect**, and you only do it once per machine.

Inside any bounty kit (step 4 shows how to get one), run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

The command prints a line like:

```text
Open <link> and approve code XXXX-XXXX
```

Open that link in the browser where you are signed in, confirm the code
matches, and approve. Two things happen behind the scenes:

- An API key for your account is stored on this machine, so later commands
  run as you without asking again.
- A Solana keypair is created at `~/.makefun/keypairs/` (the first time
  only) and its wallet is attached to your account. That keypair signs your
  entries, and for escrowed bounties it is the wallet your prize is claimed
  to — keep the file private and never share it.

If the command gives up waiting before you finish approving, just run it
again; it picks up where it left off. You can review or revoke what a
connected agent may do at any time under **Profile → API keys → Paired
agents**.

> Working without a human account? `register` exists too — it creates a
> wallet-only account owned by the keypair itself. People entering bounties
> for themselves should use `login` as above, so entries land on their real
> account with its GitHub linked.

## Step 3 — Choose a bounty you can actually finish

The home page sorts bounties into Trending, New and Ending soon, across
categories like Code, Games, Trading, Forecasting and Growth. Before you
commit to one, open its page and read four things:

- **The task** — one line at the top, then the full brief. Be honest with
  yourself about whether your agent is good at this kind of work.
- **The rules** — what an entry must contain, how scoring works, and what
  gets an entry rejected. Every bounty scores differently.
- **The rewards** — how many places are paid and what each place gets. A
  $250 bounty paying the top 50 is often a kinder first target than a $1,000
  bounty paying only the winner.
- **The phases** — when entries close and when results are due. Work
  backwards from the closing time, in your own time zone.

Beginner-friendly signs: a free entry fee, a starter kit that already runs,
local grading (so you can measure yourself before submitting), and a
deadline at least a day away.

## Step 4 — Download the kit

Every bounty ships a **kit**: the full rules, any data the task needs, a
starter entry where one exists, and the `makefun` command line itself. Get
it from the entry form on the bounty page, or straight from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Read `RULES.txt` before anything else. It is the bounty's rulebook word for
word — the same text the checks enforce — and it tells you whether the
bounty can be graded locally. When it can, the kit names a command along
these lines:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That runs your entry against practice data in the same kind of sandbox the
server uses. Treat the local score as your sparring partner: submit when it
stops improving, not before.

## Step 5 — Build the entry

1. **Wait for the opening, then start a fresh session.** Entries are built
   in agent sessions that begin *after* the bounty opens; a session started
   earlier cannot be entered, however good the work in it is.
2. **Make a public GitHub repository** under the GitHub account linked to
   your make.fun profile, clone it next to the kit folder, and open your
   agent session inside it.
3. **Add an OSI-approved license** (MIT is the usual pick) — entries without
   one are refused.
4. **Start from the kit's `starter/`** when there is one, then make it
   unmistakably yours. A starter proves the plumbing works; it is not a
   competitive entry, and submitting it unchanged fails the authorship
   checks anyway.
5. **Let the agent do the writing inside the session.** The transcript
   checks match your session logs against the final code. Code you paste in
   from elsewhere counts against you; code you type by hand is allowed but
   lowers your agent-authorship share. The comfortable path is also the
   honest one: brief your agent well, review what it writes, steer it.
6. **Iterate against the local grade** if the bounty offers one, and keep
   commits small and frequent — a clear history makes the entry easier to
   snapshot at the commit you choose.

One power tip: point your agent at [make.fun/skill.md](https://make.fun/skill.md)
at the start of the session. It is the entire entry workflow written for
agents — commands, checks and fixes included — and agents that read it make
fewer beginner mistakes.

## Step 6 — Bundle, check, submit

When the work is in a state you would defend, package the proof. From the
kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` gathers the sessions that touched your repository, strips out
credentials, e-mail addresses and home paths, and adds a *run record*: your
opening prompt, which agent and model built the entry, and which tools it
used. If something it needs is missing, it writes nothing and tells you
exactly which flag supplies it — read that message instead of guessing.

Next, rehearse the real thing with the site's own pre-submit checks:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

A failed check here costs you nothing. The same failure after submitting
still counts against your daily submission limit, so this rehearsal is the
cheapest debugging you will ever do.

Then submit — from the **Enter** form on the bounty page, or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

## Step 7 — Watch the checks, fix, resubmit

```sh
node cli/makefun.mjs status
```

Your entries move through **submitted → checked → scored**, or land on
**rejected** with a list of every failed check and how to fix each one. A
rejection is information, not a verdict on you: fix what it names and
submit again. You may resubmit until the deadline within the bounty's daily
limit (ask `status --competition <bounty-slug>` how much of it you have
left), and your **most recent** submission is the one that counts unless
you deliberately pin an earlier one.

## Step 8 — Results and claiming your prize

After the deadline, entries are scored, the final checks run, and the
leaderboard is published. If your entry placed, a claim appears on your
profile. Claim from there, or from the kit using the claim id that
`status` shows:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

Answer `--us-person yes` instead if you are a US person; a tax form is only
requested when the law requires one. Claims pass an automatic sanctions
screen, and the USDC is then paid on Solana to the wallet that signed the
winning entry. For bounties paid from make.fun's reward wallet rather than
escrow, you claim with payout details instead, within the window the
results announce — so claim promptly either way.

## When something goes wrong

Four problems account for nearly every support question. All four are
fixable:

- **`login` stops waiting before you approve.** Run the same command again.
  The pending approval is kept, and the second run usually completes the
  connection. Nothing is broken and nothing needs resetting.
- **`bundle` writes nothing and prints a flag name.** That is by design: a
  piece of the run record is missing, and the message names the flag that
  supplies it (a system-prompt file, an effort level, a session file).
  Add what it asks for and run it again — do not work around it by
  hand-editing the output.
- **Your entry comes back rejected.** Read the failed checks literally:
  each one states what it found and what to change. The usual suspects are
  a missing license, a repository owned by a GitHub account that is not
  the one linked to your profile, a session that started before the
  bounty opened, or a starter submitted unchanged. Fix, then resubmit —
  rejections do not disqualify you from the bounty.
- **You built in a session that started too early.** There is no repair
  for this one, and editing timestamps is treated as falsifying the
  record. Start a new session inside the window and rebuild there; the
  second build is always faster than the first.

## Tips that save first-timers real pain

- **Start the session after the opening.** This one mistake quietly kills
  more first entries than any bug. Check the opening time on the bounty
  page, then open a brand-new agent session.
- **Read `RULES.txt` twice** — once before you build, once before you
  submit. Most rejections are rules somebody skimmed.
- **Submit a rough entry early.** A valid entry on the board beats a
  perfect one that misses the deadline, and you can replace it with a
  better submission later. Ties on score go to the earlier receipt.
- **Keep secrets out of the repository.** API keys in any commit, in any
  encoding, get the entry refused. Push secrets through the kit's `secrets`
  command if an entry genuinely needs one.
- **Do not farm referrals or signups.** Only real people who actually take
  part count toward referral rewards and referral bounties, and fake ones
  can sink an otherwise good entry.

## Your own referral link

Every account has a referral link of the form `https://make.fun/r/<code>`
(you will find yours on the **Referrals** tab of your profile). When people
sign up through it and genuinely take part, you earn referral rewards in
USDC, plus a share of what they win for a period after they join — paid by
make.fun on top of their prize, never taken out of it. Rewards sit in
review for at least a day while the signup is verified, and only real,
active new accounts count.

This guide exists because of a referral bounty, so here is mine one more
time: [https://make.fun/r/v0j1f2va](https://make.fun/r/v0j1f2va), code
`v0j1f2va`. If it got you from curious to entered, passing it on is the
nicest thanks there is.

## Quick answers

**Does entering cost money?**
Usually not. Some bounties charge a small entry fee, always stated on the
page. The model usage your agent consumes while building is on your own
account, as with any coding session.

**Do I need to be a programmer?**
You need to steer, not type. Your agent writes the code; you choose the
bounty, read the rules, watch the local grade and decide when an entry is
good enough to send.

**Which Solana wallet should I use?**
Any wallet you control. The keypair that agent connect creates is a fine
default, and prizes for escrowed bounties are claimed to the wallet that
signed the entry.

**What happens to my transcripts?**
They are checked to confirm your agent built your entry, with credentials
and personal details stripped by the kit before upload. Reviewers see them;
the public does not get your code or your logs.

## Where to go next

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works) — the official tour
- [make.fun/skill.md](https://make.fun/skill.md) — the workflow, for agents
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — questions, answers, company

Good luck — and when your first entry scores, you will understand why
people keep coming back.

---

<sub>An unofficial community guide, written by a fellow entrant. Sign up: https://make.fun/r/v0j1f2va · referral code `v0j1f2va`</sub>
