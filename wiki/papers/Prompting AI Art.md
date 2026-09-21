# Prompting AI Art: An Investigation into the Creative Skill of Prompt Engineering

**Authors:** Jonas Oppenlaender, Rhema Linder, and Johanna Silvennoinen  
**Year:** 2025 (journal issue); first published online 28 November 2024  
**Source:** [[raw/papers/Prompting AI Art  An Investigation into the Creative Skill of Prompt Engineering.pdf]]; International Journal of Human–Computer Interaction, 41(16), 10207–10229. DOI: [10.1080/10447318.2024.2431761](https://doi.org/10.1080/10447318.2024.2431761)  
**Last updated:** 2026-09-21

## Research question

Can people discern prompt quality, write effective prompts for digital artworks, and improve their prompts after seeing generated images? The broader question is whether prompt engineering is intuitive or requires learned vocabulary and practice.

## Motivation

Descriptive language is accessible, but community-specific style and quality modifiers may be unfamiliar. Distinguishing the ability to judge a prompt from the ability to construct and refine one matters for interface design, creative support, and education. The authors examine relatively inexperienced participants before text-to-image tools became widely familiar (§§1–2).

## Method

Three consecutive Mechanical Turk studies separate appraisal, authorship, and revision (Table 1):

| Study | Dates | Sample and task |
| --- | --- | --- |
| 1: Appraisal | May 19–23, 2022 | 52 participants separately rate 20 prompts and corresponding Midjourney image stimuli on a five-point Absolute Category Rating scale; presentation blocks counterbalanced |
| 2: Authorship | June 12–23, 2022 | 125 participants write three prompts each to maximize visual attractiveness; no generated images shown and no modifier instruction |
| 3: Revision | June 20–27, 2022 | 50 returning participants view five generated images per original prompt and revise each prompt once; optional negative terms are explained and allowed |

Study 1 uses 20 stimuli selected from 111 author-generated Midjourney examples: ten volunteers classify aesthetic quality, and only unanimously classified examples are retained, ten high and ten low. Filenames are anonymized; a duplicate-image consistency check excludes ratings differing by more than one category.

Study 2 analyzes modifier presence manually and descriptive language using token counts, part-of-speech counts, and type-token ratio. Study 3 analyzes edits using Levenshtein distance, added/removed tokens, and eight qualitative edit categories. Authors compare original and revised five-image sets for details, contrast, color, distortions, watermarks, consistency, and overall quality; coding criteria are developed and revised collaboratively and disagreements resolved by discussion (§§3–5).

There is only one revision opportunity, not a longitudinal learning intervention. Revised outputs are not returned for additional participant iteration. See [[Evaluation of prompt revision]].

## Datasets

- **Study 1 corpus:** 111 author-generated Midjourney examples, initially 59 failed and 52 high-quality attempts; 20 selected for the participant experiment. The paper describes retaining the four-image-per-prompt format, so distinguish displayed image stimuli from individual generated tiles.
- **Study 2:** 375 prompts from 125 participants, with subjects frequently including landscapes, sunsets, and animals.
- **Study 3:** 150 prompt pairs from 50 returning participants, with five-image sets for each prompt condition. Nineteen participants provide 39 negative-term entries.
- **Initial generation:** 1,875 images from all 375 original prompts, five each.

**Reporting caveats:** the article calls the combined sample 227 participants, but 52 + 125 + 50 counts study participation and includes returning participants; it should not be described as 227 unique people. The generation section also reports another 1,875 revised images, which does not reconcile with 50 returning participants × 3 prompts × 5 images = 750 revised images. Table 3 clearly evaluates 150 paired sets. Retain the discrepancy when discussing corpus size rather than silently correcting it.

No external benchmark dataset, train/test split, or trained prediction model is central to these studies.

## Models

- **Study 1:** Midjourney images created by the first author; a specific version and full generation settings are not supplied in the main protocol.
- **Studies 2–3 output generation:** Latent Diffusion `text2img-large`, 1.4 billion parameters; seed 1040790415, eta 1.0, 100 DDIM steps, guidance scale 5.0, resolution 256×256, five images per prompt. The same configuration and seed are used for original and revised generations.
- Other systems, including CLIP Guided Diffusion, DALL-E mini, Disco Diffusion, and Majesty Diffusion, were explored during system selection, not used as controlled comparative baselines.

The evaluated Latent Diffusion setup should not be renamed Stable Diffusion v1.4. The experiments predate Stable Diffusion’s public release; later systems discussed in the paper are contextual examples, not evaluated replacements.

## Metrics

- Five-point Absolute Category Ratings of actual images and imagined outputs from textual prompts.
- Pearson correlation between paired prompt/image ratings; Kruskal–Wallis and Bonferroni-corrected Dunn comparisons in Study 1.
- Fleiss’ kappa for the initial ten-volunteer high/low image classification: .34, 95% CI [.31, .37]. Final stimuli are deliberately selected from unanimous judgments.
- Prompt token counts, part-of-speech frequencies, and type-token ratio $TTR=\text{unique word types}/\text{word tokens}$.
- Levenshtein distance and qualitative edit codes for revisions.
- Author-consensus worse/same/better judgments on paired image sets across seven outcome dimensions.

TTR measures lexical diversity of prompt text, not visual diversity of generated images. “Consistency” in the paired-set rubric is not a validated diversity metric. No CLIPScore, FID, or dedicated prompt-alignment score is used as an outcome here.

## Main findings

**Appraisal is possible but weakly predictive (§3.2).** Participants distinguish the selected high/low groups. Mean image ratings are 3.70 versus 3.39; corresponding prompt ratings are 3.87 versus 2.78. Prompt and image ratings correlate at $r=.29$, 95% CI [.23, .34], $p<10^{-15}$. This weak association supports partial appraisal ability, not precise prediction of generation quality.

**Descriptive language does not imply specialist modifier knowledge (§4.2).** Prompts average 12.54 tokens (SD 14.65), with mean TTR .94; 58.13% contain no repeated tokens. Only one participant deliberately uses the community modifier `unreal engine` in all three prompts, though a small number of others include generic or explicit style cues. Eighteen participants (14.4%) give instructions rather than image descriptions. These patterns concern the interfaces and sample of 2022, not universal inadequacy of conversational prompting.

**Revision mostly adds description (§5.2).** Participants add 538 tokens and remove 243; mean Levenshtein distance is 28.1 (SD 25.0). Adjective changes are common and style-modifier adoption remains sparse. Eleven prompts (7.33%) are unchanged with no negative terms.

**Most paired sets do not improve overall (Table 3).**

| Outcome | Worse | Same | Better |
| --- | --- | --- | --- |
| Details | 17 (11.3%) | 81 (54.0%) | 52 (34.7%) |
| Contrast | 17 (11.3%) | 85 (56.7%) | 48 (32.0%) |
| Color | 12 (8.0%) | 88 (58.7%) | 50 (33.3%) |
| Distortions | 32 (21.3%) | 99 (66.0%) | 19 (12.7%) |
| Watermarks | 31 (20.7%) | 85 (56.7%) | 34 (22.7%) |
| Consistency | 23 (15.3%) | 95 (63.3%) | 32 (21.3%) |
| Overall | 23 (15.3%) | 77 (51.3%) | 50 (33.3%) |

Each row covers 150 paired five-image sets, not 150 independent participants or individual images. Approximately 70% retain the same or very similar style. The paper broadly says participants could not significantly improve artworks, but its Study 3 outcome table reports descriptive counts rather than a specific inferential test of aggregate improvement. Some revisions clearly do improve outputs.

**Negative terms have mixed results (§5.2.4).** Nineteen of 50 participants use them; some attempt to remove objects, colors, text, or watermarks, while some misunderstand their operation. The examples illustrate successful and failed edits rather than an isolated causal test of negative conditioning.

**Interpretation and futures (§6).** The authors interpret the findings as evidence that prompt engineering involves acquired vocabulary and skill. They discuss four speculative futures: expert skill, everyday skill, obsolete skill, and personal-signature/curation skill. These are scenarios, not empirical predictions.

## Limitations

- Only one revision and no training condition: the studies cannot quantify a learning curve, establish required practice time, or prove an innate-versus-learned dichotomy.
- Only 40% of Study 2 participants return; attrition may affect revision results. Prior experience is self-reported and sometimes ambiguous.
- The sample and models reflect 2022. Do not generalize modifier scarcity or difficulty with instructions to present-day populations and interfaces.
- Study 1 uses author-curated examples and unanimous high/low extremes, limiting representativeness of the correlation and appraisal findings.
- Image quality is subjective. Author-consensus revision coding has no reported final independent reliability statistic, and prompt-modifier coding is primarily by one author.
- Instructions request attractive artworks but do not explicitly train or request stylistic edits; the authors acknowledge this may reduce modifier changes. Lack of specialist terms alone does not establish failure to meet user intent.
- A fixed seed/configuration helps compare edits but does not test robustness across independent seeds or generators.
- Table counts, participation totals, and some figure labels contain reporting inconsistencies. Figure examples are explicitly selected and not representative of the complete corpus.

## Relevance to my thesis

This paper connects [[Prompt engineering skill]] with [[Prompt modifiers]]: knowing how to describe an image differs from knowing model-specific style and quality cues. It complements [[A taxonomy of prompt modifiers for text-to-image generation]] by studying whether participants spontaneously use such cues.

It provides a design for separating prompt appraisal, prompt authorship, and revision, plus a multidimensional revision rubric. For a thesis on quality, diversity, and alignment, its limits motivate measuring those outcomes independently and documenting participant experience, model settings, and instruction effects.

**Proposed extensions:** compare novice/expert or trained/untrained groups over multiple iterations; retain no-edit and modifier-ablation controls; assess repeated seeds; and measure original-intent preservation alongside aesthetic change. These are proposed experiments, not findings established here.

## Related pages

- [[Prompt engineering]]
- [[Prompt engineering skill]]
- [[Prompt modifiers]]
- [[Style modifiers]]
- [[Negative prompt terms]]
- [[Evaluation of prompt revision]]
- [[Human evaluation of generated images]]
- [[A taxonomy of prompt modifiers for text-to-image generation]]
