# GUT-Check

GUT-Check is a structured evaluation framework for assessing nutrition, supplement, food, and health-adjacent claims using transparent, auditable criteria. It is designed to enforce disciplined reasoning in domains distorted by marketing, influencer amplification, and overconfident summaries.

GUT-Check emphasizes clarity, constraint-awareness, and intentional reasoning over persuasion, popularity, or conclusiveness.

Claims may originate from marketing materials, media, influencers, user questions, or AI-generated summaries. GUT-Check evaluates the claim itself, not the system that produced it.
---
## Purpose
GUT-Check exists to answer a specific problem:
“How do we evaluate food, supplement, and nutrition claims in a way that is explicit, defensible, and repeatable without pretending that evaluation itself can be fully automated?”

This project is not a benchmark, leaderboard, or automated grader. It is an evaluation aid intended for humans who need to make informed judgments under uncertainty.
---
## Core Principles
• Human-in-the-loop evaluation
• Explicit scoring criteria
• Context-aware judgment
• JSON-first, machine-readable inputs and outputs
• Separation of evaluation logic from claim sources
• Transparency over optimization
GUT-Check intentionally avoids opaque scoring, hidden heuristics, and source-specific tuning.
---
## Scope Guardrails (Anti-Drift)
The following guardrails are non-negotiable:
• The primary object of evaluation is the claim, not an AI model or content generator
• No model benchmarking, ranking, or leaderboards
• No prompt optimization or generation features
• No prescriptive medical diagnosis, dosing, or treatment guidance
• No collapse of uncertainty into unexplained single scores

Any feature or change that shifts the system toward evaluating model performance or generating persuasive content is out of scope by definition.
---
## What GUT-Check Is Not
• It is not an AI model
• It does not generate content
• It does not attempt to replace human judgment
• It is not a prompt optimization tool
• It is not a general-purpose benchmark suite

Any use of GUT-Check that treats scores as absolute truth is a misuse of the framework.
---
## High-Level Architecture
GUT-Check operates on structured inputs and produces structured evaluation outputs.

At a high level:
• Inputs are normalized JSON payloads representing claims and relevant context
• Evaluation logic applies rubric-based criteria
• Outputs are scored results with explanatory metadata

Research Awareness module:
* Where the code lives (you’ll add paths later)
* What endpoints/commands exist (even if stubbed)
* What schemas are involved (exact filenames)
* What is and is not downloaded automatically

The framework is designed so that evaluation rules can evolve independently of any specific claim source.
---
## Compliance Note
GUT-Check only auto-downloads open-access PDFs; paywalled items are returned as citations with access options.
---
## Project Status
This repository is under active development.
Initial focus areas include:
• Defining stable evaluation rubrics
• Implementing core scoring logic
• Ensuring reproducibility and traceability
• Supporting incremental extension without breaking existing evaluations

Interfaces and internal structure may change until a 1.0 release.
---
## Authoritative Specification
The authoritative design and governance specification for GUT-Check is maintained separately as a PDF document.
See:
docs/gut-check-spec-v0.2.pdf

In the event of conflict between this README and the Product Specification document, the specification document takes precedence.
---
## License
This project is licensed under the MIT License. See the LICENSE file for details.
---
End of README.md
---
