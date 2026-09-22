# Task-attempt failure analysis

Source: [[Prompt Programming for Large Language Models - Beyond the Few-Shot Paradigm]], §§5.1–5.2.

Separate outputs that never attempt the requested task from outputs that attempt it unsuccessfully. The authors observe that some GPT-3 translation prompts elicit more French text or blank answer spaces instead of an English translation. Mean BLEU hides this distinction.

## Source recommendation

Report results both including all outputs and excluding identifiable task non-attempts, so readers can distinguish failures to communicate the task from failures in executing it. The source does not report non-attempt frequencies or this conditional analysis numerically; it proposes them for future evaluation.

## Thesis adaptation

For image-generation experiments, define failure categories before scoring: for example, a missing required subject versus an identifiable subject with incorrect relations or details. This transfer requires a task-specific rubric; an image is not a language continuation, and ambiguous omissions should not automatically be labeled task non-attempts.

Retain the unconditional metric, the excluded fraction, and the conditional metric together. Conditional performance alone can reward a method that succeeds on a small easy subset. Use independent labels and uncertainty estimates where feasible. These safeguards extend the source’s recommendation.

## Related pages

- [[Task location in prompting]]
- [[Prompt alignment]]
- [[Human evaluation of generated images]]
- [[Evaluation of prompt revision]]
- [[VQA-based concept coverage]]
