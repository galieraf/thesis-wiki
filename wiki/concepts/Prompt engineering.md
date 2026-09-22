# Prompt engineering

Prompt engineering is the systematic choice and revision of text inputs to obtain desired model outputs. For text-to-image work, the desired outcome may concern subject representation, style, visual quality, or other user goals.

## Evidence in this wiki

[[Design Guidelines for Prompt Engineering Text-to-Image Generative Models]] (§§3–7) evaluates wording, subject/style keywords, seeds, and optimization length in VQGAN+CLIP. Seeds and optimization length are generation settings that accompany prompt exploration, rather than components of the prompt text itself.

Nine wording permutations did not yield a significant difference in the paper’s outlier analysis ($p=0.55$). This supports prioritizing subject and style keywords within that particular setup, but does not prove wording is irrelevant for other prompts or architectures. The very low inter-rater kappa in this experiment is an important qualification.

## Human-guided keyword search

[[Best Prompts for Text-to-Image Models and How to Find Them]] extends prompt exploration to adaptive search over keyword subsets in Stable Diffusion v1.4. It uses crowd aesthetic preferences across 60 descriptions to guide a genetic algorithm, then evaluates candidates on 12 additional descriptions. See [[Prompt modifiers]] and [[Genetic optimization of prompt keywords]]. Unlike the wording-permutation study above, this changes the keywords themselves and measures set-level aesthetic preference.

## Use in the thesis

Keep the prompt intervention explicit: changing a style keyword, a realism modifier, and sentence structure are different interventions. Record generation settings so their effects are not confused with wording effects. This is an experimental-design implication drawn from the paper.

## Explainable context-sensitive editing

[[RePrompt]] uses a LightGBM proxy, SHAP, and partial dependence plots to derive readable edits for emotional situation texts. It modifies word counts and adjective concreteness and appends an emotion label. Unlike aesthetic keyword-set search, it targets [[Prompt alignment]] along emotion and context dimensions. See [[Explainable prompt editing]].

## Skill and learning

[[Prompting AI Art]] distinguishes judging prompts, writing them, and revising them. Its 2022 participants rarely apply specialist modifiers, and most paired image sets do not improve after one revision. This supports studying [[Prompt engineering skill]] but does not establish a learning curve or make specialist keywords universally necessary.

## Promptist evaluation in HEIM

[[Holistic Evaluation of Text-to-Image Models]] compares Promptist + SD1.4 with the base generator and reports better human-rated aesthetics with comparable alignment. Its summary table also shows much lower photorealism/quality win rate for Promptist, illustrating why “better” must name an outcome. This evaluates a full learned rewriting system, not isolated modifier effects. See [[Holistic text-to-image evaluation]].

## Related pages

- [[Style modifiers]]
- [[Subject-style interaction]]
- [[Random seeds and generation variability]]
- [[Optimization length and perceptual quality]]
