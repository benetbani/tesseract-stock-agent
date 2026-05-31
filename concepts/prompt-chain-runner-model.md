# Prompt-Chain Runner Model

This is educational pseudocode. It is not Tesseract Relay source code. It is incomplete by design and cannot run as an application.

## Conceptual flow

```text
load prompt blocks
collect workflow input
open or connect to selected browser
open selected LLM page

for each prompt block:
    combine workflow input with current prompt
    add public completion instruction
    paste prompt as text into the active chat
    send prompt

    wait for a credible completion signal
    confirm the response is not empty

    if the user pauses, pause
    if the user retries, retry current step
    if the user skips, move to next step
    if the user stops, stop run

stop after the final marker
```

## What is intentionally omitted

This example excludes:

- Browser selectors.
- Playwright implementation.
- Electron implementation.
- Provider-specific handling.
- Real retry logic.
- IPC details.
- File handling.
- Packaging configuration.
- Production completion detection.

The goal is to show the operating model, not to publish a workflow runner.

## Why the model is useful

The model clarifies the difference between a prompt chain and a runner.

The prompt chain defines the reasoning sequence. The runner coordinates pacing, input insertion, and user controls. The LLM remains the reasoning engine. The human remains the operator.
