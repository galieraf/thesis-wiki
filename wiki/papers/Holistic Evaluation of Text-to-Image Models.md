# Holistic Evaluation of Text-to-Image Models

**Authors:** Tony Lee, Michihiro Yasunaga, Chenlin Meng (equal contribution), Yifan Mai, Joon Sung Park, Agrim Gupta, Yunzhi Zhang, Deepak Narayanan, Hannah Benita Teufel, Marco Bellagente, Minguk Kang, Taesung Park, Jure Leskovec, Jun-Yan Zhu, Li Fei-Fei, Jiajun Wu, Stefano Ermon, and Percy Liang.
**Year:** 2023; NeurIPS Datasets and Benchmarks. Supplied version: arXiv:2311.04287v1, 7 November 2023.
**Source:** [[raw/papers/lee2023heim.pdf]]. Source-listed [HEIM v1.1.0 results](https://crfm.stanford.edu/heim/v1.1.0) and [HELM code](https://github.com/stanford-crfm/helm); external resources were not independently inspected.
**Last updated:** 2026-09-22.

## Research question

How can text-to-image models be compared consistently across technical capabilities, human-perceived image properties, societal risks, and practical performance instead of relying mainly on alignment and image-quality scores?

## Motivation

Common benchmarks cover a narrow range of prompts and outcomes, automated metrics may disagree with people, and inconsistent evaluation procedures hinder comparison. HEIM combines broad scenario coverage with human and automated measurements (§§1–2).

## Method

HEIM separates an **aspect** (what is evaluated), a **scenario** (prompt dataset/use case), an **adaptation** (how the model is run), and a **metric** (how outputs are judged). The study evaluates 26 systems across 12 aspects and 62 scenarios/sub-scenarios, reporting 25 metrics. It primarily uses zero-shot prompting with each system’s default inference configuration, while also evaluating Promptist rewriting and Lexica retrieval. See [[Holistic text-to-image evaluation]].

The twelve aspects are alignment, image quality operationalized as photorealism, aesthetics, originality, reasoning, knowledge, demographic bias, toxicity, fairness as performance disparity, robustness, multilinguality, and efficiency.

Human evaluation uses Amazon Mechanical Turk Masters aged over 18 who accept potentially offensive content, with five different annotators per sample and at least 100 image samples per evaluated aspect. Questions have explicit verbal anchors. Photorealism mixes 100 real and 100 generated images. The paper reports $0.02 per multiple-choice response, an intended $16 hourly rate, and total annotation spending of $13,433.55 (Appendix E).

## Datasets

| Scenario family | Evaluation role |
| --- | --- |
| MS-COCO 2014 validation and CUB-200-2011 | General caption alignment, photographic quality, bird-specific alignment |
| MS-COCO with six appended styles | Oil painting, watercolor, pencil sketch, animation, vector graphics, pixel art; aesthetics and alignment |
| Modified MS-COCO | Gender substitution, word-level dialect substitution, typo/format perturbations, and Chinese/Hindi/Spanish translation |
| DrawBench and PartiPrompts | General alignment, compositional tasks, and world knowledge |
| Common Syntactic Processes, Relational Understanding, Winoground | Linguistic and relational reasoning |
| PaintSkills-style Detection | Object recognition, counts, and spatial relations |
| Historical Figures | 99 entity prompts for knowledge |
| Dailydall.e, Landing Pages, Logos, Magazine Covers | Art/design prompts for aesthetics and perceived originality: 93, 36, 100, and 50 prompts respectively |
| Demographic Stereotypes and Mental Disorders | Representation bias; 15 descriptor and 13 occupation prompts, plus 9 disorder prompts |
| Inappropriate Image Prompts (I2P) | Seven categories of potentially inappropriate output |

The datasheet reports approximately 500,000 prompts across the 62 scenarios, collected December 2022–June 2023. This is scenario inventory, not a statement that every prompt received human annotation. No recommended train/validation/test splits are supplied. FID uses 30,000 randomly selected MS-COCO prompts with one generated image each, resized to 512×512 and compared with associated reference images (Appendix C.2).

## Models

The July 2023 model snapshot comprises 26 systems:

- SD v1.4, v1.5, v2 base, v2.1 base; Dreamlike Diffusion 1.0 and Photoreal 2.0; Openjourney and Openjourney v4; Redshift; Vintedois.
- Safe Stable Diffusion at weak, medium, strong, and max settings; Promptist + SD1.4; Lexica Search over SD1.5 images.
- DALL-E 2, DALL-E mini, DALL-E mega, minDALL-E, CogView2, MultiFusion, DeepFloyd-IF M/L/XL, and GigaGAN.

Openjourney v4 was previously named v2, explaining differing labels between Tables 4 and 5 (Appendix D). The evaluated system set includes retrieval and prompt rewriting, not just generator backbones. Default resolutions and extra processing differ; Dreamlike Photoreal generates 768×768 by default versus SD’s 512×512. This is a historical comparison, not a current leaderboard.

## Metrics

| Aspect | Operational measurements |
| --- | --- |
| Alignment | Human 1–5 alignment, CLIPScore and multilingual CLIPScore |
| Quality | Human 1–5 photorealism, FID, Inception Score |
| Aesthetics | Human 1–5 appeal, three-option subject clarity, LAION aesthetic predictor, distance of fractal coefficient from 1.4 |
| Originality | Human 1–5 perceived originality conditioned on the prompt, LAION watermark detection |
| Reasoning and knowledge | Human alignment, CLIPScore; ViTDet object/count/spatial-relation accuracy for diagnostic reasoning |
| Bias | Eight images per prompt; binary gender proportion distance from 0.5 and ten-category Monk Skin Tone distribution L1 distance from uniform |
| Toxicity | LAION NSFW, NudeNet, SD blackout frequency, DALL-E 2 API rejection frequency |
| Fairness, robustness, multilinguality | Change in alignment after relevant input transformations |
| Efficiency | Raw runtime and denoised runtime intended to factor out service/performance variation |

A reported model **win rate** compares metric performance against another model drawn uniformly from the tested pool. It is a relative model-ranking summary, not necessarily a human pairwise preference frequency or an absolute success rate. Metric-level results and aggregation context matter.

## Main findings

- **No universal winner (§7).** DALL-E 2 leads general human-rated alignment; art-tuned systems excel on some aesthetic/originality judgments; less biased or less toxic systems may be weaker on alignment and photorealism. These are observed cross-system patterns, not controlled causal effects of training interventions.
- **Photorealism remains limited.** Real MS-COCO images average 4.48/5, while no tested model averages above 3. The claim concerns mean ratings, not that every generated image is unrealistic.
- **Prompt rewriting helps one outcome.** Promptist + SD1.4 improves human-rated aesthetics over SD1.4 with reportedly comparable alignment (§7, finding 14). Table 5 gives aesthetic win rates 0.883 versus 0.667 and photorealism/quality win rates 0.04 versus 0.88. The result therefore does not establish improvement in every image-quality dimension.
- **Art-style performance differs by criterion.** In the six-style scenario, the narrative identifies Openjourney as strongest for human aesthetic appeal, DALL-E 2 for alignment, and Dreamlike Photoreal for subject clarity. This is not a dedicated style-fidelity score or a causal estimate for individual modifiers.
- **Reasoning is weak.** The strongest model, DALL-E 2, reaches 47.2% overall detection accuracy on PaintSkills; errors include object counts and spatial relations.
- **Automatic and human scores only partly agree.** Reported correlations are 0.42 for CLIPScore/alignment, 0.59 for FID/photorealism, and 0.39 for LAION aesthetics/human aesthetics. The supplied text does not specify the correlation type, aggregation unit, or FID direction transformation sufficiently to reinterpret the positive 0.59 as raw per-image agreement. FID is distribution-level.
- **Input changes expose gaps.** Around half the models lose human alignment under gender/dialect changes and under typo perturbations. Typo losses are generally at most 0.2 on the five-point scale; Openjourney loses 0.25 under dialect substitution. These results cover the tested transformations, not unrestricted robustness.
- **Language support varies.** DALL-E 2’s English alignment of 4.438 falls by 0.536 in Chinese, 0.162 in Spanish, and 2.640 in Hindi. CogView2 is a notable case of better Chinese than English performance.
- **Runtime differs.** The paper reports approximately 2 seconds denoised runtime for vanilla SD and 0.14 seconds for GigaGAN. Extra rewriting/safety processing and higher resolutions add cost. These measurements are not energy consumption or hardware-independent speed guarantees.

## Limitations

The authors acknowledge incomplete aspect coverage, narrow demographic categories, latency as only a proxy for energy, and greater subjectivity in aesthetics and originality than in alignment or clarity. They caution against strong conclusions from public judgments alone where professional artists or legal experts may disagree (§10).

Additional interpretation limits for this wiki:

- The twelve aspects do not include a dedicated measure of within-prompt visual diversity. Demographic balance, subjective originality, and IS cannot automatically stand in for that outcome.
- Perceived originality and watermark detection neither test training-set novelty comprehensively nor determine copyright infringement. See [[Perceived originality in generated images]].
- The eight-image demographic sample is small; binary gender and image-based skin classification are restricted proxies. Uniform reference distributions are evaluative choices, not self-evident definitions of fairness.
- Word substitution is a limited approximation of a dialect; automatic translations and perturbations need validation of preserved meaning. Gender substitutions intentionally alter semantics, so the desired equality is in performance, not identical pictures.
- Defaults standardize access procedures but not resolution, compute, filtering, or adaptation. Retrieval and rewriting should be identified when comparing systems.
- The paper describes five raters and verbal anchors but does not give numerical inter-rater reliability in the supplied text. Do not turn its qualitative agreement claims into measured coefficients.
- The headline reports 25 metrics, while Table 3 appears to enumerate 24 named rows. Preserve the reported count and this unresolved presentation discrepancy. Table 5 is a selected summary, not all twelve aspects separately.
- Appendix B.2 in the supplied PDF contains interleaved editorial/timeline text and duplicated passages. Core scenario definitions are recoverable, but exact reproduction should consult versioned source artifacts; those were not fetched for this ingestion.

## Relevance to my thesis

Use HEIM’s aspect–scenario–adaptation–metric structure to design a focused modifier evaluation. Keep [[Aesthetic quality]], [[Photorealism]], [[Prompt alignment]], and diversity separate. Style additions and Promptist provide directly relevant test designs, but the benchmark does not isolate the effects of individual quality boosters or all modifier combinations.

A proposed thesis adaptation is to evaluate matched base prompts across modifier conditions with fixed generation settings, several seeds, separate human questions, and calibrated automated metrics. Add a dedicated diversity measure and inspect subgroup/perturbation effects where relevant. This extends HEIM rather than reproducing an experiment it reports.

## Related pages

- [[Holistic text-to-image evaluation]]
- [[Prompt perturbation evaluation]]
- [[Human evaluation of generated images]]
- [[Style modifiers]]
- [[Prompt engineering]]
- [[Demographic diversity and bias]]
- [[CLIP-based alignment evaluation]]
- [[Evaluating Text-to-Image Generative Models - An Empirical Study on Human Image Synthesis]]
- [[Pick-a-Pic - An Open Dataset of User Preferences for Text-to-Image Generation]]
