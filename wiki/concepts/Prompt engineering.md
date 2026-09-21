# Prompt engineering

Prompt engineering is the systematic choice and revision of text inputs to obtain desired model outputs. For text-to-image work, the desired outcome may concern subject representation, style, visual quality, or other user goals.

## Evidence in this wiki

[[Design Guidelines for Prompt Engineering Text-to-Image Generative Models]] (§§3–7) evaluates wording, subject/style keywords, seeds, and optimization length in VQGAN+CLIP. Seeds and optimization length are generation settings that accompany prompt exploration, rather than components of the prompt text itself.

Nine wording permutations did not yield a significant difference in the paper’s outlier analysis ($p=0.55$). This supports prioritizing subject and style keywords within that particular setup, but does not prove wording is irrelevant for other prompts or architectures. The very low inter-rater kappa in this experiment is an important qualification.

## Use in the thesis

Keep the prompt intervention explicit: changing a style keyword, a realism modifier, and sentence structure are different interventions. Record generation settings so their effects are not confused with wording effects. This is an experimental-design implication drawn from the paper.

## Related pages

- [[Style modifiers]]
- [[Subject-style interaction]]
- [[Random seeds and generation variability]]
- [[Optimization length and perceptual quality]]
