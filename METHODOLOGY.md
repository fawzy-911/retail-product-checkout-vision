# Methodology

## Task definition

Given a checkout image, detect and classify the visible RPC product categories. A checkout prediction is also summarized as a per-class object count. Converting those predictions into a bill requires a second, store-specific mapping from the predicted class to a verified SKU and current price.

## Data protocol

The workflow preserves the official RPC split boundaries:

1. **Train:** single-item exemplar images used for detector fine-tuning.
2. **Validation:** cluttered multi-product checkout scenes used for checkpoint selection, operating-threshold selection, and iteration.
3. **Test:** held-out checkout scenes used only after model and threshold decisions are frozen.

The default profile uses the full train and validation splits. The quick profile samples within each split only to validate the software pipeline; its results must be labeled as exploratory. The test annotations are not loaded unless optional test evaluation is explicitly enabled.

## Annotation conversion

COCO category IDs are mapped once to contiguous model class indices. For each non-crowd annotation, the notebook clips the COCO `[x, y, width, height]` box to image bounds and writes the YOLO normalized center/size representation. The generated labels and image files are checked before training. Source image IDs are preserved in output filenames to support prediction-to-ground-truth matching.

## Model and training

The baseline fine-tunes the small pretrained Ultralytics YOLO26n detector with an explicit random seed, automatic batch sizing, mixed precision when supported, early stopping, and validation-based checkpoint selection. The `best.pt` checkpoint is used for downstream evaluation.

This is a baseline, not a claim that the model solves realistic automatic checkout. RPC's train images contain one product in a controlled view; checkout images contain many products with occlusion, clutter, and varied camera conditions. This domain gap is likely to limit direct transfer from exemplar-only training. Future experiments should measure checkout-like composition/synthesis, image pairing, calibration, or retrieval-based SKU recognition as separate ablations.

## Evaluation protocol

- Report detector precision, recall, mAP@0.50, and mAP@0.50:0.95.
- Inspect per-class mAP to reveal weak classes hidden by aggregate metrics.
- Independently measure exact per-image class-count accuracy and mean absolute count error.
- Select the confidence threshold on validation only; freeze it before optional test evaluation.
- Use the RPC authors' `rpctool` and protocol for official benchmark claims.

The notebook has not published numeric results. Run the full profile and preserve the generated `results.csv`, plots, checkpoint provenance, accelerator, package versions, and exact config before presenting a result.
