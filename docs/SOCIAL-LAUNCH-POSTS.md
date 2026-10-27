# Social Launch Drafts (X & LinkedIn) — Meta Hackathon Demo

> **DRAFT. Check every claim against a recorded run before posting** (verified 2026-10-27):
> - [ ] **Post 1 and LinkedIn point 1 are NOT supported by any bench cell.** In all 8 scored `linc-sam` phone cells and 2 recorded `c9` demo re-runs (2026-10-27, S24 only), Muse Spark called `nerve_ground` **0 times** and never used `nerve_tap(prompt=...)`; it tapped the unlabelled Canvas Submit from its `uiautomator` bounds. Rewrite Post 1 so the SAM 3.1 grounding is shown as the `nerve ground` CLI overlay (section 3A of the README) and the agent clip shows what the transcript shows: the ship-gate run that found the seeded Tier defect. Do not say the agent called SAM.
> - [x] `b11` now has a `-contributor` run on the `linc-sam` column: PASS, 50.9 s, 11 turns, **$0.005** (`results/b11_watch7_linc_sam_contributor/meta.json`). Quote that cell for "<$0.01 in contributor mode" and name the column; the $0.118 / 57.58 s / 92.2% numbers belong to the Standard `linc` run.
> - [x] `assets/demo.mp4` exists (111 s). Captions in it already state CLI vs agent. Post text must match them.
> - [ ] Phone grid numbers (README § 3B phone table): `linc` 8/8, `linc-sam` 8/8, c9 `linc` 667.6 s / 174 turns / $0.044, c9 `linc-sam` 630.4 s / 153 turns / $0.049; demo clip run = `results/demo_c9_linc_sam/` (PASS 577.6 s / 143 turns / $0.037). Quote only these.
> - [ ] "`$0.0025/image`" for SAM 3.1: re-check dev.meta.ai pricing on the day of posting.
> - [x] 92.2% cache rate, 57.58 s, 14 turns and $0.118 match `results/b11_watch7_run1/meta.json`.
> - [x] Tool count: 70 MCP tools (nerve 48 + crucible 8 + spectra 14) plus `Read`.

> **Note:** Posting the demo video on X before **Nov 8 EOD** qualifies for the **$20,000 Most Viral Project** bonus prize in the Meta Global AI Developer Hackathon.

---

## 1. X (Twitter) Launch Post (Attach 90–120s Split-Screen Bench Video)

**Post 1 (Main Video Hook):**
We gave Meta's new `Muse Spark 1.3` + `SAM 3.1` hands and eyes on a physical Galaxy S24 and Galaxy Watch7 over MCP.

The #1 reason mobile QA agents fail in production: empty or unlabelled UI trees (custom Compose/Flutter canvases, games, watch faces). `uiautomator dump` sees an anonymous box with zero labels.

Here is `Muse Spark 1.3` hitting an unlabelled Compose `Canvas` button, calling `SAM 3.1` to segment the icon in <1s, computing the 1-bit mask centroid, scaling to physical screen coordinates, and tapping it live on hardware:

[attach demo video]

**Post 2 (Technical Numbers & What We Learned About Meta's Stack):**
What we learned wiring `POST https://api.meta.ai/v1/responses` into `linc-nerve` and `mobile-agent-bench`:

1. **`SAM 3.1` is a native `/v1/responses` endpoint (`$0.0025/image`):**
Pass a screenshot + short noun phrase (`"submit icon"`), get back source-pixel boxes + base85 1-bit masks in ~0.94s. Decoding the 1-bit raster gives true mask center-of-mass for non-rectangular icons and circular Wear OS (`432x432`) targets.

2. **Encrypted Reasoning Replay + `prompt_cache_key`:**
Exposing 70 MCP device/debugger tools per turn would burn tokens fast if uncached. Pinning `prompt_cache_key` across turns hit a **92.2% prompt cache rate** (`434k` cached / `471k` input tokens) — a 14-turn physical Galaxy Watch7 run (`b11`) passed in 57.6s for **$0.118** (`<$0.01` in contributor mode).

**Post 3 (Open Source & Reproducible Benchmark Links):**
Everything is Apache-2.0 with sanitized transcripts for every run:

- Showcase + results: https://github.com/LincForge/nerve-muse-sam
- `linc-nerve` (`SAM 3.1` grounding): https://github.com/LincForge/nerve
- `mobile-agent-bench` (`Muse Spark` runner PR): https://github.com/LincForge/mobile-agent-bench/pull/27

---

## 2. LinkedIn Post (Attach Demo Video or Side-by-Side Overlay Image)

Every mobile automation agent eventually hits the same wall: `uiautomator dump` returns an empty or unlabelled accessibility tree.

Custom Jetpack Compose `Canvas` widgets, Flutter/Skia surfaces, 60fps animations, and circular Wear OS watch complications often expose zero text, zero `contentDescription`, and zero `resource-id`. To a structural UI agent, the screen is a black hole.

For the Meta Global AI Developer Hackathon, we wired **Meta Muse Spark 1.3** and **SAM 3.1** directly into **nerve** (our Apache-2.0 MCP device server) and evaluated them on physical hardware (**Samsung Galaxy S24** + **Galaxy Watch7**) using **mobile-agent-bench**.

Three engineering takeaways from building on Meta's new Model API (`https://api.meta.ai/v1/responses`):

1. **SAM 3.1 as a deterministic visual fallback (`nerve_ground` + `nerve_tap(prompt=...)`):**
When `nerve_elements` or `nerve_state` detects an empty tree or unlabelled clickable node, it hints the agent to ground visually. `SAM 3.1` segments the Stage-1 screenshot in ~0.94s (`$0.0025/image`), `meta-sam-parser` decodes the 1-bit raster mask to compute the true center-of-mass, and `nerve` scales the centroid from screenshot pixels (`496x1080`) into physical device coordinates (`1080x2340` on S24, `432x432` 1:1 on Watch7).

2. **Stateful encrypted reasoning across MCP tool calls:**
Running 70 MCP tools (`nerve`, `crucible`, `spectra`) over `/v1/responses` with `reasoning.encrypted_content` replay and a stable `prompt_cache_key` delivered a **92.2% cache hit ratio** (`434,621` cached tokens out of `471,556` input tokens). On our physical Galaxy Watch7 Wear OS benchmark task (`b11`), `muse-spark-1.3` completed the 14-turn flow in **57.58s** for **$0.118**.

3. **Pre-registered, confined evaluation:**
Every run executes in a confined sandbox (`no shell`, `no web`, path-guarded `Read`) with sanitized transcripts published alongside our existing Claude Sonnet 5 baseline.

Code, PRs, and raw transcripts (Apache-2.0):
- Repo: https://github.com/LincForge/nerve-muse-sam
- `nerve` MCP server: https://github.com/LincForge/nerve
- `mobile-agent-bench` PR: https://github.com/LincForge/mobile-agent-bench/pull/27
