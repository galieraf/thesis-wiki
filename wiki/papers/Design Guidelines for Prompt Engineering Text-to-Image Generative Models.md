# Design Guidelines for Prompt Engineering Text-to-Image Generative Models

**Authors:** Vivian Liu and Lydia B. Chilton  
**Year:** 2022  
**Source:** [[raw/papers/liu2022design.pdf]]; CHI ’22, 23 pages. DOI: [10.1145/3491102.3501825](https://doi.org/10.1145/3491102.3501825)  
**Last updated:** 2026-09-21

## Research question

Which prompt parameters and generation hyperparameters help users obtain desirable images from VQGAN+CLIP? Five experiments examine wording permutations, random seeds, optimization length, style coverage, and interactions between subject concreteness and style abstraction.

## Motivation

Free-form text gives users many possibilities but little guidance when generations fail. The authors seek empirical guidelines that reduce trial and error, using the prompt family `SUBJECT in the style of STYLE` as a tractable interface to visual generation (§§1–2).

## Method

The paper reports 5,493 generated images across five experiments. Evaluation combines judgments from two annotators per task with qualitative analysis of success and failure cases. Annotators had relevant art/media/design backgrounds; the paper reports compensation of $20/hour. These experiments use different evaluation tasks, so their scores should not be treated as one common image-quality measure.

| Experiment | Design | Evaluation |
| --- | --- | --- |
| 1: Wording (§3) | 12 subjects × 12 styles × 9 prompt permutations = 1,296 images; one subject–style grid excluded for inappropriate content | Randomized 3×3 grids; identify better/worse or otherwise noticeably different outliers, collapsed to outlier versus same |
| 2: Seeds (§4) | 12 subjects × 12 styles × 9 seeds = 1,296 images | Randomized 3×3 grids; outlier judgments |
| 3: Optimization (§5) | 6 subjects × 12 styles; 72 trajectories, each evaluated at 100-step intervals from 100 to 1,000 = 720 checkpoint images | Choose the preferred checkpoint from each row of 10 |
| 4: Styles (§6) | 12 subjects × 51 styles = 612 images | Rate style representation from 1 to 5, irrespective of subject fidelity; qualitative analysis and comparisons between style groups |
| 5: Subject–style interaction (§7) | 51 subjects × 31 styles = 1,581 images | Rate joint representation of subject and style from 1 to 5; analyze subject concreteness, style category, and their interaction |

The enumerated experiment totals sum to 5,505, whereas the abstract reports 5,493. The paper also alternates between 143 and 144 grids and describes “10” random seeds while listing nine. These are source-reporting inconsistencies; the total is retained as reported rather than silently reconciled.

## Datasets

- **Constructed prompt/image sets:** 51 subjects and 51 styles across the study, with subsets used in individual experiments; this is not evaluation on a standard held-out image benchmark.
- **Initial 12 subjects:** love, hate, happiness, sadness, man, woman, tree, river, dog, cat, ocean, forest. The reported mean concreteness ratings are 2.12 for the abstract subset and 4.80 for the concrete subset on a 1–5 scale.
- **Subject concreteness source:** Brysbaert, Warriner, and Kuperman’s ratings of approximately 40,000 English word lemmas (paper reference [7]); the authors use these ratings to distinguish abstract and concrete subjects.
- **Style selection sources:** the Metropolitan Museum of Art’s Heilbrunn Timeline, Aesthetics Wiki, WikiArt’s organization, and Wikipedia. Categories include media, art traditions/movements, and Internet aesthetics, partitioned by abstraction, culture, and time period.
- **Pretraining context:** the VQGAN checkpoint is ImageNet-pretrained; the paper describes CLIP’s 400-million image–text-pair pretraining in related work. These are training sources, not the study’s evaluation dataset.

Table 1’s caption gives category counts that do not sum to 51, and the appendix includes apparent labeling/list errors. Consult the PDF before reconstructing the exact prompt inventory; the prose should not be treated as an error-free machine-readable dataset.

## Models

**Evaluated:** VQGAN+CLIP, with an ImageNet-pretrained VQGAN checkpoint/configuration and codebook size 16,384. The stated baseline is 256×256 pixels and 300 optimization steps, run on an NVIDIA GeForce RTX 3080 (§3.1). Experiment 3 varies optimization length up to 1,000 steps. The paper does not clearly identify the exact CLIP backbone in this configuration.

DALL-E, BigSleep, DeepDaze, and CLIP-guided diffusion are discussed as background; they are not comparative experimental baselines. These results do not establish effects for later diffusion models.

## Metrics

- **Perceived outlier status:** better/worse or visibly different generations versus the rest of a grid (Experiments 1–2). This is neither a standardized aesthetic score nor a quantitative diversity metric.
- **Checkpoint preference:** which of ten optimization checkpoints an annotator prefers (Experiment 3).
- **Style fidelity:** five-point ordinal rating from extremely poor to excellent representation, based on stylistic motifs (Experiment 4).
- **Joint subject–style representation:** five-point ordinal rating from extremely poor to excellent representation (Experiment 5).
- **Agreement:** Cohen’s kappa is 0.0013 in Experiment 1 (despite 71.3% raw agreement), 0.13 in Experiment 2, and 0.33 in Experiment 3. These limit confidence in subjective judgments.
- **Analysis:** chi-square tests, Fisher’s exact test, Mann–Whitney and Kruskal–Wallis tests, Pearson correlation, and two-way ANOVA, depending on the experiment.

No FID, CLIPScore, LPIPS, or other automated image-quality, alignment, or diversity score is reported. See [[Human evaluation of generated images]].

## Main findings

1. **Wording:** the authors report no significant difference among nine tested permutations (chi-square statistic 0.354, $p=0.55$, §3.3). They recommend concentrating on subject/style keywords rather than connecting words. This null result is not proof that phrasing never matters.
2. **Seeds:** outlier judgments varied significantly with initialization (Fisher’s exact test, $p<0.01$, §4.3). The authors recommend trying 3–9 seeds. They tested nine seeds per combination, not a systematic comparison establishing 3–9 as an optimal sample size. See [[Random seeds and generation variability]].
3. **Optimization:** preferred checkpoints were not uniformly distributed ($p=0.01$); 200, 100, and 500 steps were most frequently preferred (§5.3). More optimization did not guarantee a more desirable image. The authors suggest 100–500 steps for rapid exploration and 300 as a practical default; at 100 steps the subject may not yet be recognizable. See [[Optimization length and perceptual quality]].
4. **Styles:** the model captured palettes, textures, lines, lighting, patterns, and motifs across many styles. Figurative styles scored 3.16 versus 2.63 for abstract styles ($p<0.01$). Western/non-Western means were 2.92/2.95 with no detected difference ($p=0.377$). Premodern, modern, and digital means were 3.11, 2.83, and 2.41 ($p<0.001$). These are style-fidelity judgments, not evidence that an entire culture or period has inherently higher image quality (§6).
5. **Subjects and styles interact:** subject concreteness correlated with mean generation rating ($r=0.62$). Reported means, ordered as **style–subject**, were abstract–abstract 3.05, abstract–concrete 3.17, figurative–abstract 3.49, and figurative–concrete 3.54. The authors report significant subject and style main effects and their interaction, all $p<0.01$ (§7.3). Concrete subjects generally performed better, while abstract subjects could succeed through recognizable symbols.
6. **Failure modes:** ambiguous style names, superficial or incomplete stylistic imitation, photorealistic/text intrusions, default motifs, subject omission, and disturbing or mature content (§§6.5, 7.4). A style may be visually recognizable while the subject is absent. The discussion also cautions about stereotypes and misrepresenting artistic traditions.

## Limitations

**Acknowledged by the authors (§8.2):** the study concentrates on one framework and largely one prompt template. Image-plus-text conditioning, intermediate steering, alternative prompt forms, and realism modifiers such as `4k` and `2048px` remain future work. Reproducing palettes or technique does not establish understanding of a style’s cultural or conceptual meaning.

**Critical reading for thesis use:**

- Two annotators per task and low reported kappa values weaken the reliability and generalizability of preference/outlier findings.
- Experiment 1’s outlier task mixes perceived quality and visible difference; its null result should not be generalized into equivalence of all phrasings.
- Broad art categories and selected prompts constrain cultural and style comparisons. A nonsignificant Western/non-Western comparison does not establish absence of bias.
- Ratings combine constructs differently across experiments. Joint subject–style scores cannot isolate aesthetics, subject alignment, and style fidelity.
- Seed variability is not a direct measure of output diversity or coverage; optimization steps are specific to this generation procedure.
- Reported counts and appendix labels contain inconsistencies, complicating exact replication. The inference from the described contingency-table analysis to a general wording recommendation also warrants caution.

## Relevance to my thesis

This is an early empirical basis for [[Prompt engineering]] and [[Style modifiers]] in text-to-image generation. It supports varying content and style systematically and controlling generation settings when studying modifier effects.

**Thesis implications (interpretation, not experiments established here):**

- Compare modifiers across multiple subjects and seeds, accounting for [[Subject-style interaction]] rather than attributing every score difference to the modifier alone.
- Evaluate subject alignment, style fidelity, visual quality, and diversity separately. The paper motivates these distinctions but does not supply a validated metric for every dimension.
- Test whether stronger style cues suppress content or introduce stereotyped motifs.
- Treat the reported seed and iteration ranges as historical hypotheses to reassess for the selected model, not universal defaults.
- The untested realism/quality modifiers offer a direct research gap; the paper does not demonstrate that `4k` improves image quality.

## Subsequent related work

[[Best Prompts for Text-to-Image Models and How to Find Them]] cites this paper and searches modifier combinations in Stable Diffusion v1.4 with human aesthetic preferences and a genetic algorithm. It extends the keyword-selection question to another model and evaluation task; it does not replicate the VQGAN+CLIP wording or style-fidelity experiments.

## Related pages

- [[Prompt engineering]]
- [[Style modifiers]]
- [[Subject-style interaction]]
- [[Random seeds and generation variability]]
- [[Optimization length and perceptual quality]]
- [[Human evaluation of generated images]]
- [[Factorial subject-style evaluation]]
