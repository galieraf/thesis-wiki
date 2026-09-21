# Human evaluation of generated images

Human evaluation should specify the construct being judged. Preference, style fidelity, subject alignment, and visual difference are not interchangeable.

## Procedures in Liu and Chilton (2022)

Source: [[Design Guidelines for Prompt Engineering Text-to-Image Generative Models]], §§3–7.

| Task | Procedure | Main limitation |
| --- | --- | --- |
| Outlier judgment | Two annotators inspect randomized 3×3 grids for better/worse or visibly different outputs; judgments collapse to same/outlier | Mixes difference and quality; does not measure diversity directly |
| Checkpoint preference | Choose one preferred image from a row of ten optimization checkpoints | Aesthetic preference can favor an image before the subject appears |
| Style representation | Rate 1–5, from extremely poor to excellent representation, using presence of stylistic motifs; ignore subject quality | Measures style, not full prompt fulfillment |
| Joint subject–style representation | Rate 1–5, from extremely poor to excellent representation of subject and style | A single score does not isolate content and style errors |

For style judgments, the anchors progress from no motifs (1), few (2), some (3), a high number (4), to a very high number (5). The source supplies Google Images references for annotators when needed. The subject–style rubric uses overall representation rather than explicit motif counts.

## Agreement and interpretation

The paper reports Cohen’s kappa of 0.0013, 0.13, and 0.33 in Experiments 1, 2, and 3 respectively. Raw agreement for Experiment 1 is 71.3%, illustrating that raw agreement and chance-corrected agreement can differ substantially. High raw agreement alone does not resolve reliability concerns.

The authors use chi-square, Fisher’s exact, Mann–Whitney, Kruskal–Wallis, correlation, and ANOVA analyses across tasks. A nonsignificant result should be recorded as a failure to detect a difference, not proof of equivalence. Five-point ratings are ordinal; their treatment in analysis should be explicitly justified in a new study.

## Adaptation for the thesis

The following are proposed extensions, not a reproduced protocol from the source: collect separate ratings for subject alignment, style fidelity, and visual quality; randomize presentation; document annotator backgrounds and agreement; and analyze repeated generations without treating every rating as independent by default. Evaluate diversity separately if it is a thesis outcome.

## Related pages

- [[Style modifiers]]
- [[Random seeds and generation variability]]
- [[Optimization length and perceptual quality]]
- [[Factorial subject-style evaluation]]
