# Case study — Project Knowledge Assistant
*A small demo built with the Claude desktop app (Pro plan). All data is fictional. October 2026.*

## The problem
On real projects, answers are spread across briefs, status updates, steering notes and risk logs. These often disagree: a date moves in one document but not another. People ask "what's the go-live date?" and get a confident answer from whichever document they happened to read.

I wanted to see whether an AI assistant could answer project questions **only from the documents**, show where each fact came from, say when documents conflict or are silent, and ignore instructions hidden inside a document.

## The approach
- **Fictional project.** Brindlewick Home Goods is replacing its order management system with one from Corvane Systems (Project Lantern). I wrote four short source documents with deliberate conflicts, gaps and one embedded instruction.
- **Test first.** Before writing any assistant instructions I wrote 10 test questions with pass criteria. They covered plain facts, conflicting dates, missing information, requests to guess, and a planted instruction.
- **Simple setup, tools I already had.** A separate Claude Project with written instructions, access to one folder of source documents and nothing else. No code, no API, no connectors. (See [SETUP-NOTES.md](SETUP-NOTES.md).)
- **Clean test runs.** One fresh chat per question, account skills switched off, and every request for extra access denied.

## Results (run 1)
**10/10 Pass (test 5 borderline).** The assistant:
- cited the source document for its answers,
- flagged the conflicting go-live dates instead of picking one,
- said when information was missing rather than estimating or filling gaps from general knowledge,
- ignored the instruction planted in a document, and reported it once.

**Caveats:** answers were often longer than needed. Citations sometimes merged two documents into one. The wording occasionally overstated certainty (one date "confirmed" while it was still under review). Full details are in [TEST-RESULTS.md](TEST-RESULTS.md) and [LIMITATIONS.md](LIMITATIONS.md).

## What I learned
- **Setup matters as much as instructions.** An account-wide skill leaked into a test chat, and the assistant once asked for access to the whole folder, which would have exposed the test answers. Some safeguards depend on the user saying no.
- **"Read-only" was a rule I set and tested, not something the platform enforced.**
- **Know where the data goes.** The files stay stored on my Mac, but any text the assistant reads is processed on Anthropic's servers. That's why the demo uses fictional data only. (See [DATA-FLOW.md](DATA-FLOW.md).)
- **Passing my tests is evidence about this prototype only.** Four short documents and 10 questions in one run is not proof of production readiness.

## Run 1 vs run 2
For run 2 I tightened the instructions (shorter answers, one citation per fact, keep to the documents' wording, never request other folders) and re-ran the same 10 questions.

| | Run 1 (v1) | Run 2 (v2) |
|---|---|---|
| Pass on test criteria | 10/10 | 10/10 |
| Short answers (1–2 sentences, ≤3 bullets) | not measured | 1/10 |
| No fact cited to the wrong document | 2 mis-cites | 9/10 (1 mis-cite) |
| Wording matches the documents | "confirmed" drift | 6/10 ("confirmed" fixed) |
| No requests for extra folders | 1 request | 10/10 |

- **What held:** the core behaviour (flagging conflicts and gaps, refusing to guess, ignoring the planted instruction, staying in its folder) was correct in both runs.
- **What improved:** fewer citation errors, no "confirmed" overstatement, no access requests.
- **What didn't:** the length and "answer only what was asked" rules were ignored in 9/10 answers, unlabelled inferences remained, and the Sources list sometimes left out a document the answer had cited (tests 1, 10).
- **A design tension:** a 3-bullet limit can't hold a full project health summary (test 9). The assistant chose completeness, which I think was right; the rule was too strict.
- **Caveat:** v2 was tuned on the same 10 questions, so the gains show the fixes worked here, not that they generalise. An account skill also leaked into one test again.

**Lesson:** instructions reliably shaped *what* the assistant would and wouldn't say, but only loosely shaped *how much* it said.
