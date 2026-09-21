# Factorial subject-style evaluation

A factorial design crosses subject choices with style choices to distinguish their effects and investigate whether the effect of one depends on the other.

## Source implementation

[[Design Guidelines for Prompt Engineering Text-to-Image Generative Models]] (§7) generates 1,581 images from 51 subjects × 31 styles, then analyzes ratings through a 2×2 grouping:

- Subject category: abstract or concrete.
- Style category: abstract or figurative.

Two annotators with art/design domain knowledge score joint subject–style representation from 1 to 5, with randomized image order. The authors report significant main effects and interaction using two-way ANOVA (all $p<0.01$). See [[Subject-style interaction]] for the group means.

This is a 51×31 generation design analyzed through broader categories; it is not just four individual prompts. The source derives subject abstraction/concreteness from an external word-rating dataset.

## Adaptation for the thesis

The following are design implications rather than additional findings of the paper:

1. Define a subject set and modifier conditions, including an appropriate baseline.
2. Cross conditions across subjects and repeat generation with recorded seeds while holding other settings fixed.
3. Measure content alignment, style fidelity, visual quality, and diversity with explicitly separate outcomes where relevant.
4. Analyze modifier effects and interactions while accounting for repeated subjects, seeds, and annotators.
5. Inspect failure cases such as subject omission and repetitive motifs alongside aggregate scores.

The original experiment uses a joint representation score and broad categories, so it cannot directly establish which dimension caused a score change. Its reported significance should not substitute for effect sizes, uncertainty estimates, or replication in a new model.

## Related pages

- [[Subject-style interaction]]
- [[Style modifiers]]
- [[Human evaluation of generated images]]
- [[Random seeds and generation variability]]
