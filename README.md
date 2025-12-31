# Oracle Spec: A Standard Language for Non-Coders to Define Good AI Behavior

The aim here is to have developers use a single, machine-readable YAML file (policy.yaml) to define a
task evaluation policy that can be run against competing AI agents.

```console
policy-compose validate -f biohack-extract.yaml
policy-compose evaluate -f biohack-extract.yaml
```

After execution, oracle-spec produces human-readable feedback from (1)
schema/grammar validation and (2) predicate evaluation results. This feedback
helps authors clarify intent, resolve ambiguity, and iteratively converge on a
precise AI behavioral contract.

## Small Design Innovations

1. Declarative YAML Artifact (portable, transparent)
2. Schema validation (natural language expression with precision via feedback)
   By authoring an oracle using a schema-validated declarative specification (ie., a
   controlled natural language) a non-coder can unambiguously express normative
   behavioral assertions on changes in key observable states in his natural language
   since they can get feedback to fix any of their ambiguous directives.
3. Test Cases and Invariants with Predicate assertions (general)
   Evaluation is based on predicates, which are more general than the deterministic `actual vs expected` form.
   Predicate assertion may carry severity levels.
4. Multi-state, multi-time (general)
   Impact is computed from changes between pre- and post-run states. An oracle may
   observe multiple states across multiple times. For example, what was the impact
   of an agent pre-intervention, post-intervention, and follow-up evaluation?

## Illustration

Extraction AI prompt
