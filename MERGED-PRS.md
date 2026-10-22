# Merged upstream pull requests

Fork of [cloudflare/security-audit-skill](https://github.com/cloudflare/security-audit-skill). Reviewed on 2026-10-22 against upstream commit `c1c8a8c`. All 50 open upstream pull requests were read in full. 18 were merged into `main` with `--no-ff` merge commits named `Merge upstream PR #<n>: <title>`. Nothing was sent back to upstream.

Test run (`node --test "skills/security-audit/*.test.cjs"`, Windows 10, Node 24): upstream `main` had 65 tests with 46 passing, 7 failing and 12 skipped. After the merges there are 89 tests with 85 passing, 0 failing and 4 skipped (the FIFO and POSIX symlink tests that skip on Windows by design).

Decisions reflect our use case, auditing a Next.js and Prisma web app from a Windows machine. A SKIPPED row is a judgment call, not a statement that the PR is wrong, except where marked flagged.

| # | Title | Author | Decision | Reason |
|---|---|---|---|---|
| 7 | Add a real /cloudflare-security-audit slash command | MayVerse4 | SKIPPED | Adds a slash command outside the skill directory, conflicts with main, and deletes the SKILL.md heading and intro. The skills CLI install makes it unnecessary. |
| 8 | feat: add findings.json → SARIF 2.1.0 converter | ppcvote | SKIPPED | SARIF converter written against an older findings contract. It drops needs_validation records, reads input without the safe-open path, and conflicts with README. |
| 9 | fix: reject invalid trace line numbers | badmuriss | SKIPPED | Superseded. Adds package.json and an old-layout test directory, and the line lower bound is already enforced (see #45). |
| 13 | Keep Antigravity from idling the hunter wave | csy20 | SKIPPED | Antigravity and Gemini adapter plus a preamble that tells child agents not to refuse. We run Claude Code, and it changes the framing of every delegated prompt. |
| 14 | docs: add Contributing section to README | cyberspace-cs | SKIPPED | Noise. README contributing section. |
| 16 | Add streaming/partial-turn early dispatch pattern to AI-AND-LLM.md | ankit-prabhavak | SKIPPED | Duplicate of #23, which was chosen for its more complete wording. |
| 17 | Update LICENSE | NirmalyaLenka | SKIPPED | Noise. Trailing whitespace edit to LICENSE with no purpose. |
| 18 | Update README.md | NirmalyaLenka | SKIPPED (flagged) | Damaging. Appends a stray backslash and dot to the npx install command and would break it. |
| 19 | Update SKILL.md | NirmalyaLenka | SKIPPED (flagged) | Damaging. Turns the closing "---" of the SKILL.md frontmatter into "--" and would stop the skill from loading. |
| 22 | feat(hunting): add modern full-stack, Next.js, and ORM attack classes | rehmanNRY | MERGED | Next.js server actions, RSC serialization leakage, route cache poisoning, Prisma mass assignment and connect overreach, RLS bypass. Direct fit for our stack. |
| 23 | Add streaming/partial-turn early dispatch pattern | alter | MERGED | Streaming and partial-turn early dispatch class for agent targets. Chosen over #16. |
| 25 | fix(coverage-ledger): verify local-check artifacts exist on disk | alter | SKIPPED | Duplicate of #26. #26 uses an options object that composes with other CLI flags and also checks archived attempts. |
| 26 | fix: validate on-disk existence and integrity of local-check artifacts | anvithsg2004 | MERGED | The ledger validator now checks that local-check artifacts exist on disk, are regular files, and stay inside the owning agent directory. Adds --output-dir and --schema-only. Conflict with #84 resolved by hand. |
| 31 | Fix CLI test suite hanging failures on platforms without O_NOFOLLOW/O_NONBLOCK | Kaushik2210 | SKIPPED | Superseded by #75. With the Windows fallback the guarded CLI tests now run instead of skipping. |
| 32 | Keep quick-profile coverage when a hunter return is malformed | Pioneer113 | MERGED | Malformed hunter return in quick profile is retried once and then deferred with an explicit reason. Conflicts with #84 and #83 text resolved by hand. |
| 33 | Add CI workflow to run the validator test suites | Kaushik2210 | SKIPPED | Duplicate of the CI workflow in #75, which pins action SHAs and covers Node 22 and 24. |
| 35 | feat(hunting): add edge isolate state leakage and distributed KV race… | jastfan | SKIPPED | Cloudflare Workers and edge isolate classes. Not relevant to a Node.js Next.js and Prisma app, so low value. |
| 36 | Guard the one CLI test that passes for the wrong reason | dharun-cohere | SKIPPED | Superseded by #75, which changes the same guard. |
| 37 | docs: clarify security audit coverage boundaries | XiongziqiangA | SKIPPED | Duplicate of #43. |
| 38 | test: guard the remaining CLI tests behind HAS_SAFE_INPUT_OPEN | SurefireStudios | SKIPPED | Superseded by #75, which makes the guarded tests run on Windows. |
| 40 | Add cryptography and key-management audit companion | berkay-byte | MERGED | Cryptography and key-management companion covering JWT verification, password hashing, randomness, nonce reuse, TLS and key rotation. Chosen over #42. README conflict resolved by hand. |
| 42 | docs/Add cryptography and key management | felpzw | SKIPPED | Duplicate of #40, which also carries worked code examples. |
| 43 | README: state that dependency advisory/CVE coverage is out of scope | Kaushik2210 | MERGED | README states that dependency advisory and CVE coverage is out of scope. Useful expectation setting. |
| 44 | feat: cross-validate findings against the coverage ledger | cyberspace-cs | SKIPPED | Cross-validator is timing dependent (must run between Phase 3 and Phase 5), is not wired into the workflow, and copies the unsafe-open code without a Windows path. |
| 45 | Bound source line numbers from above | pucedoteth | MERGED | Bounds source line numbers from above in the findings validator. Small and correct. |
| 48 | Validate retained coverage artifacts and fix platform-aware tests | ZhiHe-ma | SKIPPED | Bundle of CI, a Chinese implementation plan and artifact checks. Overlaps #75 and #26 with mixed scope. |
| 49 | Add validator environment doctor | ZhiHe-ma | SKIPPED | Environment doctor for missing O_NOFOLLOW. Obsolete once #75 makes the validators work on Windows. |
| 50 | Keep config-dependent reachability as needs_validation, not hardening | jboiie | MERGED | Config-dependent reachability stays needs_validation instead of hardening. Fits the skill design. |
| 58 | Add sequential fallback for unstable parallel agents | ghostzeronz-coder | MERGED | Documents a sequential fallback when parallel sub-agents are unstable. Tiny docs change. |
| 59 | Read validator CLI input safely on Windows | henrychen95 | SKIPPED | Duplicate Windows validator fix. #75 was chosen because it also carries the untrusted-content guard and CI. #59 would conflict with it. |
| 60 | Add sibling-Docker sandbox provisioning guide | coffeegrind123 | SKIPPED | Docker sibling-sandbox guide. Docker is not installed on this machine, and it nudges agents to provision sandboxes and build images with network access, which loosens the default stance. |
| 62 | Organize security audit skill into standard directories | dajiaohuang | SKIPPED | Directory reorganisation. Conflicts with nearly everything and upstream has not moved this way. |
| 63 | Reject extra CLI arguments instead of validating only the first file | dharun-cohere | MERGED | Validators reject extra file arguments instead of silently checking only the first. Conflict in the ledger validator resolved by rejecting a second positional path inside parseArgs. |
| 65 | docs: explain ZIP packaging for Claude app Skills upload | Dante-dan | SKIPPED | ZIP packaging notes for the Claude app Skills uploader. Not relevant to Claude Code installs. |
| 67 | security review skill | Beckleytobi | SKIPPED (flagged) | Dumps an unrelated second skill (security-review, about 4,000 lines) and rewrites the README install command to point at the contributor fork Beckleytobi/security-audit-skill. Supply chain red flag. |
| 68 | refactor: organize skill into standard subdirectories (#56) | viwe-monai | SKIPPED | Directory reorganisation. Same reason as #62. |
| 70 | Allow multiple local checks in an archived attempt to share an artifact | ALANDVO | SKIPPED | Duplicate of #82. |
| 74 | feat: model shared validation blockers in findings | Dante-dan | SKIPPED | Adds a shared_blocker record kind that changes the core findings contract. Large blast radius and little value for a single repo audit. |
| 75 | Treat audited code as untrusted input, run the validators on Windows, add CI | oherbawi | MERGED | Windows safe-open fallback for both validators, untrusted target content guard in all agent prompts, and a pinned CI workflow. Test suite goes from 7 failures to 0 on Windows. Conflict with #58 resolved by hand. |
| 76 | Harden git and symlink handling for untrusted targets | alvessh | MERGED | Neutralizes target git config and hooks and avoids following target symlinks when auditing untrusted repositories. |
| 82 | fix: allow artifact sharing within an archived attempt | Dante-dan | MERGED | Fixes false rejection when checks in one archived attempt share an artifact. Chosen over #70, #87 and #91 for the most thorough tests. |
| 83 | docs: align completion gates and carried record validation | Dante-dan | MERGED | Aligns completion gates and carried record handling in the docs. Conflicts with #84 and #32 text resolved by hand. |
| 84 | Reject in_progress units at terminal coverage validation | mvanhorn | MERGED | Adds --terminal so a complete run cannot keep in_progress or planned units, and defines handling of hunters that never return. Merged together with #26 CLI flags. |
| 85 | Validate run-metadata.json against the documented run-state contract | mvanhorn | SKIPPED | Run metadata validator is 900 lines, adds another mandatory step, and copies the unsafe-open code without a Windows path. Deferred. |
| 87 | fix: allow checks in one attempt to share a promoted artifact | lab1207 | SKIPPED | Duplicate of #82. |
| 89 | Remediation should name and preserve legitimate uses of the refused path | sarfaraz1212 | MERGED | Optional remediation.preserved_uses so fixes name the legitimate users of the refused path. |
| 90 | feat: add CWE, CVSS base vector, and references to findings | zavxai | MERGED | Adds CWE, optional CVSS base vector and references to findings. Conflicts in the reporting doc resolved by hand. |
| 91 | fix: allow checks in one attempt to share a promoted artifact | Adarsh-mk7 | SKIPPED | Duplicate of #82. |
| 92 | Add domain-format validators to Business logic class and recon mapping | Himanshu-Sharma12 | MERGED | Domain-format validators added to the Business logic class and to reconnaissance mapping. Docs only. |
| 93 | Add abort-path cleanup and cross-request stale state classes | kelmia-stack | SKIPPED | PHP and native memory-safety classes. Not relevant to Next.js and Prisma. |

## Merge order

Docs and attack classes first (#22, #40, #50, #76, #58, #43, #92, #23), then the Windows validator fix (#75), then validator fixes (#45, #82, #26, #84, #63), then workflow text (#32, #83), then schema features (#89, #90).

## Conflicts resolved by hand

- #40 with #22: README file table, both rows kept.
- #23 with #22: adjacent new classes in `AI-AND-LLM.md`, both kept.
- #75 with #58: Phase 5 verifier sentence in `VALIDATION-AND-REPORTING.md`, both additions kept.
- #84 with #26: CLI parsing and `validateDocument` options in `validate-coverage-ledger.cjs`, merged into one `parseArgs` that understands `--output-dir`, `--schema-only` and `--terminal`.
- #32 with #84: ledger consolidation and critic paragraphs in `HUNTING.md` and the test helper in the ledger tests.
- #83 with #84 and #32: completion gate wording in `HUNTING.md`, `SKILL.md` and `VALIDATION-AND-REPORTING.md`.
- #90 with #89: verifier checklist, verdict contracts and report items in `VALIDATION-AND-REPORTING.md`.
- #63 with #84 and #26: last line of the ledger validator. Extra positional arguments are now rejected inside `parseArgs`.

## Flagged PRs

- #67 rewrites the README install command to a contributor fork and adds an unrelated skill. Do not install from that repository.
- #18 and #19 would break the install command and the SKILL.md frontmatter.
