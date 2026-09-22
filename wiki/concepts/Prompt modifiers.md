# Prompt modifiers

In a narrow textual sense, prompt modifiers are words or phrases added to a core image description to influence generation. Oppenlaender’s published taxonomy uses a broader scope that also includes subject terms and image prompts. They can request style, lighting, detail, rendering characteristics, or other attributes. [[Style modifiers]] are one subset; a phrase such as `colorful background` also changes a requested scene attribute.

## Six-category taxonomy

[[A taxonomy of prompt modifiers for text-to-image generation]] identifies six practitioner-oriented categories through ethnographic research:

| Category | Intended function |
| --- | --- |
| Subject terms | Specify the subject |
| [[Style modifiers]] | Specify style, medium, technique, or artist-associated appearance |
| [[Image prompts and initial images|Image prompts]] | Provide visual subject/style targets |
| [[Quality boosters]] | Request perceived quality or detail |
| [[Repeating and magic terms|Repeating terms]] | Reinforce a subject or style |
| [[Repeating and magic terms|Magic terms]] | Encourage surprising outcomes through unusual semantic cues |

These categories can overlap. They classify intended uses, not experimentally established effects. Initial images and weighting are discussed in the workflow but are not additional categories. The journal version has six categories, distinct from the earlier five-category description cited in [[RePrompt]].

## Evidence in this wiki

[[Best Prompts for Text-to-Image Models and How to Find Them]] (§§2–4) searches subsets of 100 popular community keywords, capped at 15, and appends them alphabetically after a description. A train-selected 13-keyword set outperforms the popular Top-15 baseline in mean aesthetic rank on 12 validation descriptions (38.00 versus 12.50).

This is evidence about combinations under Stable Diffusion v1.4, not a causal ranking of individual modifiers. The reported random forest importance of `colorful background` does not show that adding it alone always improves an image. Likewise, improved aesthetic preference does not establish improved content alignment or diversity.

## Use in the thesis

Separate the core description from modifier interventions. Retain a no-modifier baseline, evaluate combinations as well as controlled ablations, and document ordering and model settings. These are design implications rather than additional experiments reported by the paper.

## Emotion-oriented additions and deletions

[[RePrompt]] combines adding concrete, context-related adjectives and an emotion label with removing excess nouns and verbs. Its baseline of merely appending the label helps distinguish the full procedure from one simple addition. The combined experiment does not isolate every edit’s causal effect, and improved emotion alignment does not settle original-context preservation. See [[Explainable prompt editing]] and [[Prompt alignment]].

## Evaluation implications from human image synthesis

[[Evaluating Text-to-Image Generative Models - An Empirical Study on Human Image Synthesis]] constructs prompts with optional lighting, camera, style, and HDR/UHD terms but does not isolate their causal effects. Its contribution to modifier research is a framework for reporting [[CAN aesthetic assessment|aesthetics]], [[Anatomical defect evaluation|defects]], [[VQA-based concept coverage|concept success]], and [[Demographic diversity and bias|demographic distributions]] separately.

## Templates combined with seed search in Pick-a-Pic

[[Pick-a-Pic - An Open Dataset of User Preferences for Text-to-Image Generation]] (§6) generates 100 candidates per prompt using five noises and twenty templates, including an unchanged prompt and quality/style additions. [[Best-of-N image selection]] with PickScore improves human preference over the tested controls. Because this combines template choice, seed choice, and scoring, the result does not identify causal benefits of individual modifiers or of templates alone.

## Related pages

- [[Prompt engineering]]
- [[Style modifiers]]
- [[Aesthetic quality]]
- [[Genetic optimization of prompt keywords]]
