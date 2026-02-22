# Overview of Foundry for Finance (Research)

## Problem
What is broken, inefficient, inconsistent, or impossible?

## Operator
Who uses this system?

Not “users.”
Be specific: researcher, analyst, operator, yourself as planner.

FDEs think in operators.

## Decision
What decision changes because this exists?

If there is no decision, it’s a demo.
If there is a decision, it’s a system.

## Architecture
High-level flow only. No paragraphs.

Example:
Chrome Extension → API Gateway → Lambda → Foundry Stream →
Pipeline → Ontology → Workshop

## Design Decisions & Tradeoffs

3–5 bullets.
Why streaming instead of batch?
Why page-level splitting?
Why union before ontology?
Why LLM extraction?

Tradeoffs signal maturity.

## Failure Modes / Production Considerations
This is what separates you from students.

What breaks?
What scales poorly?
What edge cases exist?

What would you harden before deployment?
