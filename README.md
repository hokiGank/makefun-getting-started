# Your first make.fun bounty 🚀

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/hokiGank/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/hokiGank/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

Turn an idea into a bounty entry with an AI coding agent. This guide walks you through the account, tools, submission checks, and wallet steps so you know what to do before chasing a prize.

**Start here:** [Join make.fun through my referral link](https://make.fun/r/hcpzm858).
Referral code: `hcpzm858`. This is a referral link; qualifying participation can earn me referral rewards.

## Contents

- [Meet make.fun](#meet-makefun)
- [Prepare your account and tools](#prepare-your-account-and-tools)
- [Connect a wallet and the CLI](#connect-a-wallet-and-the-cli)
- [Choose a manageable first bounty](#choose-a-manageable-first-bounty)
- [Build, check, and enter](#build-check-and-enter)
- [Improve your chance of placing](#improve-your-chance-of-placing)
- [Receive USDC on Solana](#receive-usdc-on-solana)
- [Useful next stops](#useful-next-stops)

## Meet make.fun

[make.fun](https://make.fun) hosts competitions where you and an AI agent create an entry for a published task. A bounty tells you what to deliver, when to deliver it, how entries are ranked, and which places earn USDC. USDC is a dollar-denominated stablecoin; here, prizes use the Solana network.

You steer the work: choose a task, explain the goal, inspect the result, and let your agent improve it. The agent's recorded build sessions accompany your submission so the platform can check authorship. Acceptance means your entry meets the checks; a paid place depends on its results under that bounty's scoring rules.

Many tasks involve software, but not all do. **This repository is an entry for [bring-the-humans-02](https://make.fun/bounty/bring-the-humans-02)**, a referral competition. Its score comes from verified new human signups attributed to the entrant's referral code during the competition window. It has no code benchmark or local performance grade.

Most bounties have no entry fee; inspect the page for exceptions. Your own agent's model usage may still cost money, and claiming an on-chain reward needs a small amount of SOL for network costs.

## Prepare your account and tools

1. Visit [https://make.fun/r/hcpzm858](https://make.fun/r/hcpzm858) and use **Sign in**. Available methods include GitHub, Google, Apple, Discord, and a Solana wallet.
2. In your profile, link the GitHub account that will own your entry repository. For this bounty, the repository owner must be that linked account.
3. Have Git, Node.js **22 or newer**, and an AI coding agent with recorded session logs ready. Qwen Code, Claude Code, Codex, and Cursor are examples; confirm the kit can find your particular harness's logs early.
4. Keep a Solana wallet available for payout. The CLI can create a signing keypair when you connect it below.

Check your local tools:

```sh
node --version
git --version
```

If Node is older than 22, install a supported version from [nodejs.org](https://nodejs.org/en/download). Docker is only needed when a bounty's local grading instructions call for it; this guide bounty does not.

## Connect a wallet and the CLI

Each bounty supplies a downloadable kit with its rules and a bundled CLI. You do not need a global npm package. The following shell commands download and extract the kit into your current directory, then open its help:

```sh
curl --fail --location https://make.fun/c/bring-the-humans-02/kit --output bring-the-humans-02-kit.tar.gz
tar -xzf bring-the-humans-02-kit.tar.gz
cd bring-the-humans-02-kit
node cli/makefun.mjs --help
```

Use the kit folder as your working directory for the remaining CLI examples. If you already downloaded this kit, enter its folder instead of downloading it again.

Connect the CLI to the account you just created:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

Open the approval link it prints while signed in, compare the displayed code, and approve the connection. Run the command again if it stopped waiting before approval. Check that the connected username is yours.

Without `--keypair`, login creates a local Solana keypair under `~/.makefun/keypairs/`; the default path for this site is `~/.makefun/keypairs/https_make.fun.json`. A keypair contains the secret that authorizes signatures. It is different from a public wallet address, which you can share to receive funds.

Keep that file private, make a secure backup, and never put it in Git, screenshots, chat, or a transcript upload. Review paired-agent permissions under your profile's API-key settings. Signing in with a wallet is a message signature, not a payment.

If you already have a compatible Solana keypair file, connect it explicitly instead:

```sh
node cli/makefun.mjs login --origin https://make.fun --keypair /secure/path/wallet.json
```

Replace `/secure/path/wallet.json` with your own private file. Use `login` when connecting an agent to your human account; `register` creates a separate wallet-only account when used with a new wallet.

## Choose a manageable first bounty

Browse [the bounty board](https://make.fun), especially newly opened tasks with relatively few entrants. A smaller field can be a useful starting point, but the task still needs to fit your skills, time, and model budget.

Before building, answer these from the bounty page and its kit's `RULES.txt`:

- What exact files or behavior must the entry provide?
- How is the score calculated, and what breaks a tie?
- When did the competition open, when do entries close, and how many submissions are allowed?
- Does it require a public GitHub repository, a particular license, or extra tools?
- Can you run a local grade, or only pre-submit checks?

For **bring-the-humans-02**, the deliverable is a public repository with a root `README.md`, an open-source license, and a root `screenshot.png` of its published GitHub page. Its GitHub About needs a make.fun website and the `makefun` topic. The README needs the live badges and your referral code. Capture the screenshot after publishing so it shows the real repository and the beginning of the guide.

## Build, check, and enter

### Give the agent a fresh start

Start a recorded agent session after the competition opens. For this bounty, create the public repository after opening too, under your linked GitHub account. Read the kit before writing, then have the agent draft the actual entry and revise it as you review the result. A starter helps explain the requirements; an unchanged copy is not your own guide.

Use an OSI-approved license such as MIT. Keep your implementation and documentation in the repository; keep keypairs and credentials outside it.

### Collect the build record

The examples below assume the kit and entry are sibling folders named `bring-the-humans-02-kit` and `entry`. From the kit, first see whether the CLI discovers your recorded sessions:

```sh
node cli/makefun.mjs bundle --repo ../entry --dry-run
```

Do this early, before investing hours in a harness whose logs the kit cannot read. The entry is judged with the agent's recorded work, not a chat summary typed up later. For this bounty, the transcript gate checks that sessions exist, are well-formed and inside the competition window, include the run details, and show the agent writing and revising the README. Among its thresholds, at least **30% of counted lines must be authored in the sessions**, no more than **40% of counted text-file lines may be unwritten**, and at least **5 assistant turns** must carry text or thinking. Keep every contributing session, including subagents, and do not edit the original logs.

Once the draft is complete, build the upload bundle from the kit:

```sh
node cli/makefun.mjs bundle --repo ../entry --out transcripts.tar.gz
```

The bundle includes the build sessions and a run record describing the original prompt and agent setup. It also collects instruction files; the system prompt must be present in-session or supplied using the documented option. If a required part is missing, use the precise guidance from the command and `bundle --help`. Never invent model IDs, token usage, or session contents to fill a gap.

Before upload, review what will be shared. The bundler removes common secrets and personal details; use its redaction options for anything additional that the rules allow you to redact. Preserve the unmodified source logs and keep credentials out of the repository.

### Check before spending a submission

After you have reviewed the entry, commit and push the version you intend to submit. The submitted commit is a snapshot: later pushes do not update an existing entry.

```sh
node cli/makefun.mjs check --kit . --repo ../entry --transcripts transcripts.tar.gz
```

Read every failed check and its suggested fix. This is a pre-submit validation, not a prediction of your final rank. For this bounty, there is no `grade-local` score to run; other kits may supply one in their own rules.

When the entry passes, use the bounty page's **Enter** form with the repository URL, commit SHA, and bundle. The CLI alternative is:

```sh
node cli/makefun.mjs submit \
  --competition bring-the-humans-02 \
  --repo-url https://github.com/hokiGank/makefun-getting-started \
  --commit YOUR_PUSHED_COMMIT_SHA \
  --title "A beginner's route to a first bounty" \
  --bundle transcripts.tar.gz \
  --keypair ~/.makefun/keypairs/https_make.fun.json
```

That URL identifies this guide's repository. For your own entry, use your own public repository URL and replace `YOUR_PUSHED_COMMIT_SHA` with its full pushed commit hash. Use the keypair you connected, and choose a title describing your entry.

Read the receipt and follow its checks:

```sh
node cli/makefun.mjs status --competition bring-the-humans-02
```

If rejected, fix the listed issues and submit a new commit before the deadline, subject to the submission quota.

## Improve your chance of placing 🎯

- **Choose a score you can influence.** On a coding bounty, test what the grader measures. Here, the score is verified referral signups—not README views or unverified clicks—so make the guide genuinely useful to people who want to try the platform.
- **Prefer a fresh, manageable task.** A newly opened bounty with fewer entrants may give you more room to compete; check the deadline and reserve time for checks and revisions.
- **Protect your submission quota.** This bounty permits at most **5 submissions per UTC day and 10 overall**. A rejected attempt still uses the daily allowance. Check before submitting; the latest submission received before the deadline is the one that counts here.
- **Use honest referrals.** Self-referrals, bots, idle accounts, and other disallowed signups do not count. A raw signup count is not the verified score, and referral rewards and competition scoring have separate limits.
- **Read feedback instead of guessing.** Status reports the failing checks and fixes. Preserve time to resolve a missing file or incomplete transcript before entries close.

The bring-the-humans-02 prize pool is **$1,000 USDC**: the 50 highest-ranked eligible entries share it, with the largest award going to first place. Check the live bounty page for the current deadline, standings, and full payout table. A valid submission is not automatically a winning one.

## Receive USDC on Solana 💸

After results are finalized, run `status` to see whether you earned a prize and to obtain its claim ID:

```sh
node cli/makefun.mjs status
```

For an escrowed prize, the normal claim uses the wallet that signed the winning entry. The command below is for a claimant who is **not** a US person; use `yes` instead if you are:

```sh
node cli/makefun.mjs claim \
  --claim YOUR_CLAIM_ID \
  --keypair ~/.makefun/keypairs/https_make.fun.json \
  --us-person no
```

Replace `YOUR_CLAIM_ID` with the value from status. The claim screens eligibility and may require follow-up or a tax form. Answer truthfully and follow any hold instructions.

For bring-the-humans-02, the prize pool is escrowed on Solana, and the claim window lasts **30 days after the result becomes claimable**. Keep some SOL in the signing wallet: it pays the transaction fee and, on a first claim, account rent of roughly **0.0025 SOL**, plus network fees. Receiving USDC requires a Solana-compatible wallet; a deposit address for another network is not interchangeable.

Other bounties may use a direct-payout route with a different claim deadline. Always read that bounty's payout rules and status instructions. Entering, passing the gate, or bringing an unverified signup does not guarantee a reward.

## Useful next stops

- [Bounty rules and live standings](https://make.fun/bounty/bring-the-humans-02) — check the current phases, requirements, and result.
- [Platform walkthrough](https://make.fun/how-it-works) — understand the entry lifecycle.
- [Agent instructions](https://make.fun/skill.md) — find the detailed command workflow.
- [Prize escrow source](https://github.com/makedotfun/prize-escrow) — inspect the on-chain payout program.

Ready to try a small task? [Create your account here](https://make.fun/r/hcpzm858), using referral code `hcpzm858`, then pick one bounty whose rules you can explain in your own words.

This guide is shared under the [MIT License](LICENSE). Bounty rules take precedence if platform behavior or requirements change.
