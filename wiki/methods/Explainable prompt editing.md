# Explainable prompt editing

[[RePrompt]] (§5) derives readable editing rules from explanations of a lightweight predictor of generated-image alignment. This differs from directly explaining the full generator or assuming that model feature importance is causal.

## Pipeline

1. Generate images from 10,000 emotional situation descriptions and calculate CLIP-based alignment.
2. Extract 20 interpretable text features based on part-of-speech counts and mean word concreteness.
3. Train LightGBM to classify above-mean alignment. Five-fold AUC is .60 for IEA and .73 for ITA; the IEA proxy drives rule derivation.
4. Use SHAP to identify important, adjustable features and partial dependence plots to identify ranges associated with above-average model predictions.
5. Convert the findings into text-editing rules, then validate edited prompts with fresh image generations and human judgments.

## RePrompt rubric

| Feature | Observed preferred range | Implemented rule |
| --- | --- | --- |
| Nouns | Count below 4; mean concreteness 3.5–4.2 | If more than 3 nouns, retain 3 using saliency |
| Adjectives | Count above 1; mean concreteness above 2.0 | If count below 2 or mean concreteness below 2.0, add 3 relevant adjectives above 2.0 concreteness |
| Verbs | Count below 3; mean concreteness above 2.0 | If more than 2 verbs, retain 2 using saliency |

Table 2 prints “reduce nouns” in the verb row; the rule above interprets this apparent typo as reducing verbs, consistent with its stated verb-count target. Noun and verb concreteness are not directly adjusted because replacement risks changing context.

The pipeline keeps nouns, verbs, and adjectives; ranks word saliency through CLIP similarity with the full text plus emotion label; retrieves ConceptNet words associated with the three most salient words; filters candidate adjectives by concreteness and saliency; and appends the target emotion label. The authors tested adding 1–5 words and selected three.

## Limits and adaptation

The IEA proxy is modestly predictive. Its explanations describe associations learned from the training data, not universal optimal word counts. Word-level edits can break phrases such as “old friends.” Preserving contextual meaning therefore requires checking more than individual word saliency.

A thesis adaptation should assess component ablations, original-request preservation, and category-specific metric validity. These are proposed extensions; the paper evaluates the combined method against original, manually edited, and label-appended prompts.

## Related pages

- [[Prompt engineering]]
- [[Prompt modifiers]]
- [[Prompt alignment]]
- [[CLIP-based alignment evaluation]]
- [[Genetic optimization of prompt keywords]]
