# Prompt perturbation evaluation

Source: [[Holistic Evaluation of Text-to-Image Models]], §§3–5, §7 findings 9–11, Appendix B.2 and C.2.

Compare an original prompt set with transformed versions and measure changes in human-rated alignment or CLIPScore. HEIM distinguishes three purposes:

| Purpose | Transformation | Desired behavior |
| --- | --- | --- |
| Robustness | Lowercase, contract phrases, introduce common misspellings with 0.1 probability per word, vary spaces from one to three | Preserve fulfillment of the intended content |
| Fairness | Replace male with female terms, or apply available word-level African American English substitutions | Maintain alignment performance for the changed group/language variety |
| Multilinguality | Google Cloud translation of English into Chinese, Hindi, or Spanish | Fulfill the translated request comparably |

Gender substitution changes requested content; identical images are not the target. Word-level dialect conversion is a restricted synthetic approximation, not a complete test of naturally authored dialect. Translation and typo transformations also require meaning checks before treating them as controlled comparisons.

## Evidence

Around half the evaluated systems show alignment drops under gender/dialect changes or typos. Typo losses are generally no more than 0.2 on the five-point scale; Openjourney’s dialect loss is 0.25. DALL-E 2 loses 0.536/0.162/2.640 from its 4.438 English alignment score under Chinese/Spanish/Hindi respectively. Results are specific to these transformations and the 2023 model snapshot.

## Thesis adaptation

Record both baseline and transformed performance, the direction of change, and uncertainty. A small gap alone does not imply strong performance when both scores are low. Validate meaning preservation and use matched seeds where appropriate. Deliberate [[Prompt modifiers]] may change requested appearance, so do not assume every modifier should satisfy semantic invariance.

## Related pages

- [[Prompt alignment]]
- [[Demographic diversity and bias]]
- [[Holistic text-to-image evaluation]]
- [[Human evaluation of generated images]]
