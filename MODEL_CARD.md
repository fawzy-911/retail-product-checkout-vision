# Model card

## Model

- **Task:** closed-set object detection for RPC retail product classes.
- **Baseline:** Ultralytics YOLO26n initialized from pretrained weights.
- **Training data:** RPC single-product exemplar split.
- **Selection data:** official RPC checkout validation split.
- **Test data:** official RPC checkout test split, opt-in and held out until final evaluation.

## Intended use

Educational and research experiments in retail product detection, object counting, and evaluation on the RPC dataset. Outputs may be used to inspect predictions and compare controlled experiments.

## Out-of-scope use

The model is not a production checkout or billing system. It should not independently charge a customer, resolve ambiguous SKUs, or make business decisions without verification. The predicted class is not a guaranteed SKU identity.

## Known limitations

- A domain gap separates single-product training images from multi-product checkout scenes.
- Occlusion, overlapping objects, reflections, blur, rotation, packaging redesigns, and class similarity can reduce accuracy.
- Closed-set detection does not reliably recognize unseen products.
- Confidence scores are not guaranteed calibrated probabilities.
- A correct monetary total requires a verified store catalog with SKU identity, price, and currency.
- Full-split training is resource-intensive and results vary with hardware, runtime, and dependency versions.

## Reporting requirements

Do not report a quick-profile result as a full-split benchmark. Record the profile, number of train/validation images, GPU, package versions, checkpoint, confidence threshold, detector metrics, count metrics, and any test protocol. Do not tune on the test set.
