# Change log

## 2026-09-21 — Ingest Liu and Chilton (2022)

- Read [[raw/papers/liu2022design.pdf]] and created [[Design Guidelines for Prompt Engineering Text-to-Image Generative Models]] with source attribution, experimental designs, results, limitations, and thesis implications.
- Inspected the existing wiki: the paper, concept, and method folders were empty, as were the index and log.
- Created concepts: [[Prompt engineering]], [[Style modifiers]], [[Subject-style interaction]], [[Random seeds and generation variability]], and [[Optimization length and perceptual quality]].
- Created methods: [[Human evaluation of generated images]] and [[Factorial subject-style evaluation]].
- Added reciprocal cross-links and populated [[wiki/index|the index]]. Flagged source count inconsistencies, low annotator agreement, and limits of transferring these findings to other models or diversity evaluation.
- Source files in `raw/` were left unchanged.

## 2026-09-21 — Ingest Pavlichenko and Ustalov (2023)

- Read [[raw/papers/pavlichenko2023bestprompts.pdf]] and created [[Best Prompts for Text-to-Image Models and How to Find Them]], including generation settings, search protocol, baseline/validation ranks, and thesis relevance.
- Inspected existing concepts and methods before adding [[Prompt modifiers]], [[Aesthetic quality]], [[Pairwise aesthetic preference ranking]], and [[Genetic optimization of prompt keywords]].
- Updated [[Prompt engineering]], [[Style modifiers]], [[Random seeds and generation variability]], [[Human evaluation of generated images]], and [[Design Guidelines for Prompt Engineering Text-to-Image Generative Models]] with related evidence and links.
- Updated [[wiki/index|the index]]. Distinguished relative aesthetic ranks from alignment/diversity, validation selection from final testing, and predictive keyword importance from causal effects. Recorded search-reporting and annotation limitations.
- Source files in `raw/` were left unchanged. External code/data links are attributed to the paper and were not independently inspected.

## 2026-09-21 — Ingest Wang, Shen, and Lim (2023)

- Resolved the extensionless source reference to [[raw/papers/wang2023reprompt.pdf]] and created [[RePrompt]] with the required paper sections, study designs, rubric, results, and limitations.
- Created [[Prompt alignment]], [[Emotional expression in generated images]], [[CLIP-based alignment evaluation]], and [[Explainable prompt editing]] after inspecting existing pages.
- Updated [[Prompt engineering]], [[Prompt modifiers]], [[Human evaluation of generated images]], and both previously ingested paper pages with relevant cross-links.
- Updated [[wiki/index|the index]]. Preserved the mixed ITA findings, null ranking results, small overall rating effects, emotion-dependent CLIP validity, and apparent Table 2 verb-rule typo.
- Left all files in `raw/` unchanged.

## 2026-09-21 — Ingest Oppenlaender’s modifier taxonomy

- Resolved the requested filename to [[raw/papers/A taxonomy of prompt modifiers for text-to-image generation.pdf]] and created [[A taxonomy of prompt modifiers for text-to-image generation]] with journal year 2024 and online publication date 28 November 2023.
- Expanded [[Prompt modifiers]] with the six categories and updated [[Style modifiers]] to explain overlapping functions.
- Added [[Quality boosters]], [[Repeating and magic terms]], [[Image prompts and initial images]], and [[Ethnographic analysis of prompt modifiers]] after inspecting existing notes.
- Updated [[wiki/index|the index]], separated intended effects from measured outcomes, and distinguished the published six-category version from the earlier description cited in [[RePrompt]].
- Left `raw/` unchanged.

## 2026-09-21 — Ingest Prompting AI Art

- Resolved the requested title to [[raw/papers/Prompting AI Art  An Investigation into the Creative Skill of Prompt Engineering.pdf]] and created [[Prompting AI Art]], recording the 2025 journal year, November 2024 online publication, and 2022 study dates separately.
- Added [[Prompt engineering skill]], [[Negative prompt terms]], and [[Evaluation of prompt revision]] after reviewing existing pages.
- Updated [[Prompt engineering]], [[Human evaluation of generated images]], and [[A taxonomy of prompt modifiers for text-to-image generation]] with reciprocal connections; updated [[wiki/index|the index]].
- Flagged overlapping participant counts, inconsistent revised-image totals, weak appraisal correlation, and limits of single-revision evidence. Kept lexical diversity distinct from image diversity.
- Left all source files in `raw/` unchanged.

