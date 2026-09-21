# Prompt modifiers

Prompt modifiers are words or phrases added to a core image description to influence generation. They can request style, lighting, detail, rendering characteristics, or other attributes. [[Style modifiers]] are one subset; a phrase such as `colorful background` also changes a requested scene attribute.

## Evidence in this wiki

[[Best Prompts for Text-to-Image Models and How to Find Them]] (§§2–4) searches subsets of 100 popular community keywords, capped at 15, and appends them alphabetically after a description. A train-selected 13-keyword set outperforms the popular Top-15 baseline in mean aesthetic rank on 12 validation descriptions (38.00 versus 12.50).

This is evidence about combinations under Stable Diffusion v1.4, not a causal ranking of individual modifiers. The reported random forest importance of `colorful background` does not show that adding it alone always improves an image. Likewise, improved aesthetic preference does not establish improved content alignment or diversity.

## Use in the thesis

Separate the core description from modifier interventions. Retain a no-modifier baseline, evaluate combinations as well as controlled ablations, and document ordering and model settings. These are design implications rather than additional experiments reported by the paper.

## Related pages

- [[Prompt engineering]]
- [[Style modifiers]]
- [[Aesthetic quality]]
- [[Genetic optimization of prompt keywords]]
