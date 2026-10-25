# Data flow — Project Knowledge Assistant
*25 Oct 2026. Describes the run-1 test setup. Prototype only.*

## The setup in one line
Claude desktop app (Pro plan) → Project "Lantern Test Assistant" → one local Mac folder shared through the app's folder access: `Agent-Sources` (four fictional documents). No connectors, no third-party integration.

## Where a document goes
1. **On the Mac.** The four files sit in `Documents/Brindlewick Home Goods/Agent-Sources`.
2. **Read on request.** When a question needs a file, Claude asks the desktop app to read it. The app reads it on the Mac, limited to the shared folder.
3. **Copy sent for processing.** The files themselves stay stored on the Mac. But the text Claude reads becomes part of the conversation and is sent to Anthropic's servers, where the model reads it and writes the answer. So storage is local; processing is not.
4. **Saved in chat history.** The chat, including any file text that was read, is stored in the claude.ai account like any other chat.
5. **Source files unchanged.** Claude didn't edit or create files. This is a rule we set and tested, not a platform lock.

## What Claude can see
- Files in `Agent-Sources`, but only those it chooses to open in that chat.
- The Project's custom instructions and the question.
- Account-wide features that are switched on. In setup an account skill leaked build rules into a test chat, so skills were switched off for the run.

## What Claude can't see
- **Other folders on the Mac**, unless the user approves an access request. In setup it asked for the whole project folder; approving would have exposed `TEST-QUESTIONS.md`. **The boundary depends partly on the user saying no.**
- **Other chats.** Each question ran in a fresh chat. This assumes memory and past-chat search weren't used; we didn't test that.

## What we did not verify
- How long Anthropic keeps chats and whether they may be used for model training. That depends on Anthropic's terms and the account's privacy settings, which we didn't audit.
- Exactly which files were opened in each chat. We relied on the citations and the visible tool steps.
- Whether web search was available. It wasn't part of the setup, and no answer used outside information (test 8).

## Why this matters
Because the text of any document Claude reads is processed on Anthropic's servers, this demo uses fictional data only. Real company documents would need an approved tool, a data-handling review and access controls that don't rely on someone declining a prompt.
