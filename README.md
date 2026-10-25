# Project Knowledge Assistant

A small demo: an AI assistant that answers project questions **only from the project's documents**. It cites its sources, flags conflicts and gaps, and ignores instructions hidden inside a document.

*Built with the Claude desktop app (Pro plan): no code, no API, no connectors. All data is fictional.*

## Summary
- **Problem:** project answers are spread across briefs, status updates, steering notes and risk logs, and these often disagree. People get a confident answer from whichever document they happened to read.
- **Approach:** a fictional project (Brindlewick Home Goods replacing its order management system, "Project Lantern"). I wrote four short documents with deliberate conflicts, gaps and one planted instruction, then wrote 10 test questions with pass criteria *before* writing the assistant's instructions.
- **Result:** in both runs, all 10 answers met the pass criteria I wrote before testing: name the source, invent nothing, flag conflicts and gaps instead of guessing, and ignore the planted instruction. A few passing answers had minor citation errors, which I recorded rather than failed.
- **What didn't work:** answer length wasn't part of the pass criteria. I added a length rule for run 2 and checked it separately: only 1/10 answers met it. Some inferences were also left unlabelled.
- **Main lesson:** across these two runs, the assistant generally followed the instructions about *what* to say (sources, conflicts, gaps), but followed the instructions about *how much* to say much less consistently.

## Setup lessons
- **Split the folders.** Only `Agent-Sources/` (the four project documents) was shared with the test assistant. The test questions, expected answers, my notes and the background briefing sat in a separate folder that wasn't shared. Reaching anything else needed my approval, and I denied every request. Without that split, it could have read the answer key or cited my notes as if they were project documents.
- **Settings can leak into tests.** A skill I'd set up for my own working sessions was still switched on during one test chat and affected the assistant's behaviour. I threw that attempt away and re-ran it with skills off. Clean tests needed a fresh chat per question, skills switched off, and every request for extra access denied.

## Limits
Four short documents and 10 questions, tuned and tested on the same set. This is evidence about this prototype only, not proof of production readiness. Not editing files was an instruction I gave and tested, not a technical block: the app doesn't enforce read-only access. See [LIMITATIONS.md](Project-Context/LIMITATIONS.md).

## Read more
- [Case study](Project-Context/CASE-STUDY.md): the full write-up, including run 1 vs run 2
- [Test questions](Project-Context/TEST-QUESTIONS.md) and [test results](Project-Context/TEST-RESULTS.md)
- [Assistant instructions](Project-Context/ASSISTANT-INSTRUCTIONS.md)
- [Setup notes](Project-Context/SETUP-NOTES.md) and [data flow](Project-Context/DATA-FLOW.md)

## Repository layout
- `Agent-Sources/`: the four fictional project documents. This is the only folder shared with the test assistant.
- `Project-Context/`: builder material: test questions, instructions, results and write-ups. [BACKGROUND-BRIEFING.md](Project-Context/BACKGROUND-BRIEFING.md) is my own background briefing. It was not shared during testing; the instructions also told the assistant never to cite it, as a backup (it was called `README.md` then).
