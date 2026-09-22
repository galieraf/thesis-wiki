# Demographic diversity and bias

Demographic diversity describes variation in depicted demographic attributes across generated images. Concentration can reveal representational tendencies, but low diversity is not automatically unfairness: interpretation depends on the prompt and a justified reference distribution. Neither demographic diversity nor fairness is equivalent to general visual diversity.

## Entropy-based assessment in Chen et al. (2024)

Source: [[Evaluating Text-to-Image Generative Models - An Empirical Study on Human Image Synthesis]], §§4.3–4.4, §5.4, Appendix §5.

For each of 51 prompts, the authors generate 500 images and use VQA to infer perceived attributes. Their bins are gender: male/female; race: White/African/Asian/Indian; age: baby/toddler/teenager/middle-aged/old. These are the source’s restricted appearance-label categories, not verified identities.

Answers are grouped into attribute categories, and entropy measures concentration. Prompts are flagged below 0.8 for gender or 1.0 for race/age. The outputs are the proportion of flagged prompts and average entropy among flagged prompts. Entropy here varies **across images**, whereas entropy in [[VQA-based concept coverage]] varies **across repeated answers for one image**.

| Generator | Gender flagged | Race flagged | Age flagged |
| --- | --- | --- | --- |
| SDXL | 51% | 27% | 35% |
| SD2.1 | 41% | 35% | 31% |
| SD1.5 | 51% | 47% | 24% |

The prompts exclude three multi-person interaction concepts. The study finds that improved image quality does not guarantee improvement on every demographic measure.

## Measurement limitations

Overall VQA attribute accuracy is reported as 93.80% for gender, 92.30% for race, and 84.50% for age. The main-text claim that group differences are typically within 1% is qualified by Appendix Table 11: gender accuracy is 82.61% for the group labeled African, versus 97.18% for White and 96.04% for Asian. Aggregate accuracy does not establish negligible evaluator bias.

Prompts include explicit demographic attributes, making low entropy expected in some cases. The aggregate treatment of those cases is not explained sufficiently to treat the headline flagged proportions as universal unfairness rates. Category restrictions, classifier mistakes, subjective visual labels, and threshold selection also constrain the conclusions.

## Use in the thesis

As a proposed extension, compare demographic distributions across prompt-modifier conditions only for attributes not fixed by the prompt, justify the reference distribution, and validate the evaluator by group. Report category proportions as well as entropy: identical entropy can conceal different dominant groups. Keep this assessment separate from [[Aesthetic quality]], [[Anatomical realism]], [[Prompt alignment]], and general image diversity.
