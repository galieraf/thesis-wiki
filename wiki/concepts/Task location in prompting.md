# Task location in prompting

Task location is Reynolds and McDonell’s proposal that a prompt can identify and elicit a task already represented in a pretrained model, rather than teaching that task from a few demonstrations at inference time.

Source: [[Prompt Programming for Large Language Models - Beyond the Few-Shot Paradigm]], §§3–4.

## Evidence and interpretation

The source tests GPT-3 on French-to-English translation. A compact zero-shot language-label format can outperform the authors’ reproduced ten-shot baseline for Curie; a translator-role zero-shot prompt outperforms it for both tested API models. The table does not show that zero-shot universally dominates few-shot prompting.

Translation requires pre-existing language knowledge that a handful of examples cannot supply. This supports task location as an explanation for some prompting effects, but does not establish the absence of in-context learning or identify an exclusive internal mechanism.

The authors also observe lower scores after adding one example and interpret some errors as semantic contamination from the demonstration. Example content can influence the generated continuation instead of merely specifying a format. This is an interpretation of inspected outputs, not a controlled contamination ablation.

## Task specification strategies

- Direct specification names or describes the task, or signals it through formatting.
- Demonstrations illustrate the desired transformation or output format.
- Cultural/narrative proxies invoke familiar roles or situations carrying many implicit expectations.

These strategies can coexist. The source recommends constraining undesired continuations, not merely making the desired output one plausible option.

## Relevance to image prompting

The idea supplies background for [[Prompt engineering]] and an analogy for the contextual associations of [[Style modifiers]]. It does not prove that a diffusion model selects discrete learned tasks in the same way or that role prompting improves image quality. Evaluate such transfers independently.

## Related pages

- [[Metaprompt programming]]
- [[Task-attempt failure analysis]]
- [[Prompt modifiers]]
