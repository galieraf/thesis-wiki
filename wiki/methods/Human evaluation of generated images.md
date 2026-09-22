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

## Pairwise set preferences in Pavlichenko and Ustalov (2023)

[[Best Prompts for Text-to-Image Models and How to Find Them]] asks Toloka workers to choose the more aesthetically pleasing of two four-image sets for the same description. It uses Bradley–Terry per description and averages keyword-set ranks. This adds a relative aesthetic-preference task to the procedures above; it does not separately measure alignment or diversity. See [[Pairwise aesthetic preference ranking]] and [[Aesthetic quality]] for the protocol and quality-control assumptions.

## Adaptation for the thesis

The following are proposed extensions, not a reproduced protocol from the source: collect separate ratings for subject alignment, style fidelity, and visual quality; randomize presentation; document annotator backgrounds and agreement; and analyze repeated generations without treating every rating as independent by default. Evaluate diversity separately if it is a thesis outcome.

## Alignment ratings and rankings in RePrompt

[[RePrompt]] collects 0–100 IEA/ITA ratings and four-condition rankings from 197 screened workers over 146 image groups. Its rating results favor RePrompt especially for negative emotions, whereas rankings show no significant condition differences. Aggregate-judge correlations are .394 for IEA and .380 for ITA.

IEA is rated before ITA; the two ratings correlate at .764, and later ITA responses are faster. The authors flag possible task-order effects and treat the disagreement between human and CLIP-based ITA as unresolved. For a new study, counterbalancing measurement order would help separate constructs. See [[CLIP-based alignment evaluation]] and [[Emotional expression in generated images]].

## Appraisal and revision in Prompting AI Art

[[Prompting AI Art]] counterbalances separate five-point ratings of prompts and image stimuli, finding a weak correlation ($r=.29$). Its follow-up uses author-consensus judgments of paired five-image sets across seven quality dimensions. These are different protocols: participant aesthetic appraisal versus researcher evaluation of revision. See [[Evaluation of prompt revision]] for the unit of analysis and limitations.

## Loose and strict concept judgments in Chen et al. (2024)

[[Evaluating Text-to-Image Generative Models - An Empirical Study on Human Image Synthesis]] uses volunteers to label concept presence (loose) and concept presence plus defect-free human depiction (strict). These outcomes should be kept distinct: strict judgments combine alignment and realism. The paper reports concept-level correlations with VQA metrics, not interchangeable per-image agreement. Recruitment, validation sample sizes, and inter-rater agreement are insufficiently specified for a full reliability assessment.

Professional annotators also label body parts good, bad, or invisible for [[Anatomical defect evaluation]]. Borderline defects remain subjective. For the thesis, collect separate concept and defect labels before deriving any joint success score; see [[VQA-based concept coverage]].

## Related pages

- [[Style modifiers]]
- [[Random seeds and generation variability]]
- [[Optimization length and perceptual quality]]
- [[Factorial subject-style evaluation]]
