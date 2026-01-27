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

Research Awareness Module:
* Where the code lives (you’ll add paths later)
* What endpoints/commands exist (even if stubbed)
* What schemas are involved (exact filenames)
* What is and is not downloaded automatically

The framework is designed so that evaluation rules can evolve independently of any specific claim source.
---
## Compliance Note
GUT-Check only auto-downloads open-access PDFs; paywalled items are returned as citations with access options.
---
## Project Policies

1) “Single Source of Truth” rule:
Project policies must have exactly one canonical home here in README.
Other files may link to the canonical policy, but must not restate it verbatim. The only exception is templates, such as the Canonical x_provenance template, intended to be copied into other places.
2) Read every file in /docs for updates before starting to code.
    A) Always read the README file first.
---
## Human and AI Guardrails

1) In every AI instruction block (or prompt), add:
    A) Before generating or modifying any Schema, read the existing schema files and match its declared $schema dialect exactly. Do not upgrade drafts unless explicitly instructed.
---
## AI Assistance and Provenance

This repository may use AI tools to assist with drafting, reviewing, or refactoring code and specifications. All changes are ideally reviewed and committed by a human. Git commit history remains the authoritative source of accountability.

To improve transparency and traceability, files shall include a x_provenance object documenting human authorship and any AI assistance used during creation or modification. This metadata is informational only and does not affect runtime behavior, validation, or execution.

Applying this uniformly across all code avoids ambiguity and prevents “special cases” creep.

The x_provenance block records:
* the human responsible for review and commit
* which AI system assisted (if any)
* the role the AI played (e.g., drafting, review, refactor)
* whether the content was reviewed by a human
* optional notes describing the division of labor
* a creation timestamp for traceability

Canonical x_provenance template (use consistently):
"x_provenance": {
  "human_author": "Anna Stockel",
  "ai_assistance": {
    "system": "Claude.ai" or "Open.ai",
    "model_family": "opus 4.5" or "ChatGPT 5.2",
    "role": "(insert role, i.e., schema drafting" or "code review" etc)"
  },
  "reviewed_by_human": true or false,
  "notes": "(AI did X; human did Y.)",
  "created_utc": "(insert timestamp)"
}

Usage Guidance:
* This block shall appear in any code or specification file where AI assistance was used.
* reviewed_by_human shall be true for committed production code.
* AI systems are never considered authors or accountable actors; the committing human remains responsible.

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
