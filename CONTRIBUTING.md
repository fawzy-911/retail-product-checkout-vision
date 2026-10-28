# Contributing

Contributions that improve reproducibility, runtime, evaluation, or generalization to checkout scenes are welcome.

## Before opening a pull request

1. Keep the official RPC train/validation/test boundaries intact.
2. Never commit dataset files, credentials, Kaggle tokens, or trained checkpoints.
3. Label quick-profile metrics as exploratory and do not tune on test data.
4. Record the exact profile, image counts, model weights, package versions, accelerator, and random seed for experiments.
5. When changing the notebook, validate its JSON structure and Python cell syntax. If execution depends on Kaggle data/GPU, state clearly which cells were actually run.
6. Add research claims with a direct paper or official documentation reference.

## Scope for model changes

Prefer measured ablations over untracked changes to augmentation, thresholds, image size, or architecture. Report both detector metrics and checkout-count metrics when possible.