## 2026-09-22 — Ingest Chen et al. (2024)

- Resolved the extensionless reference to [[raw/papers/chen2024human.pdf]] and read the supplied arXiv v2 paper and appendix; created [[Evaluating Text-to-Image Generative Models - An Empirical Study on Human Image Synthesis]] with all required paper sections.
- Inspected existing notes before adding [[Anatomical realism]], [[Demographic diversity and bias]], [[CAN aesthetic assessment]], [[Anatomical defect evaluation]], and [[VQA-based concept coverage]].
- Updated [[Aesthetic quality]], [[Prompt alignment]], [[Prompt modifiers]], [[Human evaluation of generated images]], and [[CLIP-based alignment evaluation]]; added all new pages to [[wiki/index|the index]].
- Distinguished automated estimates from human judgments, single-concept alignment from compositional alignment, and demographic entropy from general image diversity. Flagged strict-coverage construct mixing and the appendix’s evaluator group-accuracy gap.
- Recomputed the 30-row coverage means in Tables 12–14: closed means reproduce Table 5, but open means do not. Preserved both reported and recomputed values with the discrepancy unresolved.
- Left all files in `raw/` unchanged. The source-linked external code/data repository was not independently inspected.

## 2026-09-22 — Ingest Kirstain et al. (2023)

- Read [[raw/papers/kirstain2023pickapic.pdf]], including the appendix, and created [[Pick-a-Pic - An Open Dataset of User Preferences for Text-to-Image Generation]] with the required paper sections.
- Inspected existing concepts and methods before creating [[Human preference in image generation]], [[PickScore preference prediction]], and [[Best-of-N image selection]].
- Updated [[Aesthetic quality]], [[Prompt alignment]], [[Prompt modifiers]], [[Random seeds and generation variability]], [[Human evaluation of generated images]], [[CLIP-based alignment evaluation]], and [[Pairwise aesthetic preference ranking]]; updated [[wiki/index|the index]].
- Distinguished experimental dataset counts from later releases, prompt-disjoint from user-disjoint splits, tie-aware accuracy from ordinary accuracy, and aggregate ranking correlations from per-image agreement. Qualified the “superhuman” claim and the ambiguously labeled training-seed spread.
- Kept seed/template selection gains separate from causal modifier effects and dedicated alignment/diversity outcomes. Left all files in `raw/` unchanged; external source-linked resources were not independently inspected.

## 2026-09-22 — Ingest Lee et al. (2023), HEIM

- Read [[raw/papers/lee2023heim.pdf]], including scenario/metric/model details and the human-evaluation appendix, and created [[Holistic Evaluation of Text-to-Image Models]] with the required paper sections.
- Inspected existing pages before adding [[Holistic text-to-image evaluation]], [[Prompt perturbation evaluation]], [[Photorealism]], and [[Perceived originality in generated images]].
- Updated [[Style modifiers]], [[Prompt engineering]], [[Aesthetic quality]], [[Prompt alignment]], [[Human evaluation of generated images]], [[CLIP-based alignment evaluation]], and [[Demographic diversity and bias]]; updated [[wiki/index|the index]].
- Preserved the 2023 model/version scope and distinguished metric win rates, human ratings, photorealism, aesthetics, representation bias, and performance fairness. Recorded the Promptist outcome trade-off and the lack of a dedicated visual-diversity measure.
- Flagged incomplete correlation reporting, the headline metric-count/Table 3 discrepancy, and editorial artifacts in Appendix B.2. Kept perceived originality separate from proven novelty or legal conclusions.
- Left all files in `raw/` unchanged. External source-linked benchmark/code resources were not independently inspected.
