# Best-of-N image selection

Best-of-N selection generates a candidate pool and returns the image with the highest score. It changes the distribution of delivered outputs without necessarily changing generator parameters. Report the candidate budget and sampling procedure alongside the selected result.

## Pick-a-Pic experiment

Source: [[Pick-a-Pic - An Open Dataset of User Preferences for Text-to-Image Generation]], §6 and Table 2.

For each of 100 held-out prompts, Dreamlike Photoreal 2.0 at CFG 7.5 produces 100 candidates: five initial noises × twenty prompt templates, including the unchanged prompt. Templates add combinations of terms such as award-winning, professional, or highly detailed. PickScore, CLIP-H, and an aesthetic predictor each select a top candidate; random selection and a random unchanged-prompt generation provide controls.

External experts prefer PickScore’s choice at the following reported rates:

| Comparator | PickScore win rate |
| --- | --- |
| Random seed, unchanged prompt | 71.4% |
| Random seed and template | 82.0% |
| Aesthetic-score selection | 85.1% |
| CLIP-H selection | 71.3% |

These are human comparisons between selected outputs, not preference-prediction accuracies. The supplied text does not fully detail annotation aggregation or confidence intervals for these rates.

## Interpretation

The experiment supports selection from a mixed seed/template pool. It does not isolate benefits of each modifier, template variation versus seed variation, or improvement of average unselected outputs. The scorer comparisons share a candidate pool; the unchanged-prompt control has no comparable search procedure.

The authors vary seeds and templates to increase candidate diversity, but do not report a dedicated diversity metric. One preferred image does not establish a diverse delivered collection. Claims that selection reduces diversity would also require separate evidence.

## Thesis adaptation

As a proposed extension, hold base prompts, candidate budgets, seed sets, and generation settings constant across modifier conditions. Report both average candidate quality and selected-output quality; include separate seed-only and template-only comparisons if attributing effects. Evaluate selected outputs with held-out human judgments and distinct alignment/diversity measures, rather than using the selection score as its own sole validation.

## Related pages

- [[PickScore preference prediction]]
- [[Human preference in image generation]]
- [[Prompt modifiers]]
- [[Random seeds and generation variability]]
- [[Genetic optimization of prompt keywords]]
