# Theory Lab: Multi-Agent AI for Mathematical Research

Theory Lab is a multi-agent AI workflow for mathematical research. It gives LLM agents separate roles in developing mathematical arguments, checking proofs independently, and reviewing the evidence. This repository shares the architecture, role instructions, and proposed evaluation.

## Why we built it

In mathematical research, a plausible argument is only the beginning. We still need to check the assumptions, find the step that does not follow, and work out whether a counterexample actually applies. A long conversation can make that work difficult to follow: an early mistake can become an unstated assumption, and a revised claim can quietly take the place of the original one.

Theory Lab grew out of a simple idea: give construction and criticism different jobs, let them start independently, and keep a written record of the evidence behind each conclusion.

The workflow has been useful in our own research. We recommend trying it, while being clear about what that recommendation means: this is personal experience, not a benchmark result.

## How it works

The figure shows the configuration proposed for the evaluation in the manuscript. The role instructions describe the more general workflow.

![Theory Lab's proposed evaluation: the Builder and Verifier work independently, save their reports before review, and pass the evidence to the Director. The final report is evaluated separately.](assets/theory-lab-workflow.png)

**The Builder develops the argument.** It makes the statement precise, lists the assumptions, tries to prove it, and looks for ways it might fail.

**The Verifier starts independently.** It receives the same starting material, but does not see the Builder's current work. It tries its own derivation or looks for a counterexample. Only after both reports are finished and saved does it read the Builder's argument and check it step by step.

**The Director reviews the evidence.** It reads both reports and the later critique, identifies the exact disagreement, and decides what belongs in the shared record. A valid counterexample matters more than agreement between several agents. Significant changes to the research objective go back to the human researcher.

The next round starts from that updated record. Useful lemmas are kept with their assumptions and supporting arguments. Failed attempts are kept too, so the same mistake does not have to be rediscovered.

## Why these choices might help

We separate the first attempts because a checker that sees the proposed proof immediately may follow the same mistaken path. An independent attempt gives the later review a second starting point. This is the reason for the separation, not a claim that separate agents always make independent errors.

We delay comparison until both reports are saved so that we can distinguish what each agent found on its own from what it learned during review.

We keep exact statements and earlier versions because changing an assumption changes the claim. A corrected theorem should not erase the counterexample to the original one. We also distinguish a computational check from a proof: testing a finite set of cases does not establish an unrestricted statement.

These choices make the reasoning easier to inspect. Whether they improve research outcomes enough to justify the extra work is still an empirical question.

## Cogentic, reproducibility, and evaluating the architecture

We wrote the first Theory Lab draft on **September 25, 2026**, before [Cogentic v1](https://arxiv.org/abs/2609.40324v1) appeared on **September 30, 2026**. Theory Lab was developed independently. These dates describe our draft and their public release; they do not establish when Google's internal work began.

Cogentic uses related ideas, including coordinated proof attempts, adversarial verification, and a record of checked intermediate results. Its paper reports expert-checked results on five research problems. These mathematical results deserve attention. They also leave two questions open for readers: how to reproduce the system, and how much its architecture contributes.

- **The appendix supplies task prompts.** [Appendix A](https://arxiv.org/html/2609.40324v1) shows what the system was asked to investigate. It does not provide the complete role prompts for the orchestrator, provers, and verifiers. Readers trying to rebuild the workflow would still need to supply those instructions.
- **Important implementation materials are missing from the linked release.** As of **October 3, 2026**, we could not find links to a complete system implementation, full role prompts, run configurations, or execution logs in the v1 paper or its [official project page](https://sites.google.com/view/cogentic). Readers trying to reproduce the system must fill in important implementation details themselves.
- **Successful cases do not establish the architecture's contribution.** The [v1 paper](https://arxiv.org/html/2609.40324v1) does not report comparisons with simpler workflows under matched resource budgets or experiments that remove individual components. Those comparisons are needed to distinguish gains from the organization of the agents, the underlying model, and additional computation.

For Theory Lab, we publish reusable role prompts for the [Builder](protocols/BUILDER.md), [Verifier](protocols/VERIFIER.md), and [Director](protocols/DIRECTOR.md), alongside the [rules for recording claims](protocols/STATUS_POLICY.md) and the [steps for running the workflow](ARCHITECTURE.md). These describe what each agent should do, when it may read another agent's work, and how its conclusions are reviewed. We want readers to be able to inspect, adapt, and implement the design. The repository does not yet include an executable runner.

Our [first-draft manuscript](docs/llm_theory_lab_first_draft.pdf) also proposes ways to test the architecture: compare it with an iterative single agent and an independent panel under common resource limits; vary when agents see each other's work and how review is conducted; grade correctness separately; and report failures alongside successes. The aim is to learn which design choices help, how much they help, and what they cost. We invite others to run these experiments, challenge the comparisons, or propose better evaluations.

The same standard applies to us. **We are sharing prompts and an evaluation proposal; we have not established that Theory Lab outperforms simpler methods.** The proposed model experiments have not been run, and we have not found a satisfactory benchmark for the workflow's practical research value. Our positive experience motivates these tests, but cannot replace them.

## Try it

Start with a bounded task and the same reading material for the Builder and Verifier. Keep their first attempts separate, save both reports before sharing, and then run the review. Read the Director's conclusions yourself, especially when an assumption or the objective has changed.

- [Builder instructions](protocols/BUILDER.md)
- [Verifier instructions](protocols/VERIFIER.md)
- [Director instructions](protocols/DIRECTOR.md)
- [How claims are recorded and reviewed](protocols/STATUS_POLICY.md)
- [Architecture details](ARCHITECTURE.md)
- [Full first-draft manuscript: workflow and proposed evaluation](docs/llm_theory_lab_first_draft.pdf)

The manuscript retains the original experimental plans: task construction, comparison methods, resource budgets, analysis, and an optional evaluation of longer mathematical arguments. These are proposals, not a completed validation of the workflow. The public revision keeps the original paper format and figures while revising the prose and removing personal details.

This repository contains the architecture, role instructions, and manuscript, but no executable runner. Keeping the agents' work separate requires actual access controls; a prompt alone cannot enforce that. An accepted claim remains open to correction.

## Use these ideas and build on them

We have not found a fully satisfactory way to evaluate the practical research value of a workflow like this. The experiments in the draft are starting points. If you have a better benchmark, a simpler comparison, or a different way to test the design, we welcome you to pursue it.

You are welcome to use and adapt these protocols and configurations, and to run or improve the proposed experiments. If your work builds on them, please cite this repository or the manuscript and identify the version you used. The repository includes a [citation file](CITATION.cff); a BibTeX entry is provided below.

```bibtex
@misc{theorylab2026,
  author = {Tang, Jiaqi and Li, Jingsu},
  title = {Theory Lab: Multi-Agent AI for Mathematical Research},
  year = {2026},
  howpublished = {GitHub repository},
  url = {https://github.com/TanhJK728/AI4MATH-Multi-Agent-System},
  note = {First manuscript draft: September 25, 2026; public text revision: October 3, 2026}
}
```
