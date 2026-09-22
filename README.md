# Jev Field Guide

English · [繁體中文](README.zh-TW.md)

A checked list of what is worth installing around Jev (TypeSafe System One).

**Knowledge only, no code.** The implementation that lives on this machine is
[royalskynet/jev-gate-mcp](https://github.com/royalskynet/jev-gate-mcp), and
that repo carries only what belongs to that tool.

## The list (checked 2026-09-22)

Stars and last push were pulled that day with `gh api graphql`, not copied from
a post. All twelve exist and none is archived (`isArchived: false`).

| # | repo | ★ | last push | what it is (author's own words) |
|---|---|---|---|---|
| 1 | [browser-use/jev-ultrafast](https://github.com/browser-use/jev-ultrafast) | 16,901 | 09-18 | Fastest and cheapest web agent |
| 2 | [vercel-labs/json-render](https://github.com/vercel-labs/json-render) | 18,001 | 09-21 | The Generative UI framework |
| 3 | [tamaratran/fast-jev-compaction](https://github.com/tamaratran/fast-jev-compaction) | 6,112 | 09-18 | Claude Code plugin that replaces the compaction summary with Jev decisions: every tool call and result scored in one fast request, stale ones dropped or truncated, everything kept stays verbatim |
| 4 | [lahfir/agent-desktop](https://github.com/lahfir/agent-desktop) | 1,451 | 09-21 | Reliable computer use on the desktop, in Rust: reads an app's real UI structure through OS accessibility trees, so refs stay stable and actions stay safe to retry instead of guessing from pixels |
| 5 | [devagrawal09/jev-review](https://github.com/devagrawal09/jev-review) | 514 | 09-17 | A staged code-review workflow and local dashboard |
| 6 | [itsmostafa/typesafe-mcp](https://github.com/itsmostafa/typesafe-mcp) | 238 | 09-21 | MCP connector giving an agent direct access to the Jev model |
| 7 | [jkudish/jev-mcp](https://github.com/jkudish/jev-mcp) | 257 | 09-21 | Fast, cheap, typed judgments from Jev, as MCP tools |
| 8 | [0xNatoshi/jev-codex-router](https://github.com/0xNatoshi/jev-codex-router) | 189 | 09-22 | Per-turn model and reasoning routing for Codex: picks model, thinking depth and speed mode each turn |
| 9 | [GhalebDweikat/winnow](https://github.com/GhalebDweikat/winnow) | 60 | 09-19 | A calibrated context sieve for Claude Code: every tool result is judged before it enters context |
| 10 | [jarrodwatts/jev-trader](https://github.com/jarrodwatts/jev-trader) | 1,921 | 09-17 | One AI trade decision every Monad block |
| 11 | [fhshaik/typesafe-mario](https://github.com/fhshaik/typesafe-mario) | 343 | 09-16 | Plays Super Mario Bros. from structured emulator state |
| 12 | [monteduro/killmyidea](https://github.com/monteduro/killmyidea) | 81 | 09-18 | Describe an idea; Jev decides kill, fix or ship |

## Claimed vs measured

The post this list came from carries numbers: a flight search in 7 seconds,
81 ms decision latency, about 60% off the bill, 237 replayed test turns. **Those
are the authors' or the poster's claims and none of them is reproduced here.**
What is checked is the table above: the repos exist, are alive, and had those
stars and push dates that day.

Only two things have actually been measured on this machine, and the numbers
live in jev-gate-mcp's DEVLOG:

- **#3 fast-jev-compaction** — installed and in use; the compaction measurement
  is DEVLOG §21.
- **#9's territory** — `hooks/jev.js` here does the same job. Nineteen real
  prune calls in the ledger, **one** of which dropped anything (a 44 KB Bash
  dump, 28,015 chars saved); the other eighteen, including three Reads of
  12-13 KB, dropped nothing. So "judge every tool result" sounds like a bargain
  and isn't: **where the threshold sits decides the yield, not how well the
  judge judges.** Below one chunk the question degenerates into drop-it-all or
  keep-it-all, and keep is the right answer. The threshold table in
  jev-gate-mcp's README has the replay.

The question worth asking before installing any of these: **at what size does
this pay for itself.** Both measurements point the same way — the saving does
not come from judging well, it comes from judging only what is worth judging.

## Minimum path in

The original post's route: read 1 for the mechanics, install 6 for the protocol,
then 3 for context and 5 for review.

The route actually taken here, recorded as a contrast: 6 first (`typesafe-mcp`,
for the primitives), then 3 (compaction — the only one that was felt
immediately), then a prune hook written locally (9's slot, because the threshold
had to be controllable). 1, 10 and 11 are demos: read them for the mechanism,
they do not enter daily use.

## Scope

This repo holds the list, the checks and the reasoning about trade-offs. Anything
specific to one tool — its implementation, configuration or debugging record —
belongs in that tool's own repo and is not copied here.
