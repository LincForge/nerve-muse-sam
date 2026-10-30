# Meta Global AI Developer Hackathon — Submission & MacBook Montaj Packet

**Submission Portal:** `https://cerebralvalley.ai/e/meta-ai-developer-hackathon/hackathon/submit`  
**Hard Deadline:** **Wednesday, Nov 4, 2026 at 9:00 PM EST (6:00 PM PST)**  
**Viral X Bonus Deadline:** **Sunday, Nov 8, 2026 at 11:59 PM EST**

---

## 1. MacBook Video Step (Montaj + YouTube Upload, ~10 min on `displays-macbook-pro`)

Per Participant Guide §4 & §7, startups building on existing codebases **must clearly identify in the demo video what was newly built during the Oct 26 – Nov 4, 2026 Hackathon window** (total video cap `<= 180s`; current `assets/demo.mp4` is `110.9s`).

### A. Montaj Edit Spec (Input: `~/projects/nerve-muse-sam/assets/demo.mp4` or `~/.linc/mab-demo/comp/`)
1. **Title Card (`0:00–0:08`, ~8s):**
   - **Title:** `nerve-muse-sam: Meta Muse Spark 1.3 + SAM 3.1 Physical-Device Agent`
   - **Subtitle:** `Meta Global AI Developer Hackathon (Oct 26 – Nov 4, 2026) · Startup Track · Push the Frontier`
   - **Built During Hackathon (Oct 26 – Nov 4, 2026):**
     - `1) SAM 3.1 Visual Grounding (linc-nerve v0.2.0 on PyPI: nerve_ground + nerve_tap prompt)`
     - `2) Muse Spark 1.3 /v1/responses MCP Agent Runner (mobile-agent-bench PR #27, merged)`
     - `3) 20 Live Hardware Benchmark Runs on Physical Galaxy S24 + Galaxy Watch7 (nerve-muse-sam)`
2. **Main Split-Screen Cut (`0:08–1:59`, `110.9s` from `assets/demo.mp4`):**
   - Keep existing captions naming **CLI (`nerve ground` SAM 3.1)** (`0:00–0:20` of clip) vs **Agent (`Muse Spark 1.3` on S24 `c9` + Watch7 `b11`)**.
3. **End Card (`1:59–2:07`, ~8s):**
   - **Scorecard Summary:**
     - `SAM 3.1 CLI Grounding (S24 c9 Canvas Submit): 1.8s, 0.84 confidence, center (173, 875)`
     - `S24 Phone Grid (muse-spark-1.3-contributor): 9/9 PASS on linc ($0.140) & 9/9 PASS on linc-sam ($0.139)`
     - `Watch7 Wear OS b11: PASS in 57.58s ($0.118 Standard, 92.2% cache) & 50.9s ($0.005 contributor)`
   - **Links:** `github.com/LincForge/nerve-muse-sam` · `pypi.org/project/linc-nerve/0.2.0/`
4. **Export Check:**
   - Save exported MP4 to `~/projects/nerve-muse-sam/assets/demo.mp4`.
   - Verify duration `<= 180s`: `ffprobe -v error -show_entries format=duration -of csv=p=0 assets/demo.mp4` (expected `~127s`).

### B. YouTube Hosting Upload
- Upload `assets/demo.mp4` to the LINC YouTube channel (`--channel linc`, `privacyStatus: unlisted` or `public`, never `scheduled`).
- Verify embeddable: `yt-dlp -J <youtube-url> | jq '{duration, playable_in_embed}'`.
- Add the YouTube URL to `README.md` §3B (`#### Demo video`) and push `nerve-muse-sam`.

---

## 2. Copy-Paste Fields for Cerebral Valley Submission Portal

- **Project Title:** `nerve-muse-sam: Meta Muse Spark 1.3 + SAM 3.1 Physical-Device Mobile & Wear OS Agent`
- **Track:** `Startup Track`
- **Problem Statement:** `Push the Frontier`
- **Bonus Categories:** `Best Agentic Use-Case ($5,000)`, `Most Viral Project on X ($20,000)`
- **Public Repository URL:** `https://github.com/LincForge/nerve-muse-sam`
- **Additional Public PR / Release Links:**
  - `https://github.com/LincForge/nerve/releases/tag/v0.2.0` (`linc-nerve[grounding]==0.2.0` on PyPI)
  - `https://github.com/LincForge/mobile-agent-bench/pull/27` (merged to `main`: `https://github.com/LincForge/mobile-agent-bench/compare/pre-hackathon-2026-10-26...main`)
