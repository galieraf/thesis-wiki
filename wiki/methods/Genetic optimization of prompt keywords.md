# Genetic optimization of prompt keywords

A genetic search proposes keyword subsets through selection, crossover, and mutation, using human preference evaluation as fitness. The source implementation is [[Best Prompts for Text-to-Image Models and How to Find Them]] (§§3–4).

## Source implementation

- **Representation:** a 100-bit mask over the 100 most popular keywords collected from Stable Diffusion Discord; at most 15 selected keywords.
- **Initialization:** an empty set and the Top-15 most popular keywords.
- **Prompt assembly:** append comma-separated selected keywords alphabetically after the description.
- **Fitness:** mean per-description rank from [[Pairwise aesthetic preference ranking]], using 60 optimization descriptions.
- **Selection:** take the two masks with the highest average ranks.
- **Crossover:** exchange a random segment.
- **Mutation:** change bits with 1% probability.
- **Candidate evaluation:** generate four images per description and add comparisons with previously evaluated candidates.
- **Stopping:** fixed annotation budget; the paper reports 56 iterations and 56 evaluated sets in its figure, without fully specifying how initialization is counted.

The model is Stable Diffusion v1.4 with DDIM, 50 steps, and guidance scale 7.5. The short report does not specify the exact treatment of offspring exceeding the keyword cap, seed policy, or all duplicate-candidate decisions.

## Results and limits

The train-selected candidate achieves validation mean rank 38.00, compared with 12.50 for Top-15 and 5.42 for no keywords. The 12-description validation set supports some transfer to other descriptions within the sampled categories, but does not establish global optimality or transfer across models.

The authors acknowledge local optima and limited keyword exploration. Their rank-based fitness also changes with the candidate pool, complicating convergence assessment. A validation-selected candidate requires an additional untouched test set for a clean final performance estimate; this is a thesis-design recommendation, not part of the reported experiment.

## Related pages

- [[Prompt engineering]]
- [[Prompt modifiers]]
- [[Aesthetic quality]]
- [[Pairwise aesthetic preference ranking]]
