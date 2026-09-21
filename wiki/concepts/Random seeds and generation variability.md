# Random seeds and generation variability

A random seed controls stochastic initialization in the evaluated generation procedure. Multiple seeds can yield different compositions and perceived outcomes from the same prompt; recording the seed supports reproduction within an otherwise fixed setup.

## Evidence in this wiki

[[Design Guidelines for Prompt Engineering Text-to-Image Generative Models]] (§4) evaluates nine seeds across 12 subjects and 12 styles (1,296 images). Annotators identify outliers within randomized 3×3 grids. The paper reports a significant result ($p<0.01$, Fisher’s exact test), with slight inter-rater agreement ($\kappa=0.13$).

The authors recommend exploring 3–9 seeds per prompt. They do not demonstrate that this range is statistically optimal, or that a particular seed consistently produces better images.

## Variability versus diversity

The experiment establishes evidence of perceived differences under seed changes in its setup. It does not quantify semantic diversity, visual coverage, or mode collapse with a dedicated diversity metric. Treat seed sampling as part of evaluation design, not as a diversity score.

## Use in the thesis

A practical extension is to compare modifier conditions across repeated, recorded seeds and report variability rather than selecting one favorable image. The appropriate number of samples must be justified for the thesis experiment; the historical 3–9 recommendation alone is insufficient.

## Multi-image evaluation in Pavlichenko and Ustalov (2023)

[[Best Prompts for Text-to-Image Models and How to Find Them]] uses four images per description–keyword-set combination and compares whole image sets. This reduces reliance on a single displayed generation, but the paper does not specify seed control or test how many samples are sufficient. Four-image aesthetic preference is not a diversity metric. See [[Pairwise aesthetic preference ranking]].

## Related pages

- [[Prompt engineering]]
- [[Human evaluation of generated images]]
- [[Factorial subject-style evaluation]]
