```
larry@d2r
─────────────────────────────────────────────────────────────────
  os        Windows 11 Pro · Debian 12 on the origins
  host      RTX 5080 · 128 GB · three boxes on three continents
  shell     pwsh, bash, and a disassembler
  uptime    Diablo II since 2000 · Resurrected since launch
  lang      Delphi · C# · Python · TypeScript · x64 asm when it lies
  editor    whatever has the hex view open
  target    D2R 3.3.93847
  policy    read-only · no telemetry · no DMs for bugs
─────────────────────────────────────────────────────────────────
```

```
$ cat ~/.plan

- resolve the new build's offsets before anyone asks
- keep the level generator byte-for-byte with the game
- the site answers from the nearest continent, or not at all
- write it down: every change, one commit, one changelog line
```

## Background

Diablo II since the summer of 2000, Resurrected since its first day: twenty-six years in one game. I have watched the game's
internals change across every patch of the classic client and every build of the new one, and most of the
tools I use I wrote because the ones that existed were wrong about something.

Before this it was operations, for years and on fleets that mattered: build and release pipelines, fleet
configuration, perimeter and host hardening, log pipelines, incident response at three in the morning and the
post-mortems that followed. That is where the habits on this page come from. A deploy that cannot skip its
gate, a server that answers only its edge, a tree hash checked before a switch: none of those are new ideas,
they are scar tissue.

The first language I shipped real tools in was Delphi. A large share of the classic Diablo II toolchain was
Object Pascal, and I still reach for it when a Windows tool needs to be a single small binary with no runtime.
C# and .NET carry that work today; the Win32 underneath has not changed.

## How the work is done

- **The game is the source.** Numbers come from the shipped data tables and the binary, not from wikis.
  Where the two disagree, the game wins and the discrepancy is written down with the evidence.
- **Read, don't write.** Tools that look at a running game open it read-only, never attach a debugger,
  never inject, never send input. If a tool cannot do its job that way it does not get built.
- **Nothing phones home.** No telemetry, no accounts, no servers a tool depends on to run.
- **One commit, one changelog entry.** Every change in every repository carries a timestamped entry
  saying what moved, why, and what the next person needs to know. Several machines work the same tree;
  git history alone is not enough.
- **The shipped tree is the tested tree.** A release is a git bundle of the commits the server lacks, a
  gate that runs the full test suite first and cannot be skipped, a build on the server, and a tree-hash
  check that stops the switch on any mismatch. One ship at a time, enforced by a lock.

## What I don't do

- Ship a binary I cannot explain line by line.
- Trust a number I did not pull from the table myself.
- Deploy from a tree the gate has not seen.
- Answer "it works on my machine". There are three machines; it works on all of them or it is not done.

## Stack

```
reverse engineering   x64 disassembly · process memory · structure recovery · CASC archives
                      level generation · game data tables · Battle.net and game-server protocols
systems               Delphi / Object Pascal · C# / .NET · Win32 · Python · Node.js
web                   TypeScript · Next.js · React · PostgreSQL · Caddy
devops                release pipelines · gated deploys · fleet configuration · git-bundle shipping · Debian
secops                perimeter and host hardening · Cloudflare rulesets and bot management · fail2ban
                      log pipelines and abuse reporting · incident response and post-mortems
game                  Diablo II since 2000 · Diablo II: Resurrected since launch
```

## Keys

```
ssh   ed25519   SHA256:XCz3y7/Kqy23Nr6yaSQVxFuAkEbyBEOa77cTTCVkIFI
```

Verify against [github.com/d2r-mythos.keys](https://github.com/d2r-mythos.keys). Anything claiming to be me
and not signed by that key is not me.

## Contact

Bugs go in the open: the [forum](https://d2r.org/forum) or the repo's issues, with the game build and what you
expected. Everything else, the [Discord](https://discord.com/invite/d2rmythos). Direct messages about bugs get
pointed back here.

[d2r.org](https://d2r.org) · [MythosLoader](https://github.com/d2r-mythos/MythosLoader) · [MythosMaphack](https://github.com/d2r-mythos/MythosMaphack)

<sub>Diablo II: Resurrected is a trademark of Blizzard Entertainment. None of this is affiliated with or endorsed by Blizzard.</sub>
