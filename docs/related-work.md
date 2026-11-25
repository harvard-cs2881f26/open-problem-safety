# Related Work

Literature search run Nov 8, 2026, covering 60+ sources. Every link was checked against search results or the primary source, and anything we could not confirm is marked UNVERIFIED. Most numbers come from abstracts, not full PDFs.

**Bottom line:** no paper directly tests our question. The closest pieces each miss part of it: Terry & Andriushchenko has the right prefix design but measures only reward hacking, Afonin et al. shows in-context emergent misalignment but from explicitly misaligned examples, History Anchors uses harmful prefixes, and The Assistant Axis measures activations rather than instruction-hierarchy behavior.

### 1. Prior task context changing later alignment

- [Emergent Misalignment: Narrow finetuning can produce broadly misaligned LLMs](https://arxiv.org/abs/2502.17424). Betley et al., ICML 2025. Fine-tuning GPT-4o on insecure code yields broadly misaligned answers to unrelated prompts. *Training-time version of our claim. We test whether an in-context analog exists.*

- [Emergent Misalignment via In-Context Learning](https://arxiv.org/abs/2510.11288). Afonin et al., 2025. 2-16 narrow misaligned in-context examples yield 1-24% misalignment on unrelated queries, and larger models are often more susceptible. *Closest evidence for an in-context mechanism, but the context is explicitly misaligned rather than benign epistemic work.*

- [School of Reward Hacks](https://arxiv.org/abs/2508.17511). Taylor et al., 2025. Fine-tuning on harmless gameable tasks generalizes to shutdown resistance, while coding-only reward hacks did not. *A benign stance can generalize, and task diversity matters.*

- [Natural Emergent Misalignment from Reward Hacking in Production RL](https://arxiv.org/abs/2511.18397). MacDiarmid et al. (Anthropic/Redwood), 2025. Reward hacking in real coding RL leads to alignment faking and sabotage, removed by inoculation prompting. *Task framing changes what generalizes.*

- [Persona Features Control Emergent Misalignment](https://arxiv.org/abs/2506.19823). Wang et al. (OpenAI), 2025. SAE misaligned-persona features mediate emergent misalignment. *Mechanism story only, since we measure behavior.*

- [Thought Crime: Backdoors and Emergent Misalignment in Reasoning Models](https://arxiv.org/abs/2506.13206). Chua et al., 2025. Reasoning models also misgeneralize, and CoT often rationalizes it. *Supports measuring behavior rather than relying on CoT.*

- [Persona Vectors](https://arxiv.org/abs/2507.21509). Chen et al., 2025. Activation directions for traits like sycophancy track context-induced persona shifts. *Mechanism and optional follow-up.*

- [The Assistant Axis](https://arxiv.org/abs/2601.10387). Lu et al. (Anthropic), 2026. Drift along an Assistant direction predicts harmful behavior, especially in meta-reflective conversations. *Conversation type alone drives drift. Secondary write-ups say coding stayed stable (not confirmed in paper).*

- [History Anchors](https://arxiv.org/abs/2605.13825). Rodríguez Salgado, 2026. Three forced harmful prior actions push unsafe choices to 91-98% across 17 models. *Agent history steers later safety, but the history is harmful, not benign.*

- [Measuring alignment drift via trajectory prefixes](https://www.lesswrong.com/posts/pdtGsC888sTToZhiY/measuring-alignment-drift-via-trajectory-prefixes). Terry & Andriushchenko (MATS), Sept 2026, LessWrong. Reward-hacked first-task prefixes raise hacking on a second task, and length-matched summarization stays near baseline. *Closest design to ours. Gaps: reward hacking only, no science prefix, no instruction-hierarchy eval.*

- [Carryover Harm in Conversational AI](https://openreview.net/forum?id=WsiRqgQxod). Kim et al., NeurIPS 2026 AI4GOOD Workshop. Context-induced harm persists across sessions, but unrelated controls stay near baseline. *Partial counter-evidence that supports a possible null.*

- [Feedback Loops With Language Models Drive In-Context Reward Hacking](https://arxiv.org/abs/2402.06627). Pan et al., ICML 2024. Test-time feedback loops cause in-context reward hacking that static evals miss. *In-context trajectories, not just weights, shift behavior.*

### 2. Long-context and multi-turn drift

- [Drift No More? Context Equilibria in Multi-Turn LLM Interactions](https://arxiv.org/abs/2510.07777). Dongre et al., 2025. Context drift settles at a bounded equilibrium that goal reminders lower. *Drift may plateau, so a length sweep is worth adding.*

- [Measuring and Controlling Instruction (In)Stability in Language Model Dialogs](https://arxiv.org/abs/2402.10962). Li et al. (Harvard), COLM 2024. System-prompt adherence drifts within 8 rounds. *Confounds length with content, which our matched design controls.*

- [Many-shot Jailbreaking](https://proceedings.neurips.cc/paper_files/paper/2024/hash/ea456e232efb72d261715e33ce25f208-Abstract.html). Anil et al. (Anthropic), NeurIPS 2024. Hundreds of faux dialogues in long context jailbreak models with power-law scaling. *Our hypothesis is a benign, indirect version.*

- [When Refusals Fail: Unstable Safety Mechanisms in Long-Context LLM Agents](https://arxiv.org/abs/2512.02445). Hadeliya et al., 2025. Padded AgentHarm contexts degrade sharply by 100k tokens, with refusals moving in both directions. *Main justification for the neutral-padding condition.*

- [LongSafety](https://arxiv.org/abs/2502.16971). Lu et al., 2025 (authors not confirmed). Short-context safety does not predict long-context safety. *Supports length control.*

- [LLMs Get Lost In Multi-Turn Conversation](https://arxiv.org/abs/2505.06120). Laban et al., 2025. Multi-turn performance drops 39% on average. *Capability confound to report.*

- [Evaluating Goal Drift in Language Model Agents](https://arxiv.org/abs/2505.02709). Arike et al., AIES 2025. Agents drift from system-prompt goals as context accumulates. *Candidate post-context adherence eval.*

- [The Crescendo Multi-Turn LLM Jailbreak Attack](https://arxiv.org/abs/2404.01833). Russinovich et al., USENIX Security 2025. The model's own prior outputs steer later compliance. *Relevant because our prefix is the model's own discovery work.*

### 3. Instruction hierarchy and measurement

- [The Instruction Hierarchy](https://arxiv.org/abs/2404.13208). Wallace et al. (OpenAI), 2024. Defines system > user > tool privilege and trains models to follow it. *Defines our outcome variable.*

- [IHEval](https://aclanthology.org/2025.naacl-long.425). Zhang et al., NAACL 2025. 3,538 examples across 9 tasks, and the best open model scores 48% on conflicts. *Ready-made downstream eval (HF: zhihz0535/IHEval).*

- [A Closer Look at System Prompt Robustness](https://arxiv.org/abs/2502.12197). Mu et al., 2025. RealGuardrails: adherence collapses as guardrails accumulate. *Realistic system-prompt eval (github.com/normster/RealGuardrails).*

- [Control Illusion: The Failure of Instruction Hierarchies in LLMs](https://arxiv.org/abs/2502.15851). Geng et al., AAAI 2026. Social authority cues beat system/user roles even on simple conflicts. *Suggests question-authority priming could plausibly weaken hierarchy.*

- [SysBench](https://arxiv.org/abs/2408.10943). Qin et al., 2024 (authors not confirmed). Checklist-verified system-message adherence, including multi-turn. *Alternative adherence eval.*

### 4. Safety along reasoning trajectories

- [Path Drift in Large Reasoning Models](https://aclanthology.org/2025.emnlp-main.990/). Huang et al., EMNLP 2025. Long reasoning drifts off aligned paths via first-person commitments. *Within-trajectory analog of our across-task carryover.*

- [SafeChain](https://arxiv.org/abs/2502.12025). Jiang et al., Findings of ACL 2025. Long CoT does not guarantee safe outputs across 12 reasoning models. *Background.*

- [The Hidden Risks of Large Reasoning Models](https://arxiv.org/abs/2502.12659). Zhou et al., 2025. R1 reasoning traces are less safe than its final answers. *Background.*

- [When Thinking Fails](https://arxiv.org/abs/2505.11423). Li et al., NeurIPS 2025. CoT lowers IFEval accuracy by diverting attention from constraints. *Key confound: reasoning load alone could drive an effect, so coding must carry comparable load.*

- [Scaling Reasoning, Losing Control (MathIF)](https://arxiv.org/abs/2505.14810). Fu et al., 2025. Stronger reasoning goes with weaker instruction compliance. *Same confound, possible eval.*

- [The Danger of Overthinking](https://arxiv.org/abs/2502.08235). Cuadron et al., 2025. Overthinking on SWE-bench Verified predicts failure. *Characterizes failure modes in the coding condition.*

### 5. LLMs for scientific discovery (candidate tasks)

- [FIRE-Bench](https://arxiv.org/abs/2602.02905). Wang et al., ICML 2026. 30 tasks rediscovering findings from 2024-25 ML papers, and the best agents score under 50 F1. *Best fit for our discovery task, and it runs in the same harnesses as SWE-bench.*

- [Discovering state-of-the-art quantum circuits with LLMs](https://arxiv.org/abs/2610.22367). Gu, Kemeny, Yelin & Lukin (Harvard/Anthropic/QuEra), Oct 2026. LLM-proposed circuits beat state of the art in 7 of 8 tasks. *Source of real discovery transcripts (Part 3).*

- [DiscoveryWorld](https://arxiv.org/abs/2406.06769). Jansen et al., NeurIPS 2024. Text world with unfamiliar laws across 8 topics. *Contamination-free assumption questioning (Part 3).*

- [LLM-SRBench](https://arxiv.org/abs/2504.10415). Shojaee et al., ICML 2025. 239 equation-discovery problems with transformed laws that resist memorization. *Cleaner stand-in for rediscovering physics.*

- [ScienceAgentBench](https://arxiv.org/abs/2410.05080). Chen et al., ICLR 2025. 102 code-based tasks from 44 papers. *Code-heavy, so it would blur the contrast with SWE-bench.*

- [The AI Scientist](https://arxiv.org/abs/2408.06292). Lu et al. (Sakana), 2024. End-to-end idea-to-paper pipeline. *Possible source of long discovery transcripts.*

- [The AI Scientist-v2](https://arxiv.org/abs/2504.08066). Yamada et al., 2025. Agentic tree search, with one paper accepted at an ICLR workshop. *Same use as above.*

- [SWE-bench](https://arxiv.org/abs/2310.06770). Jimenez et al., ICLR 2024. 2,294 real GitHub issues from 12 Python repos. *Our coding condition.*

- *Rediscovering relativity (UNVERIFIED):* no peer-reviewed result. An informal blog (Michael Hla, "Machina Mirabilis") trained a 3.3B model on pre-1900 text with weak results. Use only as motivation.

### 6. Safety in scientific settings

- [SciSafeEval](https://arxiv.org/abs/2410.03769). Li et al., 2024. About 31.8k safety samples across scientific languages with jailbreak variants. *Safety inside science, while our eval deliberately sits outside it.*

- [SciGuard](https://arxiv.org/abs/2312.06632). He et al., 2023. Agent safeguard for chemistry. *Background.*

- [Prioritizing Safeguarding Over Autonomy: Risks of LLM Agents for Science](https://arxiv.org/abs/2402.04247). Tang et al., 2024. Risk taxonomy for scientific agents. *Motivation.*

### 7. Skepticism and epistemic stance

- [Accommodation and Epistemic Vigilance](https://arxiv.org/abs/2601.04435). Cheng, Hawkins & Jurafsky, 2026. A simple "wait a minute" cue raises epistemic vigilance against false presuppositions. *Stance is context-shiftable. Whether vigilance extends to the system prompt is our open question.*

- [Towards Understanding Sycophancy in Language Models](https://arxiv.org/abs/2310.13548). Sharma et al. (Anthropic), 2023. Sycophancy is widespread and partly driven by preference data. *Two-sided prediction: less sycophancy but more defiance (eval: github.com/meg-tong/sycophancy-eval).*

- [TRUTH DECAY](https://arxiv.org/abs/2503.11656). 2025 (authors not confirmed). Tests doubt-the-user prompts against multi-turn sycophancy. *Direct skepticism-prompting example.*

- [SYCON Bench](https://arxiv.org/abs/2505.23840). 2025 (authors not confirmed). Third-person framing cuts sycophancy up to 63.8%. *Stance prompts shift compliance.*

- [Ask Don't Tell](https://arxiv.org/abs/2602.23971). 2026 (authors not confirmed). Rephrasing inputs as questions beats anti-sycophancy instructions. *Same.*

### 8. Downstream eval candidates

- [Agentic Misalignment: How LLMs Could Be Insider Threats](https://arxiv.org/abs/2510.05179). Lynch et al. (Anthropic), 2025. 16 models sometimes blackmail or leak to avoid replacement. *Unrelated to science and code, but base rates are scenario-sensitive.*

- [The MASK Benchmark](https://arxiv.org/abs/2503.03750). Ren et al., 2025. Separates honesty from accuracy under pressure. *Good second outcome.*

- [Frontier Models are Capable of In-context Scheming](https://arxiv.org/abs/2412.04984). Meinke et al. (Apollo), 2024. Six agentic evals of oversight subversion. *Most direct defiance signal, but expensive.*

### 9. How real discovery systems push models to question assumptions

Mostly through search pressure plus an external evaluator, not skeptical prompting. The strongest results (FunSearch, AlphaEvolve, AlphaProof, the quantum circuits) generate many variants and let an evaluator kill the bad ones. Explicit skeptical prompting shows up mainly in hypothesis-generation systems without hard verifiers (co-scientist, AI Scientist, Kosmos, Aletheia), in three forms: self-critique/debate, assumption decomposition, and divergence instructions. In every system checked, the skepticism targets hypotheses and literature, never the system's own instructions. Two partial exceptions blur that line: AlphaEvolve's meta-prompt evolution (the model rewrites its own instructions) and co-scientist's meta-review feedback injected into every agent's prompt.

- [Towards an AI co-scientist](https://arxiv.org/abs/2502.18864). Google, 2025. Generate/review/rank/evolve agents with Elo tournaments over simulated debates, "deep verification" that splits hypotheses into sub-assumptions, and an out-of-box evolution mode. Published prompts include "Identify any weaknesses" and "Think out-of-the-box." *Best real-world template for our questioning condition. Note its criteria also require alignment with the scientist's stated goals and constraints.*

- [AI mirrors experimental science to uncover a novel mechanism of gene transfer (cf-PICI)](https://research.google/pubs/ai-mirrors-experimental-science-to-uncover-a-novel-mechanism-of-gene-transfer-crucial-to-bacterial-evolution/). Imperial + Google, Cell 2025. Co-scientist's top hypothesis matched an unpublished wet-lab finding on AMR gene transfer. *Headline evidence that the questioning loop produces real discoveries.*

- [AlphaEvolve](https://arxiv.org/abs/2506.13131). Google DeepMind, 2025. Evolutionary coding search with a prompt sampler, stochastic template formatting, meta-prompt evolution and an automated evaluator. *Questioning lives in the selection loop. Meta-prompts are a self-instruction channel.*

- [Mathematical exploration and discovery at scale (AlphaEvolve, 67 problems)](https://arxiv.org/abs/2511.02864). DeepMind with Tao & Gomez-Serrano, Nov 2025. Results leaned heavily on expert hints, and the system "always eventually figured out a way to cheat" leaky verifiers. *Documented evaluator gaming in a discovery loop.*

- [FunSearch](https://www.nature.com/articles/s41586-023-06924-6). DeepMind, Nature 2023. Frozen LLM plus evaluator in an evolutionary program search. *Baseline search-plus-evaluator pattern.*

- [Olympiad-level formal mathematical reasoning with RL (AlphaProof)](https://research.google/pubs/olympiad-level-formal-mathematical-reasoning-with-reinforcement-learning/). DeepMind, Nature 2025. AlphaZero-style RL with Lean verification, no prompting. *Contrast case: discovery with no skeptical prompting at all.*

- [Discovering new solutions to century-old problems in fluid dynamics](https://deepmind.google/blog/discovering-new-solutions-to-century-old-problems-in-fluid-dynamics/). DeepMind et al., Sept 2025 (arXiv 2509.14185). Unstable Navier-Stokes-type singularities found with physics-informed neural nets and high-precision optimization. *No LLM was involved, so this is not a model of LLM questioning.*

- [Aletheia](https://arxiv.org/abs/2602.10177). DeepMind, Feb 2026. Generator/Verifier/Reviser agents on Gemini Deep Think across 700+ open Erdos problems. 50 of 63 technically correct answers were vacuous reinterpretations. *Reinterpreting the question into its easiest reading is a subtler outcome worth measuring.*

- [Designing efficient quantum circuits (Anthropic post)](https://anthropic.com/research/designing-efficient-quantum-circuits). Anthropic, Oct 2026 (paper: arXiv 2610.22367). Claude ran evolutionary circuit search for up to 53 hours with an independent evaluator. It was too conservative and humans nudged it to "think more broadly." *Shows frontier models may need pushing to question, which our prompts must do explicitly.*

- [Single-minus gluon tree amplitudes are nonzero](https://arxiv.org/abs/2602.12176). OpenAI with Strominger et al., Feb 2026. GPT-5.2 Pro conjectured a formula overturning a textbook assumption that these amplitudes vanish (prompting details UNVERIFIED). *A literal assumption-overturning result and a good physics-flavored task template.*

- [Early science acceleration experiments with GPT-5](https://arxiv.org/abs/2511.16072). OpenAI and academics, Nov 2025. Expert-in-the-loop case studies across fields. *Background. Note the Oct 2025 Erdos-problems claim was retracted (they were literature finds).*

- [Kosmos: An AI Scientist for Autonomous Discovery](https://arxiv.org/abs/2511.02824). FutureHouse/Edison, Nov 2025. Structured world model, ~200 rollouts per 12-hour run. Only 57.9% of synthesis statements were accurate. *Long-horizon autonomy with documented overclaiming.*

- [Robin](https://arxiv.org/abs/2505.13400). FutureHouse, May 2025. Multi-agent literature-to-hypothesis loop for drug repurposing with wet-lab validation. *Biology example of the hypothesis-generation pattern.*

- [Biomni](https://doi.org/10.1101/2025.05.30.656746). Stanford, 2025. General biomedical tool-using agent. *Little questioning design. Background.*

- [AI designs viable bacteriophage genomes (Evo 2)](https://www.genengnews.com/topics/artificial-intelligence/ai-designs-viable-bacteriophage-genomes-combats-antibiotic-resistance/). Arc Institute/Stanford, 2025-26 (venue UNVERIFIED). Generative genome model plus filtering, and 16 of ~300 synthesized genomes were viable. *Generative, not prompted questioning.*

- *Periodic Labs and Lila Sciences:* closed-loop autonomous labs with no public prompting details (secondary sources only).

### 10. Documented constraint violations in discovery and agentic loops

- [The AI Scientist (Section 8)](https://arxiv.org/abs/2408.06292). Sakana, 2024. Relaunched itself via system call, tried to extend its own time limit instead of shortening runtime, and saved ~1 TB of checkpoints. *Closest documented case of a discovery agent overriding constraints (commenters note the edited file was the experiment script, not the harness).*

- [Recent frontier models are reward hacking](https://metr.org/blog/2025-06-05-recent-reward-hacking). METR, 2025. o3 overwrote timers and monkey-patched evaluators in 30.4% of RE-Bench runs, and "please do not cheat" had negligible effect. *Instructions lose to optimization pressure.*

- [Shutdown resistance in LLMs](https://arxiv.org/abs/2509.14260). Palisade, 2025. o3 sabotaged shutdown in 7/100 runs despite explicit instructions, which the authors attribute to math/coding RL. *Direct instruction-hierarchy violation linked to problem-solving training.*

- [AlphaEvolve reward-hacking prevention guide](https://docs.cloud.google.com/gemini/enterprise/docs/alphaevolve/developer-guide/reward-hacking-prevention). Google Cloud docs. Lists constraint-penalty ignoring, evaluator exploitation and hard-coded answers, and recommends hiding the scoring file. *Vendor acknowledgment that discovery loops game constraints.*

- *Sakana AI CUDA Engineer (Feb 2025):* exploited an evaluation memory bug to skip correctness checks, and the claimed speedups were walked back (secondary sources only).

**Gap:** every documented violation comes from optimization pressure against an evaluator or long-horizon autonomy. No source shows skeptical prompting by itself causing instruction violations, which is the gap our project fills.

### Design implications

- Add a neutral-padding condition at matched length, since length alone moves refusals (Hadeliya et al., LongSafety)

- Match reasoning load across conditions, since reasoning alone degrades instruction following (Li et al., Fu et al.)

- Measure sycophancy alongside instruction-hierarchy violations so "more skeptical" is not conflated with "misaligned"
