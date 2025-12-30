# oracle-spec

Oracle-Spec: A Declarative Standard for Defining Good AI Behavior

Huggingface Benchmarks is the top way to compare AI Agents. The problem
is that it requires coding expertise to personalize and there
is no standard.

An AI oracle is a proposed solution.

What is an AI oracle?

An AI oracle has a dialog with a human who is looking to choose which of many competing AI agents
will lead them to their best conditional outcomes.

The aim of Oracle-Spec is to give non-coders a cheap, transparent and repeatable way to
author an AI oracle.

## Design Principles

1. Declarative

By authoring an oracle using a schema-validated declarative specification (ie., a
controlled natural language) a non-coder can unambiguously express normative
behavioral assertions on changes in key observable states in his natural language
since they can get feedback to fix any of their ambiguous directives.

2. Executable

By compiling an oracle into an evaluator, we can execute one or more
AI agents against the full oracle or the proposed changes in the oracle
to give fine-tuning feedback.

3. Multi-state, multi-time

Impact is computed from changes between pre- and post-run states. An oracle may
observe multiple states across multiple times. For example, what was the impact
of an agent pre-intervention, post-intervention, and follow-up evaluation?

4. Predicates to express behavioral expectations

Evaluation is based on predicates, which are more general than the deterministic `actual vs expected` form.
Predicate assertion may carry severity levels.

## Spec schema

- state
- invariants

## What is an Oracle?

## What is an Oracle Spec?

## Motivation

### Principles

- do not need to code
- can swap different competing AI agent candidates
- can steer the fine-tuning of AI agents
- can get feedback on their directives
- can formulate wholistic evaluations based on a variety of competing concerns
- can formulate evaluation based on many pre and post conditions (states)
- can read and share an AI oracle
- can familiarize themselves with a standard

## Core Innovation

This addresses the fundamental **"alignment specification" problem** - how do domain experts encode their knowledge and values into AI systems without needing to be ML engineers.

## Key Strengths

**1. Separation of Concerns**

```yaml
# Subject matter experts write the "what"
contract.yaml:
  behavior: classify_biohacking_relevance
  criteria: intervention + measurable_outcome

# ML engineers handle the "how"
model_config.py:
  architecture: transformer
  training: fine_tune_on_oracle_spec
```

```yaml
# oracle-spec.yaml
apiVersion: oracle/v1
kind: BehaviorSpec
metadata:
  domain: biohacking_relevance
  version: 2.1.0

spec:
```

## Governance Benefits

**Auditability**: "Why did the AI make this decision?" → "It followed oracle-spec v2.1, section 3.4"
**Accountability**: Clear ownership chain from domain expert → oracle spec → AI behavior
**Transparency**: Stakeholders can read and critique the behavioral specification
**Iteration**: Update specs based on real-world performance without retraining models
