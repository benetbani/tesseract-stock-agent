# Tesseract Relay System Design

This is a sanitized public case study. It explains the engineering shape of Tesseract Relay without publishing implementation details that would allow a commercial clone.

## Problem

Long prompt chains are useful but operationally annoying.

The user has to paste a prompt, wait for the model, inspect the answer, paste the next prompt, and repeat. For a short chain, this is tolerable. For a serious research process, it becomes slow and error-prone.

The design problem was to create a local helper that could assist with same-chat continuation while keeping the user in control.

## Constraints

The system had to respect several constraints:

- The user should stay inside the LLM provider they already use.
- The workflow should run in a normal Chromium-based browser session.
- The app should not require the user to expose private account credentials to a remote runner.
- The chain should remain manually understandable.
- The workflow should support an input value, such as a ticker, company name, document excerpt, or paragraph.
- The runner should not blindly send prompts without evidence that the previous step completed.
- The user should be able to pause, retry, skip, reconnect, or stop.

These constraints pushed the architecture toward local, user-directed browser automation rather than a hidden unattended process.

## Public architecture

At a high level, Tesseract Relay has four public concepts:

1. A desktop control surface.
2. A selected browser.
3. A selected LLM provider page.
4. A prompt pack with a workflow input.

The desktop surface gives the user controls and diagnostics. The browser holds the real conversation. The prompt pack defines the staged work. The workflow input tells the chain what object to analyze.

## Why the chain needs an input

A prompt chain without an input is only a template.

If a chain asks for stock analysis, it needs a ticker or company. If it asks for document analysis, it needs the document or excerpt. If it asks for product strategy, it needs the product context.

Tesseract Relay treats the input as part of the run, not as a separate afterthought. The chain supplies the method. The input supplies the subject.

## Why completion markers exist

The workflow needs a way to know that step N has finished before step N + 1 begins.

The public protocol separates two concerns:

```text
Press N+1 to continue.
RELAY_STEP_COMPLETE_N
```

The first line is readable by a person. The second line is a structured marker for workflow coordination.

This keeps manual use and assisted use aligned. A person can run the chain by reading the instruction. A workflow helper can watch for the marker.

## What is not published

This repository does not publish:

- Source code.
- Provider selectors.
- IPC wiring.
- Retry thresholds.
- Provider-specific fallbacks.
- App packaging configuration.
- Full production completion detection.

Those details belong to the commercial product.

## Design lesson

The important lesson is that AI workflow tooling is not only prompt writing. It is systems work.

The value comes from combining prompt structure, input handling, browser coordination, user controls, diagnostics, and failure recovery into one practical operating layer.

That is the design space Tesseract Relay occupies for [Tesseract Stock Agent](https://www.researchtesseract.com/tesseractstockagent).
