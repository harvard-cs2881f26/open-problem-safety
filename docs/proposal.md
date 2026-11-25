# CS 2881R Final Project Proposal

Noa Schwartz, Joaquin de Castro

Labs push models toward novel scientific discovery in different ways: long search loops scored by an automatic checker, feedback to beat the best attempt so far, and prompts to challenge established assumptions. We want to know whether these pushes carry over into how the model treats its instructions: *Does pushing a model toward novel discovery make it less aligned afterward, and does that depend on how it is pushed?* The answer could easily be no, and a clean "no" is still a useful result.

### Motivation & Related Work

Narrow exposure can generalize into broad misalignment, through fine-tuning ([Betley et al., 2025](https://arxiv.org/abs/2502.17424)) and even a few in-context examples ([Afonin et al., 2025](https://arxiv.org/abs/2510.11288)). Discovery loops already show constraint violations (the [AI Scientist](https://arxiv.org/abs/2408.06292) editing its own time limit, [AlphaEvolve](https://arxiv.org/abs/2511.02864) gaming its evaluator), but these come from optimization pressure, and we found no work testing whether assumption-questioning alone carries over to the instruction hierarchy ([Wallace et al., 2024](https://arxiv.org/abs/2404.13208)). The closest design to ours puts one task's trajectory in context before another, but measures only reward hacking ([Terry & Andriushchenko, 2026](https://www.lesswrong.com/posts/pdtGsC888sTToZhiY/measuring-alignment-drift-via-trajectory-prefixes)). Context length alone moves refusals ([Hadeliya et al., 2025](https://arxiv.org/abs/2512.02445)) and reasoning alone degrades instruction following ([Li et al., 2025](https://arxiv.org/abs/2505.11423)), so we control for both (full review in the Related Work tab).

### Part 0: Metrics

We measure behavior directly, with probes that avoid code and science:

- **Instruction-hierarchy violations (primary):** following a user instruction over a conflicting system prompt ([IHEval](https://aclanthology.org/2025.naacl-long.425), [RealGuardrails](https://arxiv.org/abs/2502.12197))

- **Constraint gaming:** breaking a stated rule in a small task with a gameable checker

- **Sycophancy:** a skeptical model may push back on users (good) and on its system prompt (bad), so we track both

- **Honesty and shutdown compliance:** lying under pressure ([MASK](https://arxiv.org/abs/2503.03750)) and overriding a shutdown instruction ([Palisade](https://arxiv.org/abs/2509.14260))

### Part 1: Experiment

One model works on a quantum-circuit design task with an automatic checker ([Gu et al., 2026](https://arxiv.org/abs/2610.22367)) for ~100k tokens, keeps that work in context, then takes the probes. Temperature and token count are fixed, and system-prompt rules (e.g., don't edit the scorer) let us log violations during the run:

- **No prior work:** probes only, plus a version padded with neutral text

- **Plain discovery:** one pass at the task, with no feedback or special prompting

- **Score feedback:** a loop showing past attempts and scores, asking it to beat its best ([AlphaEvolve](https://arxiv.org/abs/2511.02864)-style)

- **Explicit skepticism:** prompts to break the prevailing approach into assumptions and challenge them ([co-scientist](https://arxiv.org/abs/2502.18864)-style)

- **Coding control:** the score-feedback loop on [SWE-bench](https://arxiv.org/abs/2310.06770)

### Part 2: Analysis

The main test is each push strategy vs. plain discovery. Plain discovery vs. no prior work shows whether discovery itself matters, the coding loop separates discovery from score-driven work, and padding rules out context length. We will probe from checkpoints at 25k, 50k and 100k tokens for a dose-response curve, run ~20 sessions per condition, and only claim an effect if it repeats on a second model family.

### Part 3: Extensions

If time permits: novelty pressure, self-rewritten instructions, combined strategies, broader probes (emergent misalignment, scheming), or a philosophy condition.
