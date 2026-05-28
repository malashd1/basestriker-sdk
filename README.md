# BaseStriker SDK

<div align="center">

![Base](https://img.shields.io/badge/Base-0052FF?style=for-the-badge&logo=coinbase&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![License](https://img.shields.io/badge/license-MIT-4cff7a?style=for-the-badge)

**Read-only TypeScript SDK for the [BaseStriker](https://github.com/malashd1/Basestriker) leaderboard and stats API.**

</div>

---

## What this does

A tiny `fetch`-based SDK around `https://api.basestriker.xyz` for anyone who wants to read public game state on Base:

- Weekly + lifetime leaderboard
- Per-wallet stats: highest level, total runs, lifetime POINTS
- Daily missions (read-only — claim flow requires a signed wallet)
- USDC treasury balance + 7-day spend

Useful for: third-party dashboards, Farcaster Frames, Telegram bots, alt-frontends.

## Install

```bash
npm install @malashd1/basestriker-sdk
```

## Quickstart

```ts
import { BaseStrikerClient } from '@malashd1/basestriker-sdk';

const client = new BaseStrikerClient();

// Weekly top 10
const top = await client.getLeaderboard({ limit: 10 });
for (const row of top) {
  console.log(`#${row.rank} ${row.player} — LV ${row.level} · ${row.score} pts`);
}

// Per-player stats (replace with any player wallet address)
const me = await client.getPlayer('0xYourWalletAddressHere');
console.log(`Lifetime POINTS: ${me.points}, highest LV: ${me.highestLevel}`);
```

## API surface

| Method | Returns |
|---|---|
| `getLeaderboard({ limit, week? })` | `LeaderboardRow[]` |
| `getPlayer(address)` | `{ points, highestLevel, totalRuns }` |
| `getMissions(address)` | `Mission[]` (read-only — no claim) |
| `getTreasury()` | `{ usdcBalance, spend7d }` |
| `getHealth()` | `{ ok, signer, chainId }` |

All methods return strongly typed values; no `any`.

## Tech

- Zero dependencies (just `fetch`, available in Node 18+ and modern browsers)
- TypeScript-first, full types exported
- Published to npm + GitHub Packages

## Status

🚧 **Work in progress.** Scaffold + readme; client implementation pending.

## Studio

BaseStriker SDK is a [Chisoft](https://chisoft.co/) project — an independent
game studio based in Prague, Czech Republic. Issues + PRs welcome on this repo.

## License

MIT — see [LICENSE](LICENSE).
