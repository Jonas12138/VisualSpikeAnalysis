# E001: Linear SVM baseline

## Status and question

- Status: **Planned; no analysis has been run.**
- Run date: Pending.
- Question: Can VISp spike counts distinguish two predefined natural images better than a majority-class predictor?
- Reference experiment: First baseline.
- Main comparison: Standardized linear SVM versus majority-class prediction, using identical samples and splits.
- Planned outcome: A verified feature matrix, reproducible split, and measured validation comparison. An improvement is a hypothesis, not a guaranteed result.

## Before running

- [ ] Record the session ID and verify that VISp and natural scenes are available.
- [ ] Choose two image IDs before inspecting decoding accuracy; document the selection rule.
- [ ] Specify unit quality filters and save ordered unit IDs.
- [ ] Specify the response window relative to stimulus onset and verify stimulus duration.
- [ ] Define development and final test partitions; save the presentation IDs and class counts.
- [ ] Verify alignment with a raster plot and preserve zero-spike presentations.
- [ ] Record the code commit, working environment, and run instructions.

## Features and model plan

Use one fixed-window spike count per selected unit for each presentation. Keep the unit ordering identical across all partitions.

1. Fit a majority-class predictor on training labels.
2. Fit a pipeline that standardizes features using training data and trains a linear SVM. Start with a predeclared `C=1.0` baseline; record the exact estimator and all settings actually used.
3. Evaluate both on the same validation partition, reporting accuracy, balanced accuracy, class counts, and a confusion matrix.
4. Run a documented shuffled-training-label control on development data. Preserve grouping or temporal structure when the evaluation protocol requires it; do not tune settings to make the control look favorable.
5. Leave the final test partition untouched. Further tuning or an RBF comparison belongs to a documented follow-up experiment.

## Reproduction record

| Item | Actual value |
| --- | --- |
| Session and image IDs | Pending |
| Unit filters and ordered unit-ID file | Pending |
| Response window and feature matrix shape | Pending |
| Split method, saved IDs, and per-class counts | Pending |
| Code commit and notebook/script | Pending |
| Environment versions and seeds | Pending |
| Complete estimator settings | Pending |
| Predictions, figures, and other artifact paths | Pending |

## Measured validation results

| Model | Accuracy | Balanced accuracy |
| --- | --- | --- |
| Majority-class baseline | Not measured | Not measured |
| Linear SVM | Not measured | Not measured |

- Confusion matrix: Pending.
- Shuffled-label control: Pending.
- Failures or unexpected behavior: None recorded; run not started.
- Interpretation: Pending actual results.
- Next step: Complete data selection and alignment checks above.
