# Hidden-assessment access-separation gate

Gate: `IOS-EXPERT-HIDDEN-ASSESSMENT-001`
Status: `BLOCKED_CAPABILITY`
Date: 2026-10-07

## Requirement
Concrete held-out assessment tasks must be technically unreadable by the training identity (`ios-expert` / PP-RM), including through current files, branches, Git history, API reads, inherited repository access or workflow-edit paths.

## Observed current contour
The connected GitHub identity used in this ChatGPT/Scheduled-Task contour has read/write/admin-class repository capability for `lvlaksim1/ios-expert`. Scheduled training tasks use the same connected GitHub integration.

Therefore the following are NOT sufficient isolation:
- another path in ios-expert;
- another branch in ios-expert;
- deleted files preserved in Git history;
- a second repository readable by the same training connection;
- plaintext/generated hidden tasks committed before the attempt;
- same-repository Actions secret if the training identity can alter the workflow or otherwise cause secret exfiltration.

## Acceptable future contours
Preferred:
1. separate evaluator GitHub App/connection/identity;
2. private assessment repository readable by evaluator but not by the training identity;
3. evaluator publishes only assessment-spec metadata, task instance ID, result and permitted evidence back to ios-expert.

Alternative only if independently proven:
- protected GitHub Actions evaluation environment with hidden task material in secrets/secure storage, immutable evaluator workflow from the training identity, approval/protection that the training identity cannot bypass, and no API/history path exposing the task.

## Pass test
Create a non-sensitive canary task in the assessment contour.
The evaluator must prove it can read/use the canary.
The training identity must attempt all permitted read paths and receive access denial/not-found without learning the canary.
Only then may real held-out tasks be generated there.

## Current decision
Do not create real hidden assessment tasks yet. The gate remains BLOCKED_CAPABILITY until an actually separate evaluator identity/access boundary exists.
