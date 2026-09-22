# Holistic text-to-image evaluation

Source: [[Holistic Evaluation of Text-to-Image Models]], §§2–7, Tables 1–5.

HEIM organizes evaluation into four components:

| Component | Meaning | Example for modifier research |
| --- | --- | --- |
| Aspect | The property being assessed | Aesthetic appeal or original-content alignment |
| Scenario | A prompt dataset/use case | Common scenes, artistic prompts, compositional descriptions |
| Adaptation | How the system receives inputs and runs | Unedited prompt, appended style, or prompt rewriting |
| Metric | The measurement used | Human appeal rating or CLIPScore |

The last column is a thesis adaptation. HEIM itself evaluates 26 systems, 62 scenarios, and twelve aspects: alignment, photorealistic quality, aesthetics, originality, reasoning, knowledge, bias, toxicity, fairness, robustness, multilinguality, and efficiency. It reports 25 metrics, although the named rows in Table 3 appear to total 24.

## Interpretation

No system is strongest on all outcomes. Automated scores should be checked against human judgments: the source reports correlations of 0.42 for alignment, 0.59 for quality, and 0.39 for aesthetics, with insufficient detail in the paper to infer the exact correlation/aggregation convention. These are benchmark findings, not universal calibration constants.

Win rates summarize metric comparisons against other models in the tested pool. They depend on the competitor set and aggregation, unlike an absolute percentage of correct images. Do not confuse them with the human pairwise preference frequencies in [[Best-of-N image selection]].

## Use in the thesis

Choose a justified subset of outcomes rather than collapsing them into a single overall quality score. Hold generation settings and candidate budgets fixed across modifier conditions, use multiple seeds, and preserve separate judgments of appeal, content, and style fidelity. These are proposed design choices. HEIM uses model defaults, which do not equate compute, resolution, filtering, or system adaptation.

Add an explicit visual-diversity outcome if diversity is a research question: neither HEIM’s demographic balance nor its perceived-originality rubric measures general within-prompt diversity.

## Related pages

- [[Aesthetic quality]]
- [[Photorealism]]
- [[Prompt alignment]]
- [[Perceived originality in generated images]]
- [[Human evaluation of generated images]]
- [[Prompt perturbation evaluation]]
