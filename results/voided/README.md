# Voided Muse addendum cells (2026-10-27)

- `c9_run1_turncap40` — muse-spark-1.3-contributor, FAIL at 131 s: the
  Muse runner's hard-coded 40-turn cap cut the run off mid-task (fixed in
  e20e04e; the timeout_s budget is now binding, as for the Claude cells).
  The agent also drove the Pixel 8 Pro, not the S24.
- `c9_run2_wrong_device` — same model, regex PASS at 773.7 s / 187 turns /
  $0.063, VOID: seven devices were attached and the agent picked the Pixel 8
  Pro (stock-flavor APK) from nerve_discover instead of the S24 the harness had
  reset with the seeded APK. It reported Tier as working, so it never localized
  the seeded defect; the regex matched an unrelated "Tier dropdown" mention.
  Same cause as mobile-agent-bench AMENDMENTS.md 2026-07 entry (2): the grid must run with only
  the pre-registered device set attached.
