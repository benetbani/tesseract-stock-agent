# Completion Markers

Completion markers are a small public protocol for pacing multi-step AI workflows.

The idea:

```text
Press N+1 to continue.
RELAY_STEP_COMPLETE_N
```

For example, prompt 4 can ask the model to finish with:

```text
Press 5 to continue.
RELAY_STEP_COMPLETE_4
```

The final prompt uses:

```text
Final analysis finished.
RELAY_STEP_COMPLETE_N
```

## Why the two lines are separate

The first line is for people. It keeps the chain understandable when someone runs it manually.

The second line is for workflow coordination. It gives a structured signal that a runner can watch for before moving to the next step.

This separation matters because the same prompt chain should not need two completely different versions: one for manual use and one for assisted use.

## What the marker does not solve

A marker is not a complete reliability system.

It does not prove that the model answered well. It does not prove that the response is long enough. It does not solve provider UI changes. It does not replace user judgment.

The marker is one signal in a broader workflow design. It helps prevent the most obvious failure: sending the next prompt before the previous answer has ended.

## Public boundary

This repository explains the protocol, not the production parser. The commercial Tesseract Relay implementation includes additional guardrails that are not published here.
