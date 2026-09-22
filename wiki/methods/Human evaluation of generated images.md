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

## Original-user preference and external experts in Pick-a-Pic

[[Pick-a-Pic - An Open Dataset of User Preferences for Text-to-Image Generation]] collects general preferences between two images with a tie option. Original prompt authors supply training/test labels, whereas friends and colleagues of the authors serve as expert evaluators. Experts lack the original user’s private intent; their 68.0% agreement and PickScore’s 70.5% use a tie-aware partial-credit metric, not ordinary binary accuracy.

Repeated app interactions retain a winning image and replace its competitor, so observations can share users, prompts, and images. Record these dependencies when designing uncertainty estimates. See [[Human preference in image generation]] and [[PickScore preference prediction]] for split construction and tie handling.

## Anchored ratings in HEIM

[[Holistic Evaluation of Text-to-Image Models]] uses five distinct MTurk Masters per sample, at least 100 images per aspect, and explicit verbal anchors. Alignment progresses from no match to exact match; aesthetics from unappealing to highly appealing; originality from overfamiliar to highly creative. Subject clarity has three options (unclear, uncertain, clear). Photorealism mixes 100 real with 100 generated images and uses five response categories.

The paper reports $0.02 per question, an intended $16/hour, and $13,433.55 total cost. It notes higher variability in aesthetics/originality but supplies no numerical inter-rater reliability in the text. Its metric-based model win rates should not be mistaken for direct human pairwise votes. See [[Photorealism]], [[Perceived originality in generated images]], and [[Holistic text-to-image evaluation]].

## Binary realism questions in REAL

[[REAL - Realism Evaluation of Text-to-Image Generation Models for Effective Data Augmentation]] samples 100 images each from iNaturalist, Birds, and UnRel. Three workers answer each manually constructed attribute/relation question; majority votes become binary labels, and positive-label proportions form image scores. Appendix A.2 describes English-speaking MTurk Masters paid $0.05 per example with an estimated $9 hourly rate. No inter-rater agreement coefficient is supplied.

This validates correspondence to the source’s structured rubric, rather than an unrestricted holistic realism judgment. See [[Schema-based realism evaluation]] for correlations and evaluator dependence.

## Related pages

- [[Style modifiers]]
- [[Random seeds and generation variability]]
- [[Optimization length and perceptual quality]]
- [[Factorial subject-style evaluation]]
