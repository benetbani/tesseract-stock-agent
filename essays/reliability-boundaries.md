# Reliability Boundaries

Structured AI workflows need a realistic reliability model. They are powerful, but they do not behave like deterministic software pipelines.

Tesseract Relay is designed for local, user-visible workflow assistance. That gives the user control, but it also means the system operates inside browser pages and model interfaces that can change.

## What can go wrong

Common failure modes include:

- The provider page changes its layout.
- The chat input behaves differently after an update.
- A long prompt is treated as an attachment instead of pasted as text.
- The model starts answering but stops early.
- The model answers without the expected completion marker.
- A network delay makes the workflow look idle.
- The page is blocked by login, rate limits, or a consent screen.
- A provider introduces a new mode that changes the send behavior.

These are normal reliability boundaries for browser-based LLM tooling.

## The wrong standard

The wrong standard is "the runner should behave like a backend worker."

A backend worker owns the queue, the API contract, the input format, the retry semantics, and the output destination. A browser-based workflow runner owns none of those completely. It coordinates a visible session controlled by the user and the provider page.

That is why user controls matter: pause, resume, retry, skip, reconnect, and stop are not secondary buttons. They are part of the reliability model.

## The right standard

The right standard is controlled assistance:

- Make the workflow state visible.
- Avoid sending the next prompt too early.
- Prefer text insertion over attachment behavior.
- Give the user recovery controls.
- Treat provider changes as expected operational risk.
- Keep the user in the loop when the page cannot be trusted.

This does not guarantee perfect execution. It creates a better operating environment than manual repetition.

## Completion detection is a judgment problem

A completion marker is useful because it gives the workflow an explicit signal. But no single signal is enough in every case.

The model can omit the marker. The page can be slow. The response can be too short to be meaningful. A provider can render content in a way that changes how text is detected.

The production Tesseract Relay implementation uses guardrails that are intentionally not published here. The public concept is enough to understand the design: do not send step N + 1 until step N has produced a credible completion signal.

## When not to use this pattern

This infrastructure is not ideal when:

- The work must run unattended with guaranteed execution.
- The provider page blocks automation.
- The workflow requires regulated audit guarantees.
- The input or output must be handled by a strict backend contract.
- The user cannot supervise or recover the run.

In those cases, a direct API integration or a controlled backend pipeline is usually a better fit.

## Practical conclusion

The value of Tesseract Relay is not that it makes browser-based LLM workflows perfectly deterministic. It is that it makes long same-chat workflows more practical, observable, and recoverable.

That is the realistic engineering line.
