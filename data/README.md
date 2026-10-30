# Figure summary data

These tables accompany *LLM Theory Lab: Evidence Flow and the Cost of Structured Verification* (October 30, 2026). They are the saved descriptive inputs used for the paper's workflow-cost and matched-task figures.

## Population

The analysis contains 172 selected completed attempts from a 192-assignment study: S45, P44, F45, and E38. Selection uses completion status and the existing attempt selection before reading CTS outcomes. All included runs pass CTS. The paper describes the selection, measurements, and comparisons in full.

## Files

- `condition_summary.csv`: completed-run counts, CTS fractions, mean active minutes, mean admitted computation executions, and mean active minutes for each of four stages.
- `paired_task_means.csv`: saved matched task-and-repeat summaries used in the paired figure. Available matched repeats are averaged within each task; each task receives equal weight in the reported comparisons.

S is a continuing single agent. P is an independent solver panel with a continuing Integrator. F is the full Builder–Verifier–Director workflow. E uses the same role sequence with earlier Builder-report disclosure.

Active time sums native solver-stage intervals, including model and tool waits. Allocation, between-stage handoff, sealing, and cleanup are outside this measure. All workflows have common resource ceilings; their actual consumption differs.

## Provenance

The tables are unchanged copies from the empirical article's saved figure data, derived from `completed172_v1` for run `bvd_main_480s_20261008T204106719015Z`. The repository release reuses those results without rerunning models, grading, or statistical analysis. Column names and units are preserved from the article.

[Read the empirical paper](../docs/llm_theory_lab_empirical_article.pdf) · [Return to the results](../README.md#results-the-cost-of-structured-verification)