- **Demo Video URL:** `<INSERT_YOUTUBE_URL_FROM_STEP_1B>`
- **Meta Models Used:** `muse-spark-1.3`, `muse-spark-1.3-contributor`, `sam-3.1` (via `POST https://api.meta.ai/v1/responses` + `meta-sam-parser==0.1.0`)

### Short Description (1-2 sentences, unwrapped)

```text
We gave Meta's Muse Spark 1.3 and SAM 3.1 hands and eyes on a physical Samsung Galaxy S24 and Galaxy Watch7 over the Model Context Protocol (MCP), shipping SAM 3.1 visual UI grounding in linc-nerve v0.2.0 and evaluating 20 confined hardware runs on mobile-agent-bench.
```

### Detailed Description & Hackathon Contribution Manifest (Paste-Ready)

```text
What Was Newly Built During the Hackathon (Oct 26 - Nov 4, 2026):
Per Startup Track rules, we tagged our existing open-source repositories at pre-hackathon-2026-10-26 before writing any code. 100% of the following three surfaces was built during the Oct 26 - Nov 4, 2026 window:

1) Visual UI Grounding with Meta SAM 3.1 (shipped in linc-nerve v0.2.0 on PyPI and github.com/LincForge/nerve):
- Built src/linc_nerve/core/grounding.py and tests/test_grounding.py.
- Sends Stage-1 device screenshots + open-vocabulary concept prompts to POST https://api.meta.ai/v1/responses (model="sam-3.1").
- Decodes 1-bit base85 masks via meta-sam-parser==0.1.0, computes the true pixel center-of-mass, and scales source-image coordinates (496x1080 on S24, 432x432 on Watch7) to physical display coordinates (1080x2340 on S24, 432x432 on Watch7).
- Exposes the nerve_ground MCP tool and CLI command (--annotate renders green masks + red centroids), nerve_tap(prompt=...) semantic fallback, and visual_grounding_hint when uiautomator returns empty or unlabelled nodes.

2) Native Meta Muse Spark 1.3 MCP Agent Runner (merged in github.com/LincForge/mobile-agent-bench/pull/27, diff pre-hackathon-2026-10-26...main):
- Built mobile_agent_bench/meta_agent.py and tests/test_meta_agent.py (68 unit tests).
- Drives 70+ MCP device, build, and JDWP debugger tools (nerve, crucible, spectra) over POST https://api.meta.ai/v1/responses.
- Replays sealed reasoning.encrypted_content items in exact turn order across stateless multi-turn tool calls.
- Pins a per-run prompt_cache_key across turns, achieving an 87.9% to 99.0% input token cache hit rate on live hardware runs.

3) Live Physical Hardware Evaluation & Public Showcase (github.com/LincForge/nerve-muse-sam):
- Evaluated across 20 scored physical-device cells (plus 2 disclosed voided cells) under strict sandbox confinement on a physical Samsung Galaxy S24 (SM-S921U, Android 16) and Samsung Galaxy Watch7 (SM-L300, Wear OS 16).
- SAM 3.1 CLI Grounding on Seeded c9 Canvas Submit: uiautomator reports the Submit control as an android.widget.Button at [72,804][276,948] with no text, contentDescription, or resource-id (its play-triangle is drawn on a Compose Canvas). nerve ground --prompt "play button" segmented it at [72,817][274,934] (center 173, 875, confidence 0.84) in 1.8s.
- Galaxy S24 Phone Grid (9 tasks x 2 columns on muse-spark-1.3-contributor): 9/9 PASS on the frozen linc column ($0.140 total) and 9/9 PASS on the linc-sam addendum column ($0.139 total). On the c9 ship-gate task, Muse Spark localized the seeded Tier dropdown bug in 153-174 turns for 4 cents ($0.044 linc, $0.049 linc-sam) and tapped Submit directly from its uiautomator bounds (0 nerve_ground calls across all agent cells, disclosed in README §3B).
- Galaxy Watch7 Wear OS Benchmark (b11): PASS in 57.58s (14 turns, 92.2% cached, $0.118 on muse-spark-1.3 Standard) and PASS in 50.9s (11 turns, 90.1% cached, $0.005 on muse-spark-1.3-contributor).
```
