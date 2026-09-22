# REAL: Realism Evaluation of Text-to-Image Generation Models for Effective Data Augmentation

**Authors:** Ran Li, Xiaomeng Jin, and Heng Ji.
**Year:** 2025; supplied preprint arXiv:2502.10663v1, 15 February 2025.
**Source:** [[raw/papers/li2025real.pdf]]. Ingestion is based on the supplied paper and appendix; no external implementation or dataset was inspected.
**Last updated:** 2026-09-22.

## Research question

Can structured evaluation of fine-grained attributes, unusual object relationships, and photographic style better reflect human realism judgments and identify useful images for data augmentation?

## Motivation

Prompt similarity can overlook incorrect species traits, implausible objects or relations, and illustrative appearance when photographs are required. Such errors can undermine downstream training even when a generated image roughly matches its prompt. REAL evaluates task-relevant realism with separate modules (§§1–3).

## Method

- **Attributes:** build class-specific part/description schemas from knowledge sources or existing labels. A VQA existence/realism check gates evaluation. For each part, ask whether it is visible and, if so, whether it matches the description. Score correct visible attributes divided by visible attributes, returning zero when none are visible.
- **Relations:** ask whether each entity exists and looks realistic/natural. Return zero if an entity is missing; otherwise score entity checks and requested relations. The printed formula is an unnormalized sum, although benchmark scores are reported between zero and one. The normalization is not specified in the supplied text.
- **Style:** fine-tune CLIP to distinguish photographs from illustrations using 9,400 real/generated images. The photo-class probability is the style score. Training uses a contrastive objective, learning rate $5\times10^{-5}$, batch size 8, and five epochs.
- **Validation:** compare scores with human answers and baseline metrics, then use REAL to rank augmentation candidates and test downstream training outcomes. Attribute/style filtering uses the heuristic product $S_{att}S_{sty}$; the relation experiment uses relation and style scores but does not give an equally explicit combination formula.

See [[Schema-based realism evaluation]] and [[Realism-based data augmentation filtering]].

## Datasets

| Dataset/collection | Role |
| --- | --- |
| iNaturalist | Random sample of 200 fine-grained classes from the described 10,000-class collection; attribute/style evaluation and downstream classification/captioning |
| Birds (CUB-200-2011) | All 200 bird classes; class schemas derived from common image-level annotations among 312 binary attributes |
| UnRel | 76 unique object–relation–object triplets; unusual-relation/style evaluation and relationship detection |
| Style classifier training | 9,400 images: real examples sampled from the three datasets and illustrations generated evenly across the four generators |
| Human validation | 100 images per dataset, 300 total; three workers answer each binary question |
| Style ablation | 100 real and illustration-style iNaturalist images |

For iNaturalist, Wikipedia descriptions are collected and GPT-4 extracts major parts and descriptions. Birds schemas aggregate class annotations. The paper does not fully specify the number of generations per class/triplet, the real/illustration balance of the style-training set, or all splits needed to rule out overlap between evaluator training and evaluation.

## Models

- **Generators:** Stable Diffusion 1.1, Stable Diffusion 3.5 Turbo, DALL-E 3, and Kandinsky 3, as named in the supplied version. Table 5 abbreviates SD3.5 without “Turbo.”
- **REAL evaluators:** GPT-4o VQA by default; GPT-4 for knowledge-schema extraction; a fine-tuned CLIP style classifier. The exact CLIP checkpoint for the style classifier is not clearly specified.
- **VQA ablations:** BLIP2-Flan-T5-XL, PaliGemma-3B, mPLUG-Owl3-7B, Gemini-1.5-Flash-002, and GPT-4o, with temperature zero.
- **Baselines:** BLIP-Image-Captioning-Base followed by SPICE; CLIP-ViT-Base cosine scoring; and direct GPT-4o scoring supplied with the same knowledge but without the structured question procedure.
- **Downstream models:** ViT-Base-Patch16-224 classification, BLIP-Image-Captioning-Base captioning, and Visual Genome-pretrained RelTR for relationships. YOLO11 supplies missing bounding boxes for UnRel.

## Metrics

- Attribute score $S_{att}=R/C$ for $C>0$, where $C$ counts visible parts and $R$ counts visible parts matching the schema; otherwise zero. “Confidence” is a count, not a calibrated uncertainty estimate.
- Relationship score combines entity visibility, entity realism, and relations; normalization remains under-specified.
- Style score: classifier probability of photo rather than illustration.
- Human correspondence: Spearman’s $\rho$ and Kendall’s $\tau$ against per-image proportions of positive answers after per-question majority voting.
- Classification: accuracy and F1. Captioning: ROUGE-1 and BLEU against short class-template captions. Relationship detection: mean recall at 20 and 50.
- Generator benchmark: separate attribute, relation, style scores and their reported arithmetic mean. This mean is distinct from the product used for attribute/style filtering.

## Main findings

**Human correspondence (Table 1).**

| Dataset | REAL Spearman / Kendall | CLIP Spearman / Kendall | Direct GPT Spearman / Kendall |
| --- | --- | --- | --- |
| iNaturalist | 0.5223 / 0.4281 | 0.2176 / 0.1590 | 0.2716 / 0.2175 |
| Birds | 0.6162 / 0.4880 | 0.1698 / 0.1167 | 0.1106 / 0.0816 |
| UnRel | 0.5672 / 0.5034 | 0.1670 / 0.1255 | 0.2092 / 0.1817 |

