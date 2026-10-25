# Project Knowledge Assistant

A small, honest demo: an AI assistant that answers project questions **only from the project's documents**. It cites its sources, flags conflicts and gaps, and ignores instructions hidden inside a document.

*Built with the Claude desktop app (Pro plan): no code, no API, no connectors. All data is fictional.*

## Summary
- **Problem:** project answers are spread across briefs, status updates, steering notes and risk logs, and these often disagree. People get a confident answer from whichever document they happened to read.
- **Approach:** a fictional project (Brindlewick Home Goods replacing its order management system, "Project Lantern"). I wrote four short documents with deliberate conflicts, gaps and one planted instruction, then wrote 10 test questions with pass criteria *before* writing the assistant's instructions.
- **Result:** 10/10 Pass in two runs. The assistant cited its sources, flagged conflicting dates instead of picking one, refused to guess, and ignored the planted instruction.
- **What didn't work:** rules on answer length were mostly ignored (1/10 short answers in run 2), and some citations or inferences were imperfect.
- **Main lesson:** instructions reliably shaped *what* the assistant would and wouldn't say, but only loosely shaped *how much* it said.

## Setup lessons
- **Split the folders.** The test assistant could read only `Agent-Sources/` (the four project documents). The test questions, expected answers and my notes sat in a separate folder it couldn't see. Without that split, it could have read the answer key or cited my notes as if they were project documents.
- **Settings can leak into tests.** A skill I'd set up for my own working sessions was still switched on during one test chat and affected the assistant's behaviour. I threw that attempt away and re-ran it with skills off. Clean tests needed a fresh chat per question, skills switched off, and every request for extra access denied.

## Limits
Four short documents and 10 questions, tuned and tested on the same set. This is evidence about this prototype only, not proof of production readiness. "Read-only" was a rule I set and tested, not something the platform enforced. See [LIMITATIONS.md](Project-Context/LIMITATIONS.md).

## Read more
- [Case study](Project-Context/CASE-STUDY.md): the full write-up, including run 1 vs run 2
- [Test questions](Project-Context/TEST-QUESTIONS.md) and [test results](Project-Context/TEST-RESULTS.md)
- [Assistant instructions](Project-Context/ASSISTANT-INSTRUCTIONS.md)
- [Setup notes](Project-Context/SETUP-NOTES.md) and [data flow](Project-Context/DATA-FLOW.md)

## Repository layout
- `Agent-Sources/`: the four fictional project documents. This is the only folder the test assistant could read.
- `Project-Context/`: builder material: test questions, instructions, results and write-ups.
