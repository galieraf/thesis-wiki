# Pairwise aesthetic preference ranking

This method compares outputs from two prompt conditions and aggregates choices into relative rankings. In [[Best Prompts for Text-to-Image Models and How to Find Them]] (§§2–4), the compared units are **sets of four images**, not individual images.

## Source protocol

1. Generate four images for every description–keyword-set combination.
2. For each description, sample comparisons between keyword sets. With $n$ candidates the implemented target is $3n\log_2 n$ comparisons.
3. Show the same description and two four-image sets, concealing the modifier keywords, and ask which set is more aesthetically pleasing.
4. Fit Bradley–Terry using Crowd-Kit separately for each description and order the keyword sets by estimated preference.
5. Average the ranks across descriptions. Higher mean rank is better in this paper.

When adding one candidate, the proposed incremental budget is $3[(n+1)\log_2(n+1)-n\log_2 n]$ comparisons per description. The short paper does not detail rounding or all sampling/connectivity decisions needed for replication.

## Quality control

The source inserts comparisons against DALL-E Mini generations, assumes choosing them over Stable Diffusion is an error, and suspends workers below 80% accuracy on these synthetic golden tasks. That assumption can affect the evaluator population and should not be treated as an objective aesthetic truth.

## Interpretation and limitations

Mean rank is conditional on the candidate pool. A rank of 38 is neither 38% preference nor an absolute aesthetic score; changing the pool can change ranks. The source explicitly notes that rank metrics do not reliably establish search convergence.

The method collects aesthetic judgments, not separate alignment or diversity measurements. The paper argues pairwise choices avoid differences in how people use numerical scales, but does not present a controlled comparison proving superiority over rating scales. No detailed inter-rater reliability or uncertainty estimates are reported.

## Related pages

- [[Aesthetic quality]]
- [[Human evaluation of generated images]]
- [[Genetic optimization of prompt keywords]]
