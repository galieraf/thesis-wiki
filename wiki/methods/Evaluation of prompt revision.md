# Evaluation of prompt revision

[[Prompting AI Art]] (§5) evaluates a single revision by comparing original and revised five-image sets under the same Latent Diffusion seed and configuration.

## Source procedure

Participants see images generated from their three original prompts, revise the prompts once, and may supply negative terms. They do not see revised outputs for further iteration. Fifty returning participants supply 150 paired prompt conditions.

The authors quantify edits with token additions/removals, part-of-speech analysis, and Levenshtein distance. Qualitative edit categories include adjectives/adverbs, subjects, prepositions, paraphrasing/synonyms, reordering, cardinal numbers, simplification, and prompt modifiers.

The authors develop an image-evaluation rubric, code independently during its development, and resolve differences by discussion. The final outcome table records worse/same/better judgments for details, contrast, color, distortions, watermarks, consistency, and overall quality. Overall, 50 sets improve, 77 remain the same, and 23 worsen out of 150.

## Interpretation

The unit is a paired set of five images, not an individual image or participant. Levenshtein distance measures string editing, not semantic improvement. Prompt type-token ratio measures lexical diversity, not output diversity. The image consistency category also should not be relabeled as a validated diversity metric.

The paper’s Study 3 table provides descriptive outcomes; it does not state an inferential test establishing a global null effect of revision. Final author-consensus judgments have no reported independent reliability coefficient.

## Adaptation for the thesis

A proposed extension is to use repeated seeds, blinded/counterbalanced image comparisons, independent raters, uncertainty estimates accounting for repeated participants/prompts, and separate alignment, aesthetics, and diversity outcomes. Multiple rounds and a training control are needed to study learning, while component ablations can separate negative terms from positive-prompt edits.

## Diagnosing failures beyond an average score

[[Prompt Programming for Large Language Models - Beyond the Few-Shot Paradigm]] recommends distinguishing task non-attempts from unsuccessful task execution. For image prompt revision, a proposed extension is to report missing required content separately from fine-detail errors while retaining the overall outcome and excluded fraction. See [[Task-attempt failure analysis]]. The source itself studies language-model translation, not image revision.

## Related pages

- [[Prompt engineering skill]]
- [[Negative prompt terms]]
- [[Human evaluation of generated images]]
- [[Random seeds and generation variability]]
