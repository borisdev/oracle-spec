# Oracle Spec: A Standard Language for Non-Coders to Define Good AI Behavior

eval-compose is an open-source tool that lets you define an AI task evaluation policy in a declarative way.
The aim here is to have developers use a machine-readable YAML file to define a
task evaluation policy that can be run against competing AI agents.

```console
policy-compose validate -f biohack-extract-policy.yaml
policy-compose evaluate -f biohack-extract-policy.yaml
policy-compose nl_update -f biohack-extract-policy.yaml --text "never use bad words"
```

Execution produces two types of feedback:

1. schema and ambiguity validation and (2) predicate evaluation results. This feedback
   helps authors clarify intent, resolve ambiguity, and iteratively compose an AI behavioral contract using natural language.

## Highlights

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

https://raw.githubusercontent.com/replicate/cog/refs/heads/main/README.md
How it works

Define the Docker environment your model runs in with cog.yaml:

build:
gpu: true
system_packages: - "libgl1-mesa-glx" - "libglib2.0-0"
python_version: "3.12"
python_packages: - "torch==2.3"
predict: "predict.py:Predictor"

Define how predictions are run on your model with predict.py:

from cog import BasePredictor, Input, Path
import torch

class Predictor(BasePredictor):
def setup(self):
"""Load the model into memory to make running multiple predictions efficient"""
self.model = torch.load("./weights.pth")

    # The arguments and types the model takes as input
    def predict(self,
          image: Path = Input(description="Grayscale input image")
    ) -> Path:
        """Run a single prediction on the model"""
        processed_image = preprocess(image)
        output = self.model(processed_image)
        return postprocess(output)

## Illustration

Extraction AI prompt

Why are we building this?
It’s really hard for researchers to ship machine learning models to production.

Part of the solution is Docker, but it is so complex to get it to work: Dockerfiles, pre-/post-processing, Flask servers, CUDA versions. More often than not the researcher has to sit down with an engineer to get the damn thing deployed.

Andreas and Ben created Cog. Andreas used to work at Spotify, where he built tools for building and deploying ML models with Docker. Ben worked at Docker, where he created Docker Compose.

We realized that, in addition to Spotify, other companies were also using Docker to build and deploy machine learning models. Uber and others have built similar systems. So, we’re making an open source version so other people can do this too.

Hit us up if you’re interested in using it or want to collaborate with us. We’re on Discord or email us at team@replicate.com.
