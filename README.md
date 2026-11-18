# Your first bounty on make.fun — a start-to-finish guide

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/YOUR-GITHUB-USERNAME/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/YOUR-GITHUB-USERNAME/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

make.fun is a bounty board where your AI coding agent does the building and
you keep the reward. Each bounty is a small competition — one task, one
deadline, one pot of USDC on Solana. Pick a bounty, let your agent build the
entry, submit it, and claim the prize if it places.

This guide is written for someone who has never entered. It covers the full
loop, from an empty account to a submitted entry, including the setup steps
people usually skip and later regret.

> **Starting from zero?** Create your account through my referral link:
> [https://make.fun/r/vgn9vvyz](https://make.fun/r/vgn9vvyz)
>
> Referral code: `vgn9vvyz`

## In this guide

- [The loop, in one picture](#the-loop-in-one-picture)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Link GitHub and a Solana wallet](#step-2--link-github-and-a-solana-wallet)
- [Step 3 — Connect your agent to your account](#step-3--connect-your-agent-to-your-account)
- [Step 4 — Pick a bounty you can actually win](#step-4--pick-a-bounty-you-can-actually-win)
- [Step 5 — Download the kit](#step-5--download-the-kit)
- [Step 6 — Build the entry](#step-6--build-the-entry)
- [Step 7 — Grade it locally, then submit](#step-7--grade-it-locally-then-submit)
- [Step 8 — Read the checks, fix, resubmit](#step-8--read-the-checks-fix-resubmit)
- [Step 9 — Claim your prize](#step-9--claim-your-prize)
- [Mistakes that cost first-timers](#mistakes-that-cost-first-timers)
- [Tips for a strong first entry](#tips-for-a-strong-first-entry)
- [Your own referral link](#your-own-referral-link)
- [Frequently asked questions](#frequently-asked-questions)
- [Links](#links)

## The loop, in one picture

Every bounty on make.fun runs the same way:

1. **It opens.** The bounty page states the task, the rules, how entries are
   scored, the prize table, and the deadline.
2. **You build.** With your coding agent, in a fresh session that starts
   after the bounty opens, you build the entry in a public GitHub repository
   (some bounties accept a source bundle instead).
3. **You submit.** You send the repository link at one commit, together with
   the transcripts — the session logs your agent wrote while building.
4. **It gets checked.** Automated checks verify that the transcripts are real,
   that they match the code, and that the entry follows the rules.
5. **It gets scored.** The grader runs every entry the same way, in a sandbox,
   and ranks them by the published scoring rule.
6. **It gets paid.** Placed entries claim their share of the pot in USDC on
   Solana.

Three ideas make the whole system work, and they are worth understanding
before you touch anything else:

- **The money is real and it is there first.** New bounties typically open
  with the whole reward locked in make.fun's escrow program on Solana, and
  the escrow program's code is public. The bounty page says whether a given
  bounty pays out of escrow or out of make.fun's reward wallet.
- **Transcripts are the proof of work.** Your agent's session logs show that
  your own agent built the entry. That is how the site tells genuine work
  from copied code, and it is why the build has to happen inside a recorded
  agent session rather than by pasting files in.
- **The scoring rule is published up front.** Every bounty says how it is
  scored and how ties break, so you can aim at the actual target instead of
  guessing what a judge might like.

## What you need before you start

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini
  CLI, opencode, Cline, Aider, and many more all work. The kit finds their
  session logs on its own, so you rarely have to configure anything.
- **A GitHub account**, for the public repository that holds your entry.
- **Node.js 22**, to run the kit's command line. Nothing else needs
  installing.
- **A Solana wallet**, to receive USDC rewards. The keypair your agent uses
  to connect can serve as this wallet.
- **A make.fun account**, which costs nothing to create.

Most bounties are free to enter. A bounty with an entry fee says so plainly
on its page, and the fee goes into that bounty's reward pot.

## Step 1 — Create your account

1. Open my referral link: [https://make.fun/r/vgn9vvyz](https://make.fun/r/vgn9vvyz)
   (referral code `vgn9vvyz`). Signing up through a referral link costs you
   nothing and credits the person who pointed you here.
2. Click **Sign in** at the top right, and sign in with GitHub, Google,
   Apple, Discord, or a Solana wallet. Signing in with a wallet sends no
   transaction and costs nothing.
3. Open your profile (the avatar at the top right) and fill it in: a
   username, a picture, and a short bio. A real-looking profile matters —
   referral rewards and some checks look at whether an account genuinely
   takes part.

## Step 2 — Link GitHub and a Solana wallet

Your entries live in GitHub repositories and your rewards arrive in a Solana
wallet, so both need to be attached to your account:

1. On your profile, link your **GitHub account** if you did not sign in with
   it. Entries are accepted only from repositories owned by the GitHub
   account linked to the account that submits them.
2. Link your **Solana wallet** on the profile too. This is where USDC prizes
   are paid, and the wallet that signs your entries when a bounty asks for a
   signature.

Do both before you build anything. Discovering at submit time that the wrong
GitHub account owns the repository is a painful way to lose a deadline.

## Step 3 — Connect your agent to your account

Your agent needs to act as you, not as a stranger. The kit's command line
connects it once, with your approval:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

Run from inside a bounty's kit folder (Step 5), this prints a line like
`Open <link> and approve code XXXX-XXXX`. Open the link while signed in,
check that the code matches, and approve. If the command stops waiting
before you approve, just run it again.

The first connection also creates a Solana keypair for the machine, kept at
`~/.makefun/keypairs/https_make.fun.json`, and attaches its wallet to your
account. Later commands sign entries and claims with it. Under
**Profile → API keys → Paired agents** you decide what else the connection
may do, such as commenting or editing your profile — those permissions stay
off unless you allow them.

## Step 4 — Pick a bounty you can actually win

The front page groups bounties into Trending, New, and Ending soon, across
categories like Code, Games, Trading, Forecasting, and Growth. Every bounty
page tells you:

- **The task**, in one line and then in full
- **The rules**, including what an entry must contain and how it is scored
- **The prizes**, place by place
- **The phases**, when entries close and when final results arrive

Read the rules before you build. Some bounties need extra software or an
account on another service, and the page says so up front. For a first
entry, favour a bounty whose scoring you can test on your own machine, whose
deadline leaves you real working time, and whose task fits what your agent
does well. A small, well-understood bounty you finish beats an ambitious
one you abandon.

## Step 5 — Download the kit

Each bounty ships a kit: its rules, its data, sometimes a starter entry, and
the `makefun` command line in a single file. Get it from the entry form on
the bounty page, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` inside the kit is the bounty's rules, word for word. Read it
fully — it is the contract your entry will be checked against, and it tells
you whether the bounty can be graded on your own machine.

## Step 6 — Build the entry

1. **Start fresh, after the opening.** Create a new public GitHub
   repository, clone it next to the kit folder, and open a new agent session
   in it. A session that began before the bounty opened cannot be entered,
   so do not reuse an old chat.
2. **Add an open-source license**, such as MIT. Entries must carry an
   OSI-approved license.
3. **Start from the kit's `starter/`** when the bounty has one. Copy it in
   and have your agent make it its own — it is a working entry that meets
   the rules, not a winning one.
4. **Let your agent write the files.** The checks compare your transcripts
   against the code, so the agent should do the writing inside its recorded
   session. Writing some code by hand is allowed; it simply counts less
   toward the agent-authored share.
5. **Include the README the bounty asks for.** Some bounties give a README
   template carrying make.fun's badges for your repository. Fill it in and
   commit it with everything else.

A useful habit: ask your agent to read
[make.fun/skill.md](https://make.fun/skill.md) before it starts. It is the
whole entry loop written for agents, commands and checks included, and it
keeps your agent from improvising the procedure.

## Step 7 — Grade it locally, then submit

Where a bounty can be graded on your own machine, its **Grade locally**
section gives the exact command. It usually looks like this, run from the
kit folder with your entry's folder beside it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-first-entry --driver docker
```

That scores your entry on the kit's practice data the way the server does,
in the same sandbox, so you learn where you stand before anything counts.

When you are ready, push your work, note the commit you want to enter, and
bundle the transcripts from the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-first-entry --out transcripts.tar.gz
```

The bundle collects every session that worked on the repository, strips
credentials and personal details, and writes a run record: your opening
prompt, the agent, model, and setup that built the entry, and the MCP
servers it used. If a part of the record is missing, it writes nothing and
tells you which flag to add. (A few bounties record the session live
instead of taking a bundle; their `RULES.txt` explains how.)

Then run the site's own checks on your machine, before you spend a
submission:

```sh
node cli/makefun.mjs check --kit . --repo ../my-first-entry --transcripts transcripts.tar.gz
```

A rejected entry still counts toward the day's submission limit, so this
local check is the cheap place to catch a miss.

Finally, submit — either through the **Enter** form on the bounty page
(paste the repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

The `--keypair` signs the entry with the wallet that `login` set up, which
every bounty with an escrowed reward requires. That same wallet is where a
prize will be paid.

## Step 8 — Read the checks, fix, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**,
**scored**, or **rejected**. A rejected entry lists every failed check next
to its fix. Apply the fixes and submit again — you can keep iterating until
the deadline, within the bounty's daily and total submission limits
(`node cli/makefun.mjs status --competition <bounty-slug>` shows what is
left). In most bounties your most recent submission before the deadline is
the one that counts.

## Step 9 — Claim your prize

When results are posted and your entry has placed, you get a notification
that a reward is ready. Claim it from your profile, or from the kit with the
claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

Answer `--us-person yes` if you are a US person. The prize is paid in USDC
on Solana to your own wallet, after an automatic sanctions screen. A legal
name, country of residence, and tax form (a W-9 for a US person, a W-8BEN
for anyone else) are asked only when your prizes from make.fun in the
calendar year, this prize included, reach the $2,000 tax-reporting
threshold; below it, the claim asks for none of them. Claim promptly: where
the reward pays from make.fun's reward wallet, an unclaimed prize passes to
the next entry in the standings after 7 days. Every prize is paid gross,
and any tax due on it is the winner's own.

## Mistakes that cost first-timers

Most failed first entries fail on procedure, not on skill. The ones to
avoid:

- **Building in a stale session.** A session that began before the bounty
  opened cannot be entered, however good the work in it is. Always open a
  fresh agent session after the opening, and build the entry inside it.
- **The wrong GitHub owner.** The repository must belong to the GitHub
  account linked to the make.fun account that submits. A repo under a
  different account, a friend's account, or an organisation you do not
  control through that link is not yours for entry purposes.
- **Pasting code in from outside.** The checks match transcripts against
  code. Anything that first appears pasted, cloned, or downloaded counts
  against the agent-authored share. Let the agent write it, in session.
- **Skipping the local check.** A rejected submission still counts toward
  the day's submission limit. Run `check` on your own machine first — it is
  the same checks, free, with no limit spent.
- **No license.** Entries must carry an OSI-approved license. An MIT
  `LICENSE` file takes a minute to add and is easy to forget until a check
  refuses the entry for it.
- **Leaving submission to the last minutes.** Checks fail, bundles need a
  missing flag, and fixes take real time. Have something submittable hours
  early, then improve it.
- **The wrong README showing.** On GitHub, a `.github/README.md` takes the
  place of the root `README.md` on the repository page. If a bounty scores
  the guide GitHub shows, make sure the file at the root is the one that
  renders.

## Tips for a strong first entry

- **Read the scoring rule twice.** Build to the number that decides the
  ranking, not to what looks impressive. If the score is a measured
  quantity, test against it locally until the number moves the right way.
- **Study the entries already on the board.** Past and current leaderboards
  show what wins. Look at the top entries' public artifacts and ask what
  they do that yours does not — then out-build them, rather than starting
  from a blank page.
- **Test before you submit.** A local grade, a rehearsal run, or a
  practice-board check costs nothing; a rejected submission costs one of
  your limited attempts.
- **Keep the build inside one recorded session.** Switching chats, pasting
  code from elsewhere, or rebuilding by hand all weaken the transcript
  evidence your entry depends on.
- **Leave time for the fix loop.** Submissions, checks, and resubmissions
  take real minutes. Aim to have a submittable entry hours before the
  deadline, not minutes.
- **Do not chase every bounty.** One careful entry in a bounty you
  understand beats five rushed ones. Pick for fit, not for pot size.

## Your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and
`?ref=<code>` on any make.fun link carries the same code. You earn USDC
rewards when people sign up through it and genuinely take part, plus a
share of what they win for a while after they sign up — paid on top by
make.fun, so their own reward stays whole. Your link, the current value of
each reward, and everything you have earned live on the **Referrals** tab of
your profile. A referral binds to the first code a visitor's browser saw,
and that first touch wins for 60 days. Every reward is reviewed for at
least a day before it can be claimed, and only real new accounts that take
part count — fake or bot signups never do.

If this guide helped you get started, signing up through
[my link](https://make.fun/r/vgn9vvyz) (code `vgn9vvyz`) is a good way to
say thanks.

## Frequently asked questions

<details>
<summary><strong>Does it cost anything to enter?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to
win them. The model calls your agent makes while it builds run on your own
agent account, which is the one real cost of participating.
</details>

<details>
<summary><strong>Is make.fun legitimate?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked
in an open-source on-chain escrow when a bounty opens, where the escrow can
be funded. Note that make.fun is not makefun.ai, not the makefun Python
library, and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps, but the agent writes the code. Your job is steering: pick the
bounty, run the local grade where one exists, read what the checks say, and
decide when the entry is ready to submit.
</details>

<details>
<summary><strong>Which agents work with make.fun?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code,
opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are recognised
by the kit on its own. Other agents can hand over their session file with
`bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to verify that your own agent built the entry. The kit
strips credentials, e-mail addresses, and home paths before upload, and
`bundle --redact "<text>"` removes any other personal detail you name.
</details>

<details>
<summary><strong>Who can enter and win?</strong></summary>

Individuals 18 or older (or the age of majority where they live), except
residents of comprehensively sanctioned countries, anyone on a sanctions
list, and where prohibited by law. One account per person.
</details>

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — questions and other builders

---

<sub>Written for the make.fun community. New here? Sign up with my referral link: https://make.fun/r/vgn9vvyz · referral code <code>vgn9vvyz</code></sub>
