# Pick-a-Pic: An Open Dataset of User Preferences for Text-to-Image Generation

**Authors:** Yuval Kirstain, Adam Polyak, Uriel Singer, Shahbuland Matiana, Joe Penna, and Omer Levy.
**Year:** 2023; NeurIPS 2023.
**Source:** [[raw/papers/kirstain2023pickapic.pdf]]. Source-listed resources: [code](https://github.com/yuvalkirstain/PickScore), [Pick-a-Pic v1](https://huggingface.co/datasets/yuvalkirstain/pickapic_v1), [v2](https://huggingface.co/datasets/yuvalkirstain/pickapic_v2), and [PickScore v1](https://huggingface.co/yuvalkirstain/PickScore_v1). External resources were not independently inspected.
**Last updated:** 2026-09-22.

## Research question

Can an open dataset of real users’ pairwise image preferences support a learned scoring function that predicts those preferences, evaluates generators, and improves selected outputs?

## Motivation

Prompt authors know intentions that may be absent from the written prompt and unavailable to outside annotators. Existing photographic caption benchmarks and distribution-level metrics may not reflect creative image-generation use. The authors collect user-authored prompts and preferences, then train PickScore to predict prompt-conditioned satisfaction (§1).

## Method

1. A web app shows two images generated for a user’s prompt. The user chooses one or indicates a tie; the rejected image is replaced, and comparisons continue until the user changes the prompt. Users consent to public release and receive anonymized IDs.
2. Quality controls include authentication, activity monitoring, bans for misuse, NSFW phrase filtering, and interaction limits. Residual problematic content and careless judgments remain possible.
3. Split by prompt: sample 1,000 prompts from distinct users, assign 500 each to validation and test, and retain one comparison per prompt. Training excludes all comparisons sharing those prompts. This does not guarantee user-disjoint training and evaluation.
4. Fine-tune CLIP-H on pairwise preferences with soft targets for ties and inverse prompt-frequency loss weighting. See [[PickScore preference prediction]].
5. Evaluate individual preference prediction, aggregate generator rankings, and selection of one image from 100 candidates. See [[Best-of-N image selection]].

## Datasets

| Collection | Reported scope and purpose |
| --- | --- |
| Logged interactions at the reported snapshot | 968,965 rankings, 66,798 prompts, 6,394 users |
| Filtered experimental training set | 583,747 comparisons, 37,523 prompts, 4,375 users |
| Validation and test | 500 comparisons each, with one comparison per prompt and 1,000 distinct prompt authors across the two sets |
| Model-rating evaluation | Approximately 14,000 collected comparisons for test-set prompts, rather than only the 500 selected test examples |
| MS-COCO evaluation | 100 validation captions; nine generator configurations produce images ranked by experts |
| Candidate-selection evaluation | 100 Pick-a-Pic test prompts, 100 generated images per prompt |

Each preference example contains a prompt, two images, and a first-image/second-image/tie label. The paper also mentions a later release exceeding one million examples; this is distinct from the experimental training snapshot and is not a claim about the dataset’s current size.

## Models

- Dataset generators: Stable Diffusion 2.1, Dreamlike Photoreal 2.0 (fine-tuned SD1.5), and SDXL variants, with varying classifier-free guidance (CFG).
- PickScore: CLIP-H architecture fine-tuned for preference prediction. Training uses 4,000 steps, learning rate $3\times10^{-6}$, batch size 128, 500 warmup steps, and linear decay; the best validation checkpoint is selected at 100-step intervals using accuracy without tie prediction. Training takes under an hour on eight A100 GPUs; no hyperparameter search is reported.
- Preference baselines: zero-shot CLIP-H, a CLIP-L-based aesthetic predictor, random predictions, human experts, HPS, and ImageReward.
- MS-COCO comparison: SD1.5, SD2.1, and Dreamlike Photoreal 2.0, each at CFG 3, 6, and 9: nine configurations, not nine independent model families.
- User-ranking comparison: 45 configurations from four backbones with differing guidance scales.
- Candidate selection: Dreamlike Photoreal 2.0, CFG 7.5; five noise initializations × twenty prompt templates, including an unchanged-prompt template.

## Metrics

- **Tie-aware preference accuracy:** 1 for exact label agreement, 0.5 when exactly one of prediction/label is a tie, and 0 otherwise. Each automatic model’s tie threshold is chosen on validation data. This is not ordinary binary accuracy, and chance is not automatically 50%.
- **Model evaluation on MS-COCO:** Spearman correlation between model win ratios induced by expert rankings and automatic judgments. FID assigns a pair’s winner using generator-level FID, since it cannot score individual prompt–image pairs.
- **Model evaluation on Pick-a-Pic:** Spearman correlation of user-derived and metric-derived Elo ratings. Fifty random comparison orders quantify Elo order sensitivity; reported spreads are standard deviations across those orders.
- **Image selection:** human preference win rate for PickScore’s chosen image versus each alternative. Additional aesthetic/CLIP comparisons use automatic proxies rather than separate human judgments of those constructs.

## Main findings

**Preference prediction (Table 1b).**

| Predictor | Tie-aware test accuracy (%) |
| --- | --- |
| Random | 56.8 |
| Aesthetic predictor | 56.8 |
| CLIP-H | 60.8 |
| ImageReward | 61.1 |
| HPS | 66.7 |
| Human experts | 68.0 |
| PickScore | 70.5 |

The text reports PickScore as $70.5\pm0.142$ over three training seeds; its footnote calls this mean and variance, so the spread should not be relabeled as a standard deviation or confidence interval. The appendix’s alternative objective with in-batch negatives achieves 65.2, below the main objective.

“Superhuman” here means better prediction of original user labels than external annotators who lack the author’s private intent. It does not mean superior taste or better knowledge of a user’s wishes than the user. Experts throughout the paper are friends and colleagues of the authors.

**Model rankings (§5).** On the nine MS-COCO configurations, PickScore win ratios correlate with expert win ratios at 0.917, while FID-derived win ratios correlate at −0.900. The authors hypothesize that higher CFG increases vividness and preference while departing from the photographic reference distribution. This finding is conditional on the tested setup, not a universal claim that FID is negatively correlated with human judgment.

On approximately 14,000 user comparisons across 45 configurations, Elo correlations are PickScore $0.790\pm0.054$, HPS $0.670\pm0.071$, ImageReward $0.492\pm0.086$, and CLIP-H $0.313\pm0.075$. These are aggregate configuration-ranking results, distinct from per-example prediction accuracy.

**Selection from 100 candidates (§6, Table 2).**

| Alternative to PickScore selection | Human win rate for PickScore (%) |
| --- | --- |
| Random seed, unchanged prompt | 71.4 |
| Random seed and random template | 82.0 |
| Aesthetic-score selection | 85.1 |
| CLIP-H selection | 71.3 |

PickScore selections have higher aesthetic-predictor scores than CLIP-H selections for 68.5% of prompts, and higher CLIP-H alignment scores than aesthetic selections for 90.5%. These are proxy-score comparisons; they do not independently establish human-rated improvements on both dimensions.

## Limitations

- Users recruited through social media are self-selected. Their preference distribution need not represent all users, cultures, tasks, or later generators. The paper acknowledges preference biases, residual NSFW content, and careless labels.
- Prompt-disjoint splits prevent reuse of identical held-out prompts, not necessarily author overlap or semantically similar prompts. Repeated comparisons retain winning images, so interactions are not independent random image pairs.
- The 500-example preference test and convenience-sampled experts limit generalization. Expert sample sizes, agreement, and uncertainty for several human comparisons are insufficiently specified.
- PickScore can prefer aesthetically pleasing images at the expense of prompt faithfulness (§4). It measures learned overall preference, not isolated aesthetics, alignment, realism, fairness, or diversity.
- Comparisons with HPS/ImageReward confound training distribution, dataset scale, architecture, and implementation. The authors explicitly leave their individual contributions unresolved.
- The FID study uses only nine model–guidance configurations and 100 captions for human ranking; the text does not fully specify the underlying FID computation sample count. Elo spread measures comparison-order variation, not population uncertainty.
- Candidate selection combines seeds, templates, and scoring. Its improvement does not isolate modifier effects or show the unselected generator distribution improved. No dedicated diversity outcome or complete list of twenty templates is provided in the supplied appendix.
- Training-seed uncertainty is ambiguously presented as a plus/minus quantity described as variance; preserve that wording rather than silently reinterpret it.

## Relevance to my thesis

Pick-a-Pic supplies a source of natural creative prompts and a preference-learning benchmark. [[PickScore preference prediction]] can complement [[Aesthetic quality]] and [[Prompt alignment]] measures, but should not replace them. This distinction complements the separate outcomes in [[Evaluating Text-to-Image Generative Models - An Empirical Study on Human Image Synthesis]].

The ranking experiment directly connects [[Prompt modifiers]] with [[Random seeds and generation variability]]. For the thesis, a proposed extension is to fix base prompts, seeds, and candidate budgets across modifier conditions, distinguish average generation quality from best-of-N selection quality, and use held-out human judgments to check metric-driven selection. Measure diversity separately and preserve original user intent as the evaluation reference.

## Related pages

- [[Human preference in image generation]]
- [[PickScore preference prediction]]
- [[Best-of-N image selection]]
- [[Human evaluation of generated images]]
- [[Pairwise aesthetic preference ranking]]
- [[CLIP-based alignment evaluation]]
- [[Best Prompts for Text-to-Image Models and How to Find Them]]
