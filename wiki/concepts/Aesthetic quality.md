# Aesthetic quality

Aesthetic quality concerns how visually appealing an image is to an evaluator. It is distinct from faithful representation of a requested subject, compliance with a style, and diversity across multiple outputs.

## Evidence in this wiki

[[Best Prompts for Text-to-Image Models and How to Find Them]] (§§2–4) operationalizes aesthetic appeal as crowd preference between two four-image sets generated for the same description. Per-description Bradley–Terry rankings are averaged across descriptions. This measures relative preference among tested keyword sets, not absolute aesthetic quality.

[[Design Guidelines for Prompt Engineering Text-to-Image Generative Models]] (§5) finds that more VQGAN+CLIP optimization does not guarantee a preferred image; an early image can be preferred before its subject clearly emerges. Its style and joint-representation ratings in other experiments measure different constructs.

## Implications

An attractive result may omit content, and a faithful result may not be preferred aesthetically. A thesis evaluation should therefore name and measure its outcomes separately. Set-level aesthetic choices alone do not establish whether an output collection is diverse or whether one unusually good image dominates the judgment.

## Disentangled aesthetic assessment in Chen et al. (2024)

[[Evaluating Text-to-Image Generative Models - An Empirical Study on Human Image Synthesis]] evaluates aesthetics with [[CAN aesthetic assessment]] and measures [[Anatomical realism]] separately. CAN approximately matches TANet on AVA and improves cross-dataset agreement most clearly on PARA. The model-comparison scores favor Midjourney and SDXL under the tested prompts, but they are automatic predictions, not universal human preference rankings. Aesthetic-score standard deviation measures score stability, not image diversity.

## Aesthetic appeal versus learned preference

[[Pick-a-Pic - An Open Dataset of User Preferences for Text-to-Image Generation]] trains [[PickScore preference prediction]] on general user choices. The aesthetic-only baseline achieves 56.8% tie-aware preference accuracy versus PickScore’s 70.5%. This shows that the tested aesthetic predictor does not capture the full preference task; it does not make preference a pure aesthetic measure. PickScore can also favor appeal at the expense of prompt faithfulness. See [[Human preference in image generation]].

## Aesthetics, clarity, and photorealism in HEIM

[[Holistic Evaluation of Text-to-Image Models]] separately rates aesthetic appeal (five levels), subject clarity (three options), and [[Photorealism]]. Its reported human/LAION-aesthetic correlation is 0.39, reinforcing the need to validate automatic measures in the intended setting. Its fractal metric measures distance from a coefficient of 1.4, a specific proxy assumption rather than a general law of aesthetic quality.

## Related pages

- [[Human evaluation of generated images]]
- [[Pairwise aesthetic preference ranking]]
- [[Optimization length and perceptual quality]]
- [[Prompt modifiers]]
