# Social Launch Drafts (X & LinkedIn) — Meta Hackathon Demo

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
Exposing 72 MCP device/debugger tools per turn would burn tokens fast if uncached. Pinning `prompt_cache_key` across turns hit a **92.2% prompt cache rate** (`434k` cached / `471k` input tokens) — a 14-turn physical Galaxy Watch7 run (`b11`) passed in 57.6s for **$0.118** (`<$0.01` in contributor mode).

**Post 3 (Open Source & Reproducible Benchmark Links):**
Everything is Apache-2.0 with sanitized transcripts for every run:

- Showcase + results: https://github.com/LincForge/nerve-muse-sam
- `linc-nerve` (`SAM 3.1` grounding PR): https://github.com/LincForge/nerve/pull/1
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
Running 72 MCP tools (`nerve`, `crucible`, `spectra`) over `/v1/responses` with `reasoning.encrypted_content` replay and a stable `prompt_cache_key` delivered a **92.2% cache hit ratio** (`434,621` cached tokens out of `471,556` input tokens). On our physical Galaxy Watch7 Wear OS benchmark task (`b11`), `muse-spark-1.3` completed the 14-turn flow in **57.58s** for **$0.118**.

3. **Pre-registered, confined evaluation:**
Every run executes in a confined sandbox (`no shell`, `no web`, path-guarded `Read`) with sanitized transcripts published alongside our existing Claude Sonnet 5 baseline.

Code, PRs, and raw transcripts (Apache-2.0):
- Repo: https://github.com/LincForge/nerve-muse-sam
- `nerve` PR: https://github.com/LincForge/nerve/pull/1
- `mobile-agent-bench` PR: https://github.com/LincForge/mobile-agent-bench/pull/27
