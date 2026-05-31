# Workflow Patterns

Tesseract Stock Agent is a finance product, but the underlying pattern is broader: use a structured chain to move from input to staged reasoning to final synthesis.

This catalog describes public patterns without publishing private commercial prompt libraries.

## 1. Input-bound research chain

The user supplies one object of analysis:

- A ticker.
- A company.
- A product.
- A document excerpt.
- A market.
- A technical system.

The chain then applies a fixed sequence of steps to that object. This is the core pattern behind Tesseract Stock Agent.

## 2. Diagnostic chain

The workflow starts with a failure, anomaly, or unclear situation. Each step narrows the problem:

- What is happening?
- What changed?
- What evidence matters?
- What hypotheses are plausible?
- What should be tested next?

This works well for software debugging, operational analysis, and business process review.

## 3. Due diligence chain

The workflow starts with a claim or opportunity and tries to break it.

Useful stages include:

- Base case.
- Evidence quality.
- Counterarguments.
- Incentives.
- Failure modes.
- Conditions that would change the conclusion.

This is close to the mindset used in serious investment research, but it is not limited to investing.

## 4. Transformation chain

The workflow converts one form of information into another:

- Notes into a memo.
- A transcript into decisions.
- A document into a risk register.
- A product description into positioning.
- Raw research into an executive brief.

The key is to separate extraction, interpretation, and final writing.

## 5. Comparator chain

The workflow compares several options using the same criteria.

This is useful for:

- Vendor selection.
- Competitive analysis.
- Product prioritization.
- Market mapping.
- Tool evaluation.

The chain creates discipline by forcing every option through the same questions.

## 6. Final synthesis chain

The workflow accumulates evidence first and writes last.

This is the opposite of a one-shot prompt. The model is not asked to produce the final memo until the earlier stages have built the context.

That is the core philosophy behind [Tesseract Research](https://www.researchtesseract.com): make the process carry the reasoning load.
