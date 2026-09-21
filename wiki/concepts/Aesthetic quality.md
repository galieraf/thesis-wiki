# Aesthetic quality

Aesthetic quality concerns how visually appealing an image is to an evaluator. It is distinct from faithful representation of a requested subject, compliance with a style, and diversity across multiple outputs.

## Evidence in this wiki

[[Best Prompts for Text-to-Image Models and How to Find Them]] (§§2–4) operationalizes aesthetic appeal as crowd preference between two four-image sets generated for the same description. Per-description Bradley–Terry rankings are averaged across descriptions. This measures relative preference among tested keyword sets, not absolute aesthetic quality.

[[Design Guidelines for Prompt Engineering Text-to-Image Generative Models]] (§5) finds that more VQGAN+CLIP optimization does not guarantee a preferred image; an early image can be preferred before its subject clearly emerges. Its style and joint-representation ratings in other experiments measure different constructs.

## Implications

An attractive result may omit content, and a faithful result may not be preferred aesthetically. A thesis evaluation should therefore name and measure its outcomes separately. Set-level aesthetic choices alone do not establish whether an output collection is diverse or whether one unusually good image dominates the judgment.

## Related pages

- [[Human evaluation of generated images]]
- [[Pairwise aesthetic preference ranking]]
- [[Optimization length and perceptual quality]]
- [[Prompt modifiers]]
