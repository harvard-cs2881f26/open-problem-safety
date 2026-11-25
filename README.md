# Does Scientific Discovery Spill Over into Instruction-Following?

This project tests whether the prompts labs use to push models toward novel scientific discovery change how those models follow their spec on unrelated requests later in the same conversation. We make no claims that any discovery happens.

We compare a stateless baseline and an analysis-only Discussion control against three push types:

- **Optimization:** a score loop showing past attempts and asking the model to beat its best (FunSearch, AlphaEvolve, OpenEvolve, autoresearch).
- **Novelty:** pushing for new, qualitatively different approaches with encouragement after failure (Anthropic's Riemann zeta and quantum circuit work, Sakana's AI Scientist, co-scientist).
- **Critique:** a ladder from self-verification to falsification to attacking the field's consensus (co-scientist reflection, DeepMind's Aletheia, Stanford's POPPER).

Each push runs at three levels of persistence on 40 open problems from OpenProblemBench, using gpt-oss-120b. After each conversation we run OpenAI's Model Spec Evals and break results down by section (chain_of_command, stay_in_bounds, seek_truth and so on) to see which kind of push moves which behavior.

CS 2881R (AI Safety & Alignment) final project, Noa Schwartz + Joaquin de Castro.

- Proposal (earlier draft, predates this design): [Google Doc](https://docs.google.com/document/d/1SY5eFXU_2OBCh5n_4oEPYj7Ttb9LhUdaTuhvpOrlnoo/edit) (tabs: Proposal, Related Work)
- Local copies: [`docs/proposal.md`](docs/proposal.md), [`docs/related-work.md`](docs/related-work.md)
- Origin: office hours, Nov 5, 2026 (Granola: "Scientific discovery with LLMs")

## Design principles

From office hours with Boaz (Nov 5, 2026), still applied in this design:

- Measure behavior directly, not through activations
- Leave the push conversation in context, then evaluate on requests unrelated to it
- Keep the contribution narrow: reuse existing problems (OpenProblemBench) and evals (Model Spec Evals) rather than building new benchmarks
- A clean "no" is a good result. A surprising "yes" needs strong evidence

## Layout (planned)

```
docs/        proposal + literature review
harness/     push prompts (optimization / novelty / critique x 3 persistence levels), baseline + Discussion control, conversation runner
evals/       Model Spec Evals config + per-section scoring
results/     raw transcripts + scored outputs
analysis/    notebooks / plots
```
