# Setup notes — how run 1 was set up
*25 Oct 2026. Repeat these to reproduce the test.*

**Needs:** Claude desktop app on a Mac, Pro plan. No API, no connectors, no paid add-ons.

## Folder layout
```
Brindlewick Home Goods/
├── PROJECT-STATUS.md      builder only
├── Project-Context/       builder only (instructions, questions, results)
└── Agent-Sources/         the ONLY folder the test assistant gets
    ├── Project-Lantern-Brief.md
    ├── Project-Lantern-Status-Update.md
    ├── Project-Lantern-Steering-Notes.md
    └── Project-Lantern-Risks-Issues-Log.md
```

## Steps
1. Create a separate Project: "Lantern Test Assistant".
2. Paste `ASSISTANT-INSTRUCTIONS.md` into its custom instructions.
3. Share only `Agent-Sources` with it through the desktop app's folder access.
4. Switch account skills off (one leaked into a test chat during setup).
5. For each question in `QUESTIONS-TO-PASTE.md`, open a fresh chat and paste the question alone.
6. Deny any request for extra folder access. Approving it would expose the test answers.
7. Grade each answer against `TEST-QUESTIONS.md` and record it in `TEST-RESULTS.md`.

## Rules kept throughout
- Fictional data only. `README.md` is background for the builder, not a citable source.
- Source documents are never edited during tests.
