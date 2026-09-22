# CLIP-based alignment evaluation

## Definition used in RePrompt

[[RePrompt]] (§5.2) uses CLIP ViT-B/32 and defines its “CLIP Score” as raw embedding cosine similarity:

$S(c,v)=\frac{c\cdot v}{\lVert c\rVert\lVert v\rVert}$

For image–emotion alignment (IEA), the text embedding represents an emotion label. For image–text alignment (ITA), it represents the situation text; the context-preservation evaluation refers to the original text. Larger cosine indicates greater embedding similarity, not a calibrated probability or aesthetic score. The exact formula matters: do not assume every metric called CLIPScore uses this same formulation.

## Evidence and validity limits

In RePrompt, IEA improvements broadly agree with human ratings for negative emotions. Computational ITA declines for edited prompts while human ITA ratings improve. The authors discuss both imperfect metric validity and possible human rating-order effects.

Emotion6 validation (Appendix Table 8; 1,980 images) compares emotion-label cosine scores with human emotion probability distributions:

| Emotion | Pearson correlation |
| --- | --- |
| Anger | .2420 |
| Disgust | .3481 |
| Fear | .4232 |
| Sadness | .6117 |
| Joy | .0761 |
| Surprise | −.1586 |

All reported correlations are statistically significant, including the weak joy and negative surprise relationships. Statistical significance does not establish adequate measurement validity.

The appendix also demonstrates that meaningless text can produce misleading similarity scores. Text validation helps avoid malformed inputs but cannot solve conceptual limitations of the embedding model. No dedicated aesthetic or diversity outcome follows from this cosine measure.

## Use in the thesis

Record the model backbone, preprocessing, score formula, and reference text. Check human correspondence by prompt category, and consider shared representation bias if CLIP also guides generation or optimization. RePrompt uses ViT-B/16 for VQGAN-CLIP guidance and ViT-B/32 for scoring, but both remain CLIP-based.

## Thresholded CLIP versus concept coverage

[[Evaluating Text-to-Image Generative Models - An Empirical Study on Human Image Synthesis]] uses CLIPScore threshold 0.2 to estimate concept coverage. Across 30 concepts, its correlation with loose human coverage is 0.12–0.19, compared with 0.48–0.71 for closed VQA coverage. This supports checking concept-level validity and calibration; it does not establish that all CLIP-based methods fail. See [[VQA-based concept coverage]] for the exact comparison and the distinction between loose and strict human judgments.

## Preference fine-tuning changes the construct

[[Pick-a-Pic - An Open Dataset of User Preferences for Text-to-Image Generation]] fine-tunes CLIP-H into [[PickScore preference prediction]]. Test preference accuracy rises from zero-shot CLIP-H’s 60.8% to 70.5% under its tie-aware metric, but PickScore sometimes favors aesthetics over faithfulness. Shared architecture does not make a preference-trained score interchangeable with an alignment score.

## Human correspondence in HEIM

[[Holistic Evaluation of Text-to-Image Models]] reports a 0.42 correlation between CLIPScore and human alignment in its benchmark. The supplied text does not fully specify correlation type or aggregation unit; do not present this as a per-image calibration coefficient. HEIM combines CLIP with human questions and object/count/relation diagnostics, and examines alignment changes under [[Prompt perturbation evaluation|input perturbations]].

## Related pages

- [[Prompt alignment]]
- [[Emotional expression in generated images]]
- [[Human evaluation of generated images]]
- [[Explainable prompt editing]]
