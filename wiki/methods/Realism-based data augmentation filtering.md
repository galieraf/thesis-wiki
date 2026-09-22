# Realism-based data augmentation filtering

Source: [[REAL - Realism Evaluation of Text-to-Image Generation Models for Effective Data Augmentation]], §4.4, Tables 2–4, and §5.2.

REAL ranks training-image candidates to test whether realism scores predict downstream utility. This evaluates effects on a trained task model, unlike [[Best-of-N image selection]], which evaluates a chosen output image.

## Classification and captioning protocol

The iNaturalist and Birds experiments each use 200 classes. Five real images per class form the unaugmented training set and five real images per class form the test set; exact split-disjointness is not detailed. From remaining **real and synthetic** candidates, rank by $S_{att}S_{sty}$ and add the top five, bottom five, or five random images per class. Thus the augmented training sets have twice as many images as the unaugmented set.

ViT classification trains for ten epochs with augmentation and twenty without, accounting for the different dataset sizes. BLIP captioning uses analogous sets and class-name photo captions, trained for ten epochs as stated in its subsection. The text does not explicitly repeat the doubled-epoch rule for unaugmented captioning.

| Outcome | None | Low-score | Random | High-score |
| --- | --- | --- | --- | --- |
| iNaturalist classification F1 | 0.6937 | 0.6442 | 0.7271 | 0.8070 |
| Birds classification F1 | 0.6649 | 0.6685 | 0.7112 | 0.7170 |
| iNaturalist caption BLEU | 0.7194 | 0.7008 | 0.7345 | 0.7612 |
| Birds caption BLEU | 0.6454 | 0.6624 | 0.6635 | 0.7143 |

The iNaturalist high-score F1 gain is 0.1133 absolute, or 11.33 percentage points, rather than an 11.3% relative gain. Low-score augmentation harms iNaturalist classification but slightly improves Birds classification. Adding style to attribute-only filtering improves iNaturalist F1 from 0.7700 to 0.8070.

## Relationship detection

For UnRel, relation/style scores select augmentation sets. RelTR, pretrained on Visual Genome, is fine-tuned for 150 epochs; YOLO11 generates otherwise missing boxes. High-score mR@20/mR@50 is 0.3529/0.3613 versus 0.2199/0.2787 for low-score and 0.3123/0.3137 for random selection. High minus low is 0.1330/0.0826, which does not reproduce the prose’s 7.42%/5.32% claim.

## Interpretation and thesis adaptation

The results support task-specific selection in the tested pools, not a causal claim about synthetic data alone. Mixed provenance, class-template captions, fixed-seed runs without uncertainty estimates, and automated relationship boxes limit inference.

For a thesis extension, keep candidate counts and real/synthetic proportions controlled, ensure disjoint evaluator/training/test data, and compare both downstream performance and collection diversity. Higher realism may help a target task without implying better [[Aesthetic quality]] or more diverse data.

## Related pages

- [[Schema-based realism evaluation]]
- [[Fine-grained visual correctness]]
- [[Photorealism]]
