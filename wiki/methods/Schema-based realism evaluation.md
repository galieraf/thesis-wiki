# Schema-based realism evaluation

Source: [[REAL - Realism Evaluation of Text-to-Image Generation Models for Effective Data Augmentation]], §3, Tables 1, 6, and 8.

REAL decomposes evaluation into knowledge-based attribute checks, entity/relation checks, and a learned photo-versus-illustration classifier. The default VQA evaluator is GPT-4o at temperature zero.

## Attribute checks

After an initial existence/realism check, ask whether each schema part is visible and then whether its appearance matches the description. Let $V_i$ be visibility and $M_i$ description match:

$C=\sum_i V_i$, $R=\sum_i V_iM_i$, and $S_{att}=R/C$ if $C>0$, otherwise zero.

The source calls $C$ confidence, but it is a visible-attribute count. Report it with the score: a perfect ratio based on one visible part is not equivalent in coverage to a perfect ratio across many parts. A failed initial gate returns zero.

## Relation checks

Ask about each entity’s presence and realism. Missing entities force zero; otherwise evaluate requested object–relation–object links. The source prints $S_{rel}=\sum_i(V_i+M_i)+\sum_{i\ne j}R_{ij}$, but its benchmark uses scores between zero and one. It does not specify the denominator or precisely how unrequested pairs are excluded. Treat the normalized relationship metric as incompletely specified rather than inventing a formula.

## Style and combination

A CLIP model is fine-tuned on 9,400 real photographs and generated illustrations, producing a photo-class probability $S_{sty}$. Attribute-based augmentation selection uses $S_{att}S_{sty}$. The generator benchmark instead averages its three component scores. These combinations answer different questions and should not be interchanged.

## Validation

Against majority-voted human questions, REAL Spearman correlations are 0.5223 for iNaturalist, 0.6162 for Birds, and 0.5672 for UnRel. Direct GPT scoring with the same knowledge scores 0.2716, 0.1106, and 0.2092. On iNaturalist, substituting BLIP2 drops REAL’s correlation to 0.0255, showing substantial evaluator dependence.

Style fine-tuning improves correlation on a 100-image real/illustration test from 0.7775 to 0.8267. This narrow test does not establish calibration across all generators or styles.

## Use and limits

The method operationalizes realism through [[Fine-grained visual correctness]], realistic entities/relations, and [[Photorealism]]. It is not a general aesthetic or diversity score. Validate schema facts, log evaluator versions and visible counts, and separate requested stylization from unwanted illustrative output. Unlike [[VQA-based concept coverage]], REAL checks structured components per image rather than a single concept’s success frequency across a generation set.

## Related pages

- [[Anatomical defect evaluation]]
- [[Human evaluation of generated images]]
- [[Realism-based data augmentation filtering]]
