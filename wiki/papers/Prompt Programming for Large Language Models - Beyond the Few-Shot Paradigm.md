# Prompt Programming for Large Language Models: Beyond the Few-Shot Paradigm

**Authors:** Laria Reynolds and Kyle McDonell (KNC.ai).
**Year:** 2021; CHI Conference on Human Factors in Computing Systems Extended Abstracts, May 8–13, Yokohama, Japan.
**Source:** [[raw/papers/reynold2021prompt.pdf]]; [DOI supplied in the paper](https://doi.org/10.1145/3411763.3451760). The filename abbreviates Reynolds as “reynold”; the author is Laria Reynolds. External linked material was not independently inspected.
**Last updated:** 2026-09-22.

## Research question

Can natural-language prompt design elicit capabilities already present in a pretrained language model more effectively than standard few-shot formats, and how should prompts and benchmarks account for this?

## Motivation

Weak performance under one prompt may reflect failure to communicate the task rather than absence of the underlying capability. The authors argue that examples can locate a familiar task in learned knowledge, instead of necessarily teaching the task at inference time. They propose broader prompt programming through instructions, demonstrations, cultural cues, and model-generated task-specific scaffolding (§§1–4).

## Method

The paper combines one quantitative translation experiment with conceptual analysis and illustrative GPT-3 generations.

- Compare original GPT-3 translation results with attempted API reproductions and custom prompt formats on WMT’14 French-to-English.
- Test a simple language-label/colon format with zero, one, or ten demonstrations and a zero-shot translator-role narrative.
- Discuss direct specification, demonstrations, culturally meaningful proxies, and constraints that rule out unintended continuation patterns.
- Propose generating intermediate task decomposition before a final answer and using metaprompts to produce task-specific procedures or contexts.
- Recommend separating non-attempts from poor attempts in evaluation and validating metaprompt reliability across tasks and models.

The reasoning and metaprompt sections do not report a controlled benchmark demonstrating accuracy gains. See [[Task location in prompting]], [[Metaprompt programming]], and [[Task-attempt failure analysis]].

## Datasets

- **Quantitative evaluation:** WMT’14 French-to-English translation, scored with SacreBLEU. The supplied text does not give a complete evaluation signature, exact sample count, example-selection procedure, or all decoding settings.
- **Illustrative material:** a function-composition arithmetic question, an SAT-style analogy, and a fictional expert-generation scenario. These are demonstrations, not a separately quantified test set.
- **Referenced future directions:** closed-ended reasoning benchmarks and text-based games are discussed as evaluation opportunities, not newly evaluated datasets in this paper.

No text-to-image dataset or image-generation experiment is included.

## Models

- GPT-3 API Babbage and Curie for the translation experiment, juxtaposed with the original paper’s 6.7B and 13B model results. The authors note that API changes may explain reproduction differences; the comparison is not a guaranteed match of identical checkpoints.
- GPT-3 Davinci with temperature zero for the stated metaprompt examples.
- BERT is mentioned as a possible future target for constrained fill-in-the-blank prompting, not evaluated here.

API constraints prevent reproducing the original 64-shot test; ten-shot tests replace it in the authors’ own runs.

## Metrics

- Translation quality: BLEU computed using SacreBLEU. BLEU is a translation-overlap score, not classification accuracy or an image-quality measure.
- The paper discusses catastrophic task non-attempts qualitatively but does not report their frequency or conditional BLEU.
- No confidence intervals, significance tests, aggregate reasoning accuracy, image aesthetics, alignment, or diversity measurements are supplied.

## Main findings

**Translation results (Table 1).** Historical results and attempted reproductions must be distinguished.

| Prompt condition | Babbage / original 6.7B | Curie / original 13B |
| --- | --- | --- |
| Original GPT-3 paper, zero-shot | 15.5 | 22.4 |
| Original GPT-3 paper, one-shot | 31.6 | 31.4 |
| Original GPT-3 paper, 64-shot | 36.4 | 38.3 |
| Authors’ reproduction, zero-shot | 15.9 | 18.7 |
| Authors’ reproduction, one-shot | 21.8 | 24.1 |
| Authors’ reproduction, ten-shot | 25.1 | 27.9 |
| Simple colon, zero-shot | 23.5 | 33.3 |
| Simple colon, one-shot | 18.0 | 27.6 |
| Simple colon, ten-shot | 24.1 | 33.4 |
| Translator-role narrative, zero-shot | 26.5 | 32.9 |

Custom zero-shot formats substantially improve on the reproduced zero-shot baselines. Curie’s simple-colon zero-shot score of 33.3 exceeds the reproduced ten-shot score of 27.9 and nearly matches simple-colon ten-shot at 33.4. For Babbage, simple-colon zero-shot (23.5) is below reproduced ten-shot (25.1), while the translator-role prompt (26.5) exceeds it. Thus the prose’s broad statement that simple-colon zero-shot beats the reproduced ten-shot format applies to Curie, not both columns. Neither custom zero-shot result surpasses the original reported 64-shot result.

Adding one demonstration to simple-colon prompting reduces BLEU from 23.5 to 18.0 for Babbage and 33.3 to 27.6 for Curie. The authors attribute this to semantic contamination: the model may treat example content as part of a continuing narrative rather than as format-only guidance. This interpretation is based on output inspection, not an isolated causal mechanism test (§3.2).

**Conceptual contribution.** Prompts can identify tasks directly, demonstrate them, or evoke contextual knowledge through narrative/role cues. The authors advocate constraining plausible continuations and generating intermediate steps before final answers. These are hypotheses and design heuristics, not evidence that every such technique improves accuracy.

**Reasoning-example caveat.** Figure 3’s generated answer says $f(f(3))=27$ for $f(x)=x\times x$. The correct answer is $81$. The example therefore shows a generated stepwise form, not successful arithmetic reasoning. The fictional expert continuation in Figure 5 is also generated content, not a factual biographical source.

## Limitations

- The authors explicitly describe the work as exploratory and limit the quantitative study to one translation task because of budget constraints. Generalization to other tasks or models is not demonstrated.
- Task location is a proposed interpretation, not proof that in-context learning never occurs. Translation benefits may coexist with other forms of example-conditioned adaptation.
- Original/API results differ materially, the 64-shot experiment was not reproduced, and decoding/example-selection details are incomplete.
- The word “significantly” appears in the narrative without a reported inferential test. The table establishes score differences, not statistical significance.
- Semantic contamination and catastrophic non-attempts are not quantified. Mean BLEU alone does not distinguish task selection from execution quality.
- Metaprompting adds opportunities for derailment and incorrect intermediate content. The visibly wrong arithmetic example prevents treating its reasoning illustration as success evidence.
- The probability-based stopping/injection proposal does not fully specify a reproducible online rule for detecting a maximum or handling ties/thresholds.
- The authors’ broader account of language prediction and human-like contextual interpretation is conceptual. It should not be read as established mechanistic evidence or as an instruction to treat a model as a person.
- No text-to-image model, modifier ablation, aesthetic assessment, or image-diversity evaluation is performed.

## Relevance to my thesis

This paper provides historical and conceptual background for [[Prompt engineering]], especially the idea that wording can elicit different behavior without changing model weights. It motivates using meaningful prompt baselines and separating requested-task recognition from execution errors.

For text-to-image work, cultural/role cues offer an analogy to [[Style modifiers]], and metaprompts relate conceptually to automated prompt rewriting. These are connections to test, not image-generation findings from this source. [[RePrompt]] and [[Holistic Evaluation of Text-to-Image Models]] provide more direct image-domain evidence.

A proposed thesis extension is to compare modifier conditions with controlled templates and generation settings, classify missing-subject or wrong-task outputs separately from finer alignment failures, and retain overall performance alongside conditional analyses. Measure aesthetics and diversity independently; neither follows from this paper’s BLEU results.

## Related pages

- [[Task location in prompting]]
- [[Metaprompt programming]]
- [[Task-attempt failure analysis]]
- [[Prompt engineering]]
- [[Prompt modifiers]]
- [[Style modifiers]]
- [[Prompt alignment]]
- [[Evaluation of prompt revision]]
