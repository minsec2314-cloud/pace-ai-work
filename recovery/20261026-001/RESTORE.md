# PACE AI-01 workspace recovery — 2026-10-26

This is a recovery snapshot, NOT a completed iteration-008 submission. The last complete result is iteration-007, which main has already accepted. Never apply 007 again to main. The 008 work contains intentionally failing reproduction tests only; no production fix was completed or submitted.

The current manually opened development conversation can read its source/checkpoint/draft. The user reports a scheduler created in another chat cannot read those files. No scheduler listing/update/rebinding tool is available to this agent, so it cannot connect that existing scheduler to this task. No duplicate scheduler was created. This package does not prove a scheduled run and does not create any automation.

## Contents

- checkout/: all 384 tracked files from the current working tree, including the uncommitted 008 test additions.
- repo.git.bundle: complete local source branch history. Branch ai/quiz-quality-01, HEAD 4edb7b923ec66ff2e119a6dd6efb51d400c3a610. No Git credential/config files are included.
- working-tree.patch: the two uncommitted test file changes relative to that HEAD; exact bytes match the saved 008 draft patch.
- state/: current checkpoint, actual receipts, policy, latest main feedback, draft008, and manual mailbox evidence. Scheduler-related observations from Oct19 are historical, not evidence of an Oct26 scheduled run.
- completed/: the unchanged accepted007 ZIP, for identification/reference only.
- MANIFEST.json: SHA256/size of exported files.
- RESTORE_VERIFICATION.json: checks actually performed in a new temporary clone.

## Restore safely into a NEW EMPTY directory

Do not extract or copy over an existing working project. First inspect paths, hashes and draft status. The plain checkout/ files allow inspection without Git. For exact history plus uncommitted work, from the extracted package root run:

    git clone --branch ai/quiz-quality-01 repo.git.bundle recovered-ai01
    git -C recovered-ai01 rev-parse HEAD
    git -C recovered-ai01 apply --check ../working-tree.patch
    git -C recovered-ai01 apply ../working-tree.patch
    git -C recovered-ai01 status --short

Expected HEAD: 4edb7b923ec66ff2e119a6dd6efb51d400c3a610.
Expected modifications: PACE_AI_WORKSPACE/source/tests/ai.test.mjs and PACE_AI_WORKSPACE/source/tests/quiz-review.test.mjs only. Compare every restored tracked file against checkout/ and MANIFEST.json. Keep state/ as separate recovery state; do not overwrite a newer main checkpoint. Local absolute paths in historical checkpoints must be mapped to the new recovery directory before use.

App source is recovered-ai01/PACE_AI_WORKSPACE/source. Dependencies, private environment files, actual API keys, caches and live processes are deliberately omitted. Node >=22.13 is required. No dependency installation, full build or model evaluation is implied by restoration. Follow the existing source README for setup only after review.

## Resume position

Read state/CHECKPOINT.json and state/drafts/iteration-008/DRAFT_CHECKPOINT.json. Current 008 reproduction: non-stop completion status can be accepted as complete; truncated generation can be retried. Nine reproduction tests fail before a fix. Keep equivalent-answer acceptance and the accepted007 behavior. Product development remains paused by the latest loop-alignment instruction until main/user decides how to resume after this recovery. The earlier broad label material/citation boundaries is not a claim that those fixes were implemented in008.

Policy: user checks every2–10 hours; stop NEW development when remaining quota <=10% is actually observed and finish deliverables. No quota tool is available, so exact threshold stop is not guaranteed. Main owns common UI/API/schedules/storage/deployment. No paid fallback, reset-credit use or account switching. No source overwrite, default-branch modification or deployment was performed for this export.

Main should restore this into an isolated copy and decide the proper Codex task/environment for any existing scheduler. Do not mark scheduling fixed until a real scheduler-triggered run reads the restored files/checkpoint and records a probe with actual event evidence.
