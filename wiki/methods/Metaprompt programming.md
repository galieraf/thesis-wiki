# Metaprompt programming

Source: [[Prompt Programming for Large Language Models - Beyond the Few-Shot Paradigm]], §§4.6–4.7 and §5.2.

A metaprompt is a general prompt that, when combined with a particular question, induces the language model to generate task-specific instructions, a procedure, or contextual framing. It shifts part of prompt construction from the human to the model.

## Source proposals

The authors describe short seeds that induce task interpretation and decomposition, and fill-in-the-blank templates that constrain generated sections. A narrative can also ask the model to construct a relevant expert context before answering.

For closed-ended evaluation, they propose allowing intermediate generated text before extracting a verdict. They describe checking the conditional probability of a final-answer cue during generation, then inserting that cue at a maximum. The paper does not fully specify an operational stopping rule. These methods aim to balance additional computation with the risk of derailment.

The stated metaprompt examples use GPT-3 Davinci at temperature zero. No aggregate accuracy or controlled comparison demonstrates general reasoning gains. Figure 3’s arithmetic output is wrong: it gives 27 where $f(f(3))=81$ for $f(x)=x^2$. A plausible procedure is not evidence of a correct result.

## Evaluation implications

The authors recommend testing reliability across tasks and models. For a thesis adaptation involving an LLM that rewrites image prompts, save original and rewritten text, separate rewriting failures from generation failures, and evaluate the final image against the original intent. This is a proposed transfer, not an experiment in the source.

Metaprompting differs from [[Explainable prompt editing]], where RePrompt derives explicit editing rules from a proxy model, and from evaluating an already trained rewriter such as Promptist in [[Holistic Evaluation of Text-to-Image Models]]. These are related approaches to task-specific prompting, not identical mechanisms.

## Related pages

- [[Task location in prompting]]
- [[Prompt engineering]]
- [[Prompt alignment]]
- [[Task-attempt failure analysis]]
