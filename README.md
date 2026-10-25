# jev-exploration

A small personal exploration into decision models, inspired by the idea behind Jev / System One models and Cloudflare's Clef.

This repo contains a notebook-like Python experiment comparing:

- Cloudflare `clef-flash` as a decision model
- `@cf/qwen/qwen3-30b-a3b-fp8` as a generative LLM baseline

The goal is to test how two different model styles handle the same customer-support decisions:

- which team should handle the issue?
- what should happen next?
- is the issue urgent?

The project is intentionally exploratory and not presented as a benchmark or production recommendation.

## What this repo contains

- `decision_models_cloudflare_exploration.py` — the main experiment, converted from a Colab notebook into a runnable Python script.

## Why this project exists

The idea came from reading about Jev and decision models, where the model is asked to score or choose among valid options rather than generate free-form text.

The experiment asks a practical question: can a decision model provide structured, typed judgments that are useful inside software workflows?

The comparison focuses on a support triage scenario where the same input is processed by:

- a decision model with native option probabilities
- an LLM constrained to JSON output

This is useful for understanding the difference between:

- decision-first model behavior
- generative-response styling

## Core experiment

The script defines business policy and a set of sample customer messages. For each case, it asks both models the same questions:

- `team`
- `next_step`
- `urgent`

The expected policy is defined in code and used as a custom rubric, not as a public benchmark. The notebook also records provider responses, timings, and some probability outputs when available.

## Setup

You need:

- a Cloudflare account
- a Workers AI API token
- access to the relevant models

Set the following values in your environment or in Colab Secrets:

- `CLOUDFLARE_ACCOUNT_ID`
- `CLOUDFLARE_API_TOKEN`

Example:

```bash
export CLOUDFLARE_ACCOUNT_ID="your_account_id"
export CLOUDFLARE_API_TOKEN="your_api_token"
```

The script checks for these values and will prompt if they are missing.

## Running the experiment

Run the script as a notebook or Python file:

```bash
python decision_models_cloudflare_exploration.py
```

If you are using Google Colab, you can store the values in Colab Secrets and allow the notebook to access them.

## Notes

- This project is for experimentation and learning.
- It does not claim that one model is universally better.
- The script is designed to capture the raw model responses and compare behavior on a small custom set of examples.
- The focus is on the shape of the decision output and how the model reasons within constrained options.

## Sources and inspiration

- TypeSafe Jev introduction: https://typesafe.ai/blog/introducing-system-one-models-and-jev
- Cloudflare Clef introduction: https://blog.cloudflare.com/clef-decision-models/
- Cloudflare Workers AI API: https://developers.cloudflare.com/workers-ai/get-started/rest-api/
- Cloudflare Clef-flash model docs: https://developers.cloudflare.com/workers-ai/models/clef-flash/
- Cloudflare Qwen3 model docs: https://developers.cloudflare.com/workers-ai/models/qwen3-30b-a3b-fp8/

## License

This repository currently does not declare a formal license. If you plan to reuse or extend it, check whether a license is intended before publishing or distributing the code.

## Disclaimer

This is a personal research experiment and not an official benchmark, product recommendation, or production system design.
