# Social Launch Drafts (X & LinkedIn) - Meta Hackathon Demo

> **Pre-post verification checklist** (verified 2026-10-30):
> - [x] **Post 1 and LinkedIn point 1 rewritten to match recorded runs.** In all 8 scored `linc-sam` phone cells (plus `a6`, `b11`, and 2 recorded `c9` demo re-runs), Muse Spark called `nerve_ground` **0 times** and never used `nerve_tap(prompt=...)`. It tapped the unlabelled Canvas Submit from its `uiautomator` bounds `(180, 877)` inside `[72,804][276,948]`. The drafts below state that SAM 3.1 grounding (`1.8s`, confidence `0.84`, center `(173, 875)`) is run via the `nerve ground` CLI and that the agent caught the seeded Tier defect for 4 cents using `uiautomator` bounds.
> - [x] `b11` has both runs quoted accurately: Standard `linc` (`57.58s`, 14 turns, `92.2%` cached, `$0.118`) and contributor `linc-sam` (`50.9s`, 11 turns, `90.1%` cached, `$0.005`).
> - [x] `assets/demo.mp4` (`110.9s`, pending Montaj title/end cards on MacBook) captions state CLI vs agent, and the post text matches them.
> - [x] Phone grid numbers match `README.md` §3B: `linc` 9/9 (`8/8` phone-only + `a6`, `$0.140` total), `linc-sam` 9/9 (`8/8` phone-only + `a6`, `$0.139` total), `c9` `linc` `667.6s` / 174 turns / `$0.044`, `c9` `linc-sam` `630.4s` / 153 turns / `$0.049`, and recorded demo run `results/demo_c9_linc_sam/` (`577.6s` / 143 turns / `$0.037`).
> - [x] "`$0.0025/image`" (`$2.50 / 1,000 images`) matches `src/meta_agent.py` and `dev.meta.ai` pricing as of 2026-10-30 (re-confirm on `dev.meta.ai` on the day of posting).
> - [x] `92.2%` cache rate, `57.58s`, 14 turns, and `$0.118` match `results/b11_watch7_run1/meta.json`.
> - [x] Tool count: 70 MCP tools (`nerve` 48 + `crucible` 8 + `spectra` 14) plus `Read` (71 in `linc`, 72 with `nerve_ground` in `linc-sam`).
> - [x] Voice canon pass (`docs/writing/linc-voice.md`): zero em-dashes, zero semicolons, zero AI-hype words, no `"QA"` / `"test infrastructure"` framing, X = hook post + link in reply (no thread), LinkedIn <= 150 words (116 words), unwrapped paste-ready lines.

> **Note:** Posting the demo video on X before **Sun, Nov 8 EOD** qualifies for the **$20,000 Most Viral Project** bonus prize in the Meta Global AI Developer Hackathon.

---

## 1. X (Twitter) Launch Post (Hook Post + Link Reply, No Thread)

### Headline / Hook Options for Line 1
1. **Plain:** We wired Meta's Muse Spark 1.3 and SAM 3.1 into nerve (our Apache-2.0 MCP server) and ran mobile-agent-bench on a physical Galaxy S24 and Galaxy Watch7.
2. **Number-led:** 20 hardware benchmark runs on a physical Galaxy S24 and Galaxy Watch7 with Meta's Muse Spark 1.3 and SAM 3.1 over MCP (18/18 phone PASS for $0.28 total).
3. **Curiosity-gap:** We gave Muse Spark 1.3 a SAM 3.1 visual grounding tool (`nerve_ground`) for unlabelled Android Canvas buttons, then ran 12 hardware benchmark cells to see if it needed it.

### Post 1 - Main Video Post (Attach `demo.mp4`, no external links in body)

```text
We wired Meta's Muse Spark 1.3 and SAM 3.1 into nerve (our Apache-2.0 MCP server) and ran mobile-agent-bench on a physical Galaxy S24 and Galaxy Watch7.

1) SAM 3.1 (nerve v0.2.0 CLI): segmented an unlabelled Compose Canvas Submit icon on the S24 in 1.8s (0.84 confidence, $0.0025/image). It scaled the 1-bit mask center from screenshot pixels to physical coordinates (173, 875).

2) S24 phone grid (muse-spark-1.3-contributor): 9/9 PASS on both columns ($0.140 linc, $0.139 linc-sam). On the c9 ship-gate, the agent caught the seeded Tier dropdown bug for 4 cents ($0.044 linc, $0.049 linc-sam, $0.037 in the demo clip) and tapped Submit from its uiautomator bounds (0 nerve_ground calls).

3) Galaxy Watch7 (b11): PASS in 57.58s ($0.118 Standard, 92.2% cached across 70 MCP tools) and 50.9s ($0.005 contributor).
```