SPICE also trails REAL, with Spearman correlations 0.0846, 0.2011, and 0.2239. These results support the evaluated schema under this human rubric, not equivalence to every notion of realism.

**Classification (Table 2).** iNaturalist F1 is 0.6937 without augmentation, 0.6442 with low-score candidates, 0.7271 with random candidates, and 0.8070 with high-score candidates. The high-score gain over none is **0.1133 absolute F1 (11.33 percentage points)**; the low-score loss is 0.0495. These are not 11.3% and 4.95% relative changes. Birds F1 is 0.6649/0.6685/0.7112/0.7170 in the same order: low-score augmentation does not harm every dataset.

**Captioning (Table 3).** High-score augmentation gives BLEU 0.7612 on iNaturalist versus 0.7194 without and 0.7345 with random augmentation; on Birds the corresponding values are 0.7143, 0.6454, and 0.6635. The task uses class-name template captions, not unrestricted detailed descriptions.

**Relationships (Table 4).** High-score augmentation gives mR@20/mR@50 of 0.3529/0.3613 versus 0.1036/0.1821 without augmentation, 0.2199/0.2787 for low-score, and 0.3123/0.3137 for random. High minus low is **0.1330/0.0826**, which does not reproduce the prose’s 7.42%/5.32% improvement claim. Preserve the table and the unresolved discrepancy.

**Generator benchmark (Table 5).**

| Generator | Attribute | Relation | Photo style | Mean |
| --- | --- | --- | --- | --- |
| DALL-E 3 | 0.5475 | 0.7827 | 0.2430 | 0.5244 |
| SD1.1 | 0.5717 | 0.3739 | 0.6356 | 0.5271 |
| SD3.5 | 0.5791 | 0.7315 | 0.5380 | 0.6162 |
| Kandinsky 3 | 0.4925 | 0.7301 | 0.6745 | 0.6324 |

Different models lead different dimensions. Kandinsky has the highest mean; DALL-E 3 leads relations but has the lowest photographic-style score. These are REAL-specific results for the tested datasets, not overall preference rankings.

**Ablations (§5).** On iNaturalist, VQA Spearman correlation ranges from BLIP2’s 0.0255 to GPT-4o’s 0.5223; mPLUG achieves 0.4733 and Gemini 0.4950. Adding style to attribute-based filtering raises classification F1 from 0.7700 to 0.8070. Style-classifier fine-tuning raises Spearman correlation from 0.7775 to 0.8267 and Kendall from 0.6349 to 0.6754 on the separate 100-image test (Table 8, incorrectly referred to as Table 7 in the prose).

## Limitations

The authors report approximately $0.03 and ten seconds per image with GPT-4o under their setup, and note dependence on LLM schema extraction and VQA capability. These are historical observations, not current pricing or latency guarantees. They identify additional dimensions such as logic and commonsense as future work (§7).

Further interpretation and reproducibility limits:

- Class attributes and relation correctness overlap with factuality/alignment, while the style classifier measures photographic appearance. REAL’s realism construct is broader than [[Photorealism]] and is not cleanly independent of [[Prompt alignment]].
- Attribute scoring is conditional on visibility. Hiding difficult parts can leave a high normalized score despite sparse coverage; report $C$ and total schema size alongside the ratio. The initial existence prompt in the text is generic, while figures show class-specific checks.
- Schema correctness, VQA errors, class variation, and automated bounding boxes can affect outcomes. Temperature zero and a fixed seed do not establish uncertainty or eliminate evaluator bias.
- Three-rater majority votes are reported, but no inter-rater agreement coefficient or repeated-run confidence intervals are supplied. Human questions follow manually summarized traits/relations, so correspondence validates that rubric rather than all aspects of visual realism.
- Candidate pools explicitly contain **synthetic and non-synthetic images**. The downstream improvements cannot be attributed purely to synthetic augmentation or prompt modifiers. Exact real/synthetic proportions and split-disjointness details are incomplete.
- The style classifier is trained on real photographs versus generated illustrations. Source-of-image cues may be confounded with photographic style; transfer to unseen generators/styles is not established.
- Relationship-score normalization and benchmark sampling are under-specified. Table 4 conflicts with the relationship-gain prose, and percentage wording often describes absolute score differences.
- The source claims IS and FID both require ground-truth images; only FID requires a reference distribution. Do not propagate that statement as a definition of IS.
- No dedicated aesthetics, general visual-diversity, or causal modifier experiment is reported. The class-template captioning setup is narrow.

## Relevance to my thesis

REAL motivates evaluating fine-grained correctness and photographic appearance separately when testing realism-oriented [[Prompt modifiers]]. A modifier could make an image look photographic while leaving the species or relation wrong. Its visible-part normalization also makes framing and occlusion important confounds.

A proposed thesis adaptation is to report attribute correctness, visibility coverage, relation success, and photographic style separately, with held-out human validation and matched prompts/seeds. If downstream usefulness matters, compare equally sized, provenance-controlled augmentation pools. Add independent aesthetics and diversity measures; REAL does not supply these.

## Related pages

- [[Fine-grained visual correctness]]
- [[Schema-based realism evaluation]]
- [[Realism-based data augmentation filtering]]
- [[Photorealism]]
- [[Human evaluation of generated images]]
- [[VQA-based concept coverage]]
- [[Anatomical defect evaluation]]
- [[CLIP-based alignment evaluation]]
- [[Holistic Evaluation of Text-to-Image Models]]
