# Repeating and magic terms

These are two distinct categories in [[A taxonomy of prompt modifiers for text-to-image generation]] (§§4–5).

| Category | Intended purpose | Evidence boundary |
| --- | --- | --- |
| Repeating terms | Reinforce an existing subject or style through repetition, rephrasing, or synonyms | No controlled repetition ablation or measured average improvement in this paper |
| Magic terms | Encourage surprising outcomes through semantically distant or nonvisual cues | No quantitative diversity evaluation in this paper |

Examples of repetition include describing the same subject in two word orders. Examples of magic terms include `control the soul` and `feel the sound`. “Magic” is the taxonomy’s terminology for the practitioner’s use of unusual cues, not a separate model capability.

The author connects repetition with reinforcement and unusual terms with variation. Treat these as qualitative practice descriptions and hypotheses. Changing a semantic cue is different from changing a random seed; the intended variation may also alter prompt alignment or style.

## Thesis use

Separate repetition count, paraphrasing, and introduction of new semantic content as interventions. If testing magic terms, measure diversity and alignment together rather than equating unpredictability with successful variation.

## Related pages

- [[Prompt modifiers]]
- [[Random seeds and generation variability]]
- [[Prompt alignment]]
