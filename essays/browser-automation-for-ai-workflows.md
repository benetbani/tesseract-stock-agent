# Browser Automation for AI Workflows

Tesseract Relay exists because a serious AI workflow is often not a single prompt. It is a sequence of dependent steps that must happen in one conversation, with enough pacing to let the model finish before the next instruction arrives.

That sounds simple until the workflow has to run inside real browser-based LLM products.

## The browser is not a stable API

Browser automation for AI tools is difficult because the page is a living interface, not a contract.

The automation layer has to deal with:

- Provider UIs that change without notice.
- Different chat input behavior across LLM products.
- Long prompts that must be pasted as text, not uploaded as files.
- Streaming responses that may stop, retry, or continue late.
- Login states, session expiry, consent screens, and rate limits.
- New buttons, banners, tool modes, and provider experiments.
- The risk of sending the next prompt before the previous answer is complete.

This is the difference between a demo and a workflow tool. A demo can work once. A workflow tool has to survive normal user conditions.

## Why same-chat continuation matters

The most useful prompt chains carry state forward.

In equity research, step 2 depends on step 1. In a technical review, the risk assessment depends on the architecture summary. In a document workflow, the final synthesis depends on the extracted facts. If every step starts in a new chat, the chain becomes a stack of isolated prompts instead of a process.

Same-chat continuation lets the conversation accumulate context. It is also where reliability gets harder, because the automation must interact with the same active provider page over a longer period.

## Why Electron

Electron gives a local workflow runner a stable surface:

- A visible control panel.
- Local settings.
- Status and diagnostic output.
- Buttons for pause, resume, retry, skip, reconnect, and stop.
- A bridge between user intent and browser control.

For Tesseract Relay, the desktop shell is not cosmetic. It keeps the workflow visible and recoverable while the LLM conversation remains in the browser selected by the user.

## Why Playwright and CDP

Playwright can connect to Chromium-based browsers through the Chrome DevTools Protocol. At a high level, this lets a local app coordinate with a real browser session rather than forcing the user into a hidden browser or a separate backend job.

That matters because the user already has:

- A preferred browser.
- Logged-in AI accounts.
- Active conversations.
- Provider-specific settings.
- A visible place to inspect what happened.

Tesseract Relay is designed around user-directed control. It does not replace the LLM provider. It coordinates the workflow around the selected provider page.

## The real problem is pacing

The hard part is not only inserting text. The hard part is deciding when to insert the next text.

A reliable chain runner needs to answer questions like:

- Did the model actually respond?
- Is the response still streaming?
- Did the provider attach the text as a file instead of pasting it?
- Did the previous step produce enough content to be useful?
- Did the model emit the expected completion signal?
- Did the page change state after the prompt was sent?
- Can the user recover without restarting the entire chain?

This repository explains the public architecture. It intentionally avoids the production-level implementation details that would turn the notes into a cloneable app.

## Where this approach works best

Local browser automation works best when:

- The user wants to stay in a normal browser-based LLM product.
- The workflow benefits from one continuous conversation.
- The prompt chain can include completion instructions.
- The user wants visible control rather than hidden execution.
- Occasional human supervision is acceptable.

It is not a replacement for a backend queue, a financial data terminal, or direct model APIs. It is an interface layer for structured human-directed AI work.

## Public boundary

The private Tesseract Relay implementation includes production safeguards, provider handling, UI state management, and recovery behavior that are not published here.

For the user-facing system, see [Tesseract Stock Agent](https://www.researchtesseract.com/tesseractstockagent) from [Tesseract Research](https://www.researchtesseract.com).
