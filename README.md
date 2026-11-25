# Does Scientific Discovery Spill Over into Instruction-Following?

CS 2881R (AI Safety & Alignment) final project, Noa Schwartz + Joaquin de Castro.

**Hypothesis (to test, not a finding):** asking an LLM to question assumptions during novel scientific discovery might also make it more likely to question its instructions afterward, showing up as more instruction-hierarchy violations on an unrelated evaluation.

- Proposal (source of truth): [Google Doc](https://docs.google.com/document/d/1SY5eFXU_2OBCh5n_4oEPYj7Ttb9LhUdaTuhvpOrlnoo/edit) (tabs: Proposal, Related Work)
- Local copies: [`docs/proposal.md`](docs/proposal.md), [`docs/related-work.md`](docs/related-work.md)
- Origin: office hours, Nov 5, 2026 (Granola: "Scientific discovery with LLMs")

## Design guidance from office hours (Boaz)

- Measure misalignment directly (behavior), not through activations
- Three base conditions with matched token counts, prior work left in context: no prior context / after scientific discovery / after SWE-bench
- Keep the eval unrelated to all prior tasks (no code-flavored alignment eval after coding)
- Keep the contribution narrow: reuse existing discovery tasks, simple harness, ~128k context
- A clean "no" is a good class project. A surprising "yes" needs strong evidence

## Layout (planned)

```
docs/        proposal + literature review
harness/     prefix generation (discovery / coding / padding) + eval runner
evals/       instruction-hierarchy + sycophancy eval configs
results/     raw transcripts + scored outputs
analysis/    notebooks / plots
```
