# BEAR

**Asymmetric Bitemporal Evidence Learning for Remote Sensing Building Damage Assessment**

BEAR is a bitemporal framework for building damage assessment from pre-event and post-event remote sensing imagery. It jointly predicts building localization and damage severity while accounting for the different roles of the two observations, ambiguous local temporal evidence, and inconsistent pixel-wise predictions within a building.

The paper evaluates BEAR on two complementary benchmarks:

- **xBD:** optical pre-event and post-event imagery.
- **BRIGHT:** pre-event optical imagery and post-event SAR imagery.

The two datasets are trained separately. BRIGHT uses generic pretrained weights without xBD-supervised initialization.

## Method

BEAR combines three components:

1. **Asymmetric Bitemporal Adaptation (A-BA).** A shared low-rank update is used for both temporal inputs, while an additional low-rank residual is activated only for the post-event input. This preserves a common adaptation basis while allocating extra capacity to post-event appearance and damage cues.
2. **Global--Local Evidence Fusion (GL-EF).** Paired Transformer representations jointly determine the locations and weights used to read local CNN features from both dates. The post-event representation combines the sampled post-event evidence with its signed difference from the pre-event reference, and updated contextual features are returned to the CNN streams.
3. **Region-guided Evidence Refinement (R-ER).** Predicted building support is used to aggregate class-specific regional evidence. A confidence gate combines regional confidence and local uncertainty to refine dense damage features while retaining a separate prediction at each pixel.

The localization decoder uses pre-event features, while the damage decoder receives features from both dates.

## Reported Results

The following values are reported for the BEAR checkpoints used in the manuscript. Percentages are shown in the benchmark metrics' native reporting format.

| Dataset | Evaluation split | Localization F1 | Damage / classification F1 | Overall F1 | OA | mIoU |
| --- | --- | ---: | ---: | ---: | ---: | ---: |
| xBD | 933-pair local holdout | 86.79 | 75.67 | 79.01 | -- | -- |
| BRIGHT | Standard 878-pair test split | 90.99 | 73.36 | -- | 96.38 | 68.38 |

For xBD, overall F1 follows the official combination of localization and damage F1. For BRIGHT, classification F1 is computed over the building damage classes and mIoU is the four-class mean IoU over background, intact, damaged, and destroyed pixels.

Published reference values in the paper are reproduced under their reported protocols and are not presented as a common-protocol ranking. The qualitative figures are intended to illustrate local prediction behavior alongside the aggregate metrics.

## Repository Status

This repository currently contains the project README. The source code, training configuration, inference tools, and model checkpoints will be released at publication.

Until that release, please use the paper for the complete architecture, training protocol, evaluation definitions, and experimental results.

## Citation

The citation entry will be added with the final bibliographic metadata when the paper is published.

## License

A license for the released code and checkpoints will be added together with the publication release.
