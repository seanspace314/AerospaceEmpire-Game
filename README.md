# Space Empire: The Gamble (2000–2030)

> A **single-file** browser game about running a space launch company. You start in 2000 and play through **120 quarters** to 2030, taking contracts, researching tech and launching rockets to push your market share and valuation as high as you can.

This directory holds the **earliest version of the project (v1)** and also serves as the main README for the whole project. Change notes for later versions live in their own `../vN/README.md`.

---

## Quick start

Just double-click `v1.html` and it opens in your browser. No installation, no build process, no backend.

- **Needs internet**: Tailwind CSS and the Orbitron font are loaded from CDNs.
- To serve it locally instead (avoids `file://` restrictions in some browsers):

```bash
cd v1
python -m http.server 8000
# Open http://localhost:8000/v1.html
```

---

## Gameplay loop

```
Pick a faction → Browse the contract pool → Accept a contract → Research tech / unlock orbits → Launch → Success or explosion
      ↑                                                                                              ↓
      └──────────────── Cash, prestige, market share, valuation change ←──────────────────────────────┘
```

Every quarter settles automatically: revenue comes in, expenses go out, rivals act, time advances. Reach 2030 (or go bankrupt early) and the game ends, scored on final valuation and market share.

---

## Core mechanics

| System | Description |
|---|---|
| **Factions** | 5 to choose from: NASA, CASC, SpaceX, ESA, Rocket Lab. Starting cash, debt, prestige and reliability all differ, so the opening difficulty varies a lot |
| **Contract pool** | A continuously refreshing stream of launch orders, each with payload mass, target orbit, payout and failure penalty. Accepting one starts a preparation phase before ignition |
| **Cash flow** | **Contract revenue is the only source of money** — this version has no financing at all. Check manufacturing cost before accepting; don't burn cash on a contract that is bound to explode |
| **Tech tree** | Spend money on research to raise payload capacity and reliability; it gates the higher-paying contracts |
| **Orbit unlocks** | LEO → GEO → Moon → Mars, unlocked progressively; the further the orbit, the higher the payout |
| **Reliability** | Sets the success probability of each launch. Launching with low reliability sharply raises the chance of losing the rocket. **There is no test stand in this version** — research is the only way to improve reliability |
| **Rivals** | 7 AI companies compete in the same market (SpaceX, Arianespace, CASC, ISRO, Rocket Lab and others); their shares shift over time |
| **Prestige** | Affects valuation and some event checks; successful launches build it, failures hit it hard |
| **Language** | Built-in English/Chinese toggle |

---

## Tech stack

- **Pure single file**: HTML + vanilla JavaScript + Canvas 2D; all logic, styles and data live in one `.html`
- **Tailwind CSS** (CDN) for layout and colour, **Orbitron** (CDN) for the space-age typeface
- **No framework, no bundler, no persistence beyond `localStorage`**

Because it is fully self-contained, it can be dropped straight onto GitHub Pages or any static host.

---

## Version history

Each version adds a handful of features or visual upgrades on top of the previous one, and **all of them are complete, runnable single files**.

| Version | Theme | Notes |
|---|---|---|
| **v1** | Skeleton build | ← You are here. Basic business loop only; financing and ground tests left out |
| [v2](../v2/README.md) | First polish | Smooth progress animation, ground test, difficulty colouring |
| [v3](../v3/README.md) | Bilingual + speed + pseudo-3D | Full bilingual rewrite, 4× speed, world events |
| [v4](../v4/README.md) | Share rebuild + multi-orbit map | Bidirectional share coupling, hard contracts, interplanetary animation, trend chart |
| [v5](../v5/README.md) | Mobile polish | Opaque trend panel and narrow-screen scaling (**recommended build**) |

> **Just want to play?** Use [v5](../v5/README.md) — it has every feature and all known defects fixed. v1 stays here to show where the project started.

---

## Deliberately missing: what this version does not have

v1 keeps only the bare skeleton. This build has **none** of the following systems, and there is no placeholder, disabled control or any other on-screen hint that they exist. A player playing v1 would not know these features are coming; each one first appears in the version shown:

| Missing feature | First appears in |
|---|---|
| Ground test (verify reliability before launch) | [v2](../v2/README.md) |
| Difficulty colouring on contract cards | [v2](../v2/README.md) |
| Smooth, non-uniform preparation progress bar | [v2](../v2/README.md) |
| **Financing channels (VC equity / commercial bank loan)** | [v3](../v3/README.md) |
| 4× speed, full bilingual, pseudo-3D map, world events | [v3](../v3/README.md) |
| Share model rebuild, multi-orbit map, interplanetary animation, trend chart | [v4](../v4/README.md) |

No spot in the v1 interface is reserved for a future feature: the financing channels and the ground test are simply not present, and nothing on screen suggests they will ever be added. They are discovered for the first time only in the versions listed above.

## Known rough edges in v1

- The "preparing for launch" bar uses a uniform CSS transition; it feels mechanical
- Contract cards share one neutral colour with no difficulty distinction, so risk is invisible
- When cash runs short you simply have to tough it out: no bridge financing, running out of cash means bankruptcy
- The map is flat 2D with a single orbit, so satellites bunch into one ring
- No world events, no ending animation, no data trend chart
- Language coverage is incomplete; some dynamic strings remain in Chinese

---

## License

Personal project, for learning and entertainment only.
