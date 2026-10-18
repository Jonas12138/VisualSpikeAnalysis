# Experiment guide and index

An experiment is one documented question and a reproducible comparison. Record validation findings here; reserve final test evaluation for the selected pipeline.

## First-time workflow

1. Start with [the planned E001 baseline](experiments/E001-linear-baseline.md). For later experiments, copy [the experiment template](experiments/TEMPLATE.md) to a new file such as `experiments/E002-rbf-comparison.md`.
2. Fill in the question, planned change, data settings, and evaluation procedure **before** running the analysis.
3. Save or commit the code you intend to run. Record that code commit in the entry.
4. Run the analysis. Save settings, split IDs, ordered unit IDs, predictions, and figures with identifiable paths.
5. Fill in measured results, observations, failures, and the next step. If a run fails, record the failure; do not invent a score.
6. Add the experiment to the index below and commit the updated record.

Use a new ID when changing the main question, feature representation, model comparison, or split protocol. A preplanned hyperparameter search can belong to one experiment if you save its candidate settings and scores.

## Experiment index

No experiments have been run or measured by this setup.

| ID | Question | Status | Validation result | Record |
| --- | --- | --- | --- | --- |
| E001 | Can a linear SVM beat the majority-class baseline? | Planned | Not measured | [Baseline plan](experiments/E001-linear-baseline.md) |

## Illustrative entry: not a measured experiment

```text
ID: E001
Status: Planned
Question: Can VISp spike counts distinguish the two selected images?
Data: One session; session and image IDs must be entered before running.
Features: One count per unit in a fixed stimulus-aligned window.
Models: Majority-class predictor and standardized linear SVM.
Evaluation: Documented development split; final test set untouched.
Validation results: Pending.
Next step: Select data and verify spike-to-stimulus alignment.
```

## What to record for every run

- Code commit, environment versions, and run date.
- Session and image IDs, unit filters, ordered unit IDs, and feature window/binning.
- Actual split IDs or their saved file path and checksum, plus any random seeds.
- Model settings and any hyperparameter selection procedure.
- Validation metrics, class/sample counts, and baseline scores on the same partition.
- Artifact paths, limitations, unexpected behavior, and the next decision.

A useful observation explains the evidence. For example: "RBF improved validation accuracy on this split, but the difference was small; repeat the preplanned comparison before drawing a strong conclusion."

## Updating from GitHub later

1. Open the experiment record and choose **Edit** (the pencil icon).
2. Update its status, results, and observations using actual run output.
3. Choose **Commit changes** with a message such as `Record E001 validation results`.
4. Update this index with the same status and headline finding.

GitHub edits change documentation, not the code or data on your computer. Pull remote changes before continuing local edits. If a GitHub issue is created using the experiment form, use it to discuss the work; keep the reproducible record in `experiments/`.
