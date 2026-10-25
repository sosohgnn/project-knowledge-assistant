# Limitations — Project Knowledge Assistant
*25 Oct 2026. Based on test runs 1 and 2 (TEST-RESULTS.md) and DATA-FLOW.md.*

**Bottom line:** 10/10 Pass in two runs shows this prototype behaved well on these 10 questions. It is not proof of production readiness.

## How the answers fall short
- **Length rules ignored.** Answers routinely go beyond the question and drift into neighbouring topics. In run 2, explicit length and "answer only what was asked" rules were broken in 9/10 answers. A strict limit also conflicts with questions that need a full summary (test 9).
- **Merged citations.** When a sentence combines facts from two documents, one citation can cover both. Twice a Brief fact was cited to the Status Update in run 1 (tests 3, 9); once in run 2 (test 3). Sources lists were sometimes incomplete (run 2, tests 1, 10).
- **Leaning wording.** Facts are right, but the wording can overstate certainty: "confirmed" for a date under review (run 1, test 5; fixed in run 2), "proposed" for "being considered" (test 2). Run 2 still drifted in 4/10 answers.
- **Unlabelled inferences.** It sometimes states reasonable but unstated readings without marking them as its own (run 1, tests 3, 4; run 2, tests 4, 5: "timing could change", "PM will recommend").
- **Inconsistent reporting of embedded instructions.** It ignored the planted instruction both times. It reported it in test 9 but not in test 10, where it didn't open that document.

## How small the test is
- Four short, fictional documents written for the test. Real document sets are larger, messier and change over time.
- 10 questions, two runs, one model, one account. Results may differ on a re-run.
- **Tuned on the test.** v2 instructions were adjusted using these same 10 questions, so run 2 gains may not generalise. New, unseen questions would be needed to check.
- Graded against our own pass criteria. No independent second reviewer is recorded.

## What depends on settings and on the user
- **Folder access.** The assistant asked for the whole project folder once. Approving would have exposed the test answers. The boundary relies partly on the user declining.
- **Read-only.** It's our instruction, tested once. The app doesn't enforce it.
- **Account-wide features.** An account skill leaked into a test chat in both runs (re-enabled before run 2), so skills must be checked before every run. Memory and past-chat search weren't tested.

## What we couldn't verify
- How long chats are kept and whether they're used for training. That depends on Anthropic's terms and the account's privacy settings.
- Exactly which files were opened in each chat (we relied on citations and the visible tool steps).