### Reply 1 - Links (Post as direct reply to Post 1)

```text
Code, benchmark PR, and raw transcripts (Apache-2.0):
1) Showcase and transcripts: https://github.com/LincForge/nerve-muse-sam
2) nerve v0.2.0 (SAM 3.1 grounding on PyPI): https://github.com/LincForge/nerve/releases/tag/v0.2.0
3) mobile-agent-bench (Muse Spark MCP runner PR #27): https://github.com/LincForge/mobile-agent-bench/pull/27
```

---

## 2. LinkedIn Post (116 Words, `<= 150` Word Cap, Paste-Ready Unwrapped)

```text
We wired Meta's Muse Spark 1.3 and SAM 3.1 into nerve (our Apache-2.0 MCP device server). Then we ran mobile-agent-bench on a physical Galaxy S24 and Galaxy Watch7.

Results across 20 hardware runs:

1) SAM 3.1 grounding (nerve v0.2.0): The nerve ground CLI segmented an unlabelled Compose Canvas button in 1.8s at 0.84 confidence ($0.0025/image).

2) S24 phone grid (muse-spark-1.3-contributor): 9/9 PASS on both columns ($0.140 on linc, $0.139 on linc-sam). On c9, the agent caught the seeded Tier bug for 4 cents ($0.044 linc, $0.049 linc-sam) using uiautomator bounds (0 nerve_ground calls).

3) Galaxy Watch7 (b11): PASS in 57.58s ($0.118 Standard, 92.2% cached across 70 MCP tools) and 50.9s ($0.005 contributor).

Code and transcripts: https://github.com/LincForge/nerve-muse-sam
```

---

## 3. Claim Verification Table (Internal Audit - Strip Before Sending)

| Claim in Draft | Source Artifact | How Produced |
|---|---|---|
| SAM 3.1 CLI grounded unlabelled `c9` Submit in `1.8s`, conf `0.84`, center `(173, 875)` | `README.md` §3A & §3B (`assets/c9_submit_grounded_cli.png`) | Physical Galaxy S24 (`SM-S921U`), `nerve ground --prompt "play button" --annotate`, 2026-10-27 |
| `$0.0025/image` (`$2.50 / 1,000 images`) for `sam-3.1` | `src/meta_agent.py` (`SAM_PRICE_PER_IMAGE = 0.0025`) | `dev.meta.ai` pricing table, 2026-10-27 |
| S24 phone grid: `linc` 9/9 PASS (`$0.140`), `linc-sam` 9/9 PASS (`$0.139`) | `README.md` §3B, `results/phone_s24/{linc,linc-sam}/*/meta.json` | Physical Galaxy S24 (`SM-S921U`), `muse-spark-1.3-contributor`, 2026-10-27 |
| `c9` ship-gate: `$0.044` (`linc`, `667.6s`, 174 turns), `$0.049` (`linc-sam`, `630.4s`, 153 turns), `$0.037` (`demo_c9_linc_sam`, `577.6s`, 143 turns), `0` `nerve_ground` calls | `results/phone_s24/{linc,linc-sam}/c9/meta.json`, `results/demo_c9_linc_sam/meta.json` | Physical Galaxy S24 (`SM-S921U`), `muse-spark-1.3-contributor`, 2026-10-27 |
| Watch7 `b11`: `57.58s`, 14 turns, `92.2%` cached (`434,621 / 471,556`), `$0.118` (`muse-spark-1.3` Standard); `50.9s`, 11 turns, `90.1%` cached, `$0.005` (`muse-spark-1.3-contributor`) | `results/b11_watch7_run1/meta.json`, `results/b11_watch7_linc_sam_contributor/meta.json` | Physical Galaxy Watch7 (`SM-L300`), 2026-10-27 |
| 70 MCP tools (`nerve` 48 + `crucible` 8 + `spectra` 14) + `Read` | `README.md` §2 | Frozen `linc` v3 stack (`71` tools) + `nerve_ground` in `linc-sam` (`72` tools) |
