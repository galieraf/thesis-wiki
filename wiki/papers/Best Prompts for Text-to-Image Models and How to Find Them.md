# Best Prompts for Text-to-Image Models and How to Find Them

**Authors:** Nikita Pavlichenko and Dmitry Ustalov  
**Year:** 2023  
**Source:** [[raw/papers/pavlichenko2023bestprompts.pdf]]; SIGIR ’23, pp. 2067–2071. DOI: [10.1145/3539618.3592000](https://doi.org/10.1145/3539618.3592000). Code/data repository reported by the paper: [toloka/BestPrompts](https://github.com/toloka/BestPrompts) (not independently inspected for this ingestion).  
**Last updated:** 2026-09-21

## Research question

Can human preference judgments guide a search for prompt keyword combinations that make Stable Diffusion images more aesthetically appealing than either unmodified descriptions or commonly used keywords?

## Motivation

Community prompt suffixes often appear arbitrary, and popularity need not predict image quality. A prompt judged from one description or one generated image may not generalize. The authors propose evaluation across descriptions and multiple generated images, using human judgments because aesthetics are difficult to assess computationally (§§1–2).

## Method

The method combines [[Pairwise aesthetic preference ranking]] with [[Genetic optimization of prompt keywords]] (§§2–4).

1. Build a pool of 100 popular keywords and represent each candidate subset as a 100-bit inclusion mask. Initialize with an empty keyword set and the 15 most popular keywords; limit candidates to at most 15 keywords.
2. Append each selected keyword set to the description, comma-separated and in alphabetical order. Generate four images per description–keyword-set combination.
3. Ask Toloka workers to choose the more aesthetically pleasing of two sets of four images for the same description. Workers see the description but not the keyword sets. The generic prose sometimes calls these image pairs; Figure 3 makes clear that the implemented choice is between two four-image sets.
4. Aggregate pairwise choices with Bradley–Terry via Crowd-Kit separately for each description, then average each keyword set’s rank across descriptions. Higher rank is better.
5. Select the two masks with the highest average ranks, exchange a random segment, and mutate bits with 1% probability. Evaluate new candidates using additional crowd comparisons and repeat under the annotation budget.

For $n$ candidates, the target number of sampled comparisons per description is $3n\log_2 n$. New candidates receive incremental comparisons intended to maintain this budget form. The paper reports 56 optimization iterations and labels Figure 4 as containing 56 keyword sets; the precise relationship between iterations, initial candidates, and evaluated sets is not fully clarified in the short report.

**Crowd quality control:** comparisons against DALL-E Mini images serve as synthetic golden tasks. The authors assume Stable Diffusion images are preferable and suspend workers below 80% accuracy on these tasks. This is a quality-control assumption about subjective aesthetics, not independently established ground truth.

## Datasets

- **Keyword pool:** the 100 most popular keywords parsed from the Stable Diffusion Discord. Frequency counts, sampling dates, and the complete pool are not listed in the paper.
- **Descriptions:** 72 prompts sourced from Reddit and Lexica, manually stripped of modifier keywords. There are 12 descriptions in each of six categories: portraits, landscapes, buildings, interiors, animals, and other.
- **Optimization split:** 60 descriptions, ten per category.
- **Validation split:** 12 additional descriptions; given the reported allocation, two per category.
- **Generated images and judgments:** four images per description–candidate combination; the authors report releasing images, comparisons, and code. The paper does not provide a clear total annotation count or crowd-worker count.

These are curated descriptions and generated preference data, not an evaluation on a standard reference-image benchmark. No separate final test split is reported.

## Models

- **Image generator:** Stable Diffusion v1.4, 50 diffusion steps, DDIM scheduler, classifier-free guidance scale 7.5 (§§1, 4.1). The paper does not specify image resolution or the seed-control policy.
- **Quality-control generator:** DALL-E Mini, used for synthetic golden comparisons rather than as the principal evaluated prompt-optimization baseline.
- **Preference aggregation:** Bradley–Terry implemented in Crowd-Kit.
- **Post-hoc importance analysis:** a random forest regressor fitted to keyword-set representations and their evaluation metrics (§4.3).

## Metrics

The optimization objective is **mean rank across descriptions**, obtained from per-description Bradley–Terry preference rankings. It is a relative measure within the evaluated candidate pool: larger values indicate better aesthetic preference. It is not an absolute quality score, a percentage, or a win rate.

The paper reports no separate prompt-alignment or diversity metric, no automated aesthetic score, and no confidence intervals or explicit significance-test results for Table 1. Its prose describes improvements as significant; the reported table alone does not establish a statistical significance level.

## Main findings

Table 1 reports the following average ranks (the stated maximum rank is 56):

| Candidate | Optimization: 60 descriptions | Validation: 12 descriptions |
| --- | --- | --- |
| No Keywords | 3.50 | 5.42 |
| Top-15 popular keywords | 14.25 | 12.50 |
| Best Train | 43.60 | 38.00 |
| Best Val | 39.32 | 46.00 |

The train-selected candidate retains a higher rank than Top-15 on validation (38.00 versus 12.50). Best Val is selected using validation performance; its 46.00 is not a separate untouched-test estimate. Rank differences should not be interpreted as proportional increases in image quality.

**Best Train keyword set, transcribed from §4.2:**

> cinematic, colorful background, concept art, dramatic lighting, high detail, highly detailed, hyper realistic, intricate, intricate sharp details, octane render, smooth, studio lighting, trending on artstation

This contains 13 keywords, within the 15-keyword cap. The paper prints this train-selected set, not a separate list for Best Val. It is a result for this search space, model, descriptions, and evaluator population—not a universally optimal prompt suffix.

The random forest analysis identifies **colorful background** as the most important keyword (§4.3). This is predictive feature importance over the observed keyword combinations, not an isolated causal estimate of what adding that keyword does.

The authors report that keyword sets outperform no-keyword prompts in their experiment and that popularity does not identify the best-performing combination. Figure 1 explicitly uses cherry-picked descriptions and should be treated as illustration, not representative quantitative evidence.

## Limitations

**Acknowledged by the authors (§4.3):** genetic search may become trapped in a local optimum, only 56 of the 100 keywords were tried according to the discussion, and rank-based metrics are insufficient for determining convergence. The search is limited by an annotation budget. The discussion’s count of tried keywords is distinct from Figure 4’s count of keyword sets; the exact search history should be checked in the released data before replication.

**Critical reading for the thesis:**

- The evidence covers one generator version and fixed settings; transfer to other models or subject distributions is not established.
- Twelve validation descriptions give limited evidence of generalization. Selecting Best Val additionally uses that split for model selection.
- Mean rank depends on the competing candidates and cannot be compared as an absolute score across changing pools.
- Four-image set preferences do not reveal within-set diversity, individual-image quality variance, or whether the requested content is preserved.
- The synthetic golden-task assumption may filter legitimate aesthetic preferences as well as careless annotations. Worker demographics, inter-rater agreement, and detailed annotation counts are not reported.
- Correlated keywords, adaptive search, and a fitted random forest do not identify individual causal modifier effects.
- Alphabetical order is fixed, so order sensitivity is not tested; the seed policy is not specified.

## Relevance to my thesis

This directly addresses [[Prompt modifiers]] and [[Aesthetic quality]]: it supplies a concrete human-guided procedure for searching modifier combinations, a no-modifier baseline, and a popularity baseline.

It extends [[Design Guidelines for Prompt Engineering Text-to-Image Generative Models]], which emphasizes subject/style keywords in VQGAN+CLIP, with combination search in Stable Diffusion v1.4. The two papers use different models and evaluation constructs and do not directly replicate each other.

**Thesis implications (proposed extensions):** evaluate aesthetics, prompt alignment, and diversity separately; reserve a final test split after selecting modifiers; compare across recorded seeds and multiple subject categories; and use controlled ablations to estimate individual modifier effects. A transferable suffix can be a baseline, but subject-dependent performance should also be investigated.

## Comparison with RePrompt

[[RePrompt]] provides another automatic prompt-editing approach: explain a proxy model to derive contextual rules rather than search keyword subsets using crowd aesthetic preference. Its separate emotion/context outcomes make it useful for comparing optimization objectives, but the papers do not perform a head-to-head comparison.

## Related pages

- [[Prompt engineering]]
- [[Prompt modifiers]]
- [[Style modifiers]]
- [[Aesthetic quality]]
- [[Random seeds and generation variability]]
- [[Human evaluation of generated images]]
- [[Pairwise aesthetic preference ranking]]
- [[Genetic optimization of prompt keywords]]
- [[Design Guidelines for Prompt Engineering Text-to-Image Generative Models]]
