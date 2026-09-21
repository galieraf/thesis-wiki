# RePrompt: Automatic Prompt Editing to Refine AI-Generative Art Towards Precise Expressions

**Authors:** Yunlong Wang, Shuyuan Shen, and Brian Y. Lim  
**Year:** 2023  
**Source:** [[raw/papers/wang2023reprompt.pdf]]; CHI ’23, 29 pages. DOI: [10.1145/3544548.3581402](https://doi.org/10.1145/3544548.3581402)  
**Last updated:** 2026-09-21

## Research question

How do laypeople edit emotional situation descriptions to improve generated images, how can such edits be automated and made interpretable, and do the edits improve emotional expression while preserving the original context?

## Motivation

Text-to-image models may depict objects mentioned in an everyday emotional account without conveying its intended feeling. Trial-and-error editing is difficult for users, and earlier studies of short subject/style prompts do not settle how to handle natural emotional descriptions. RePrompt seeks readable, actionable edits rather than learned opaque prompt vectors (§§1–3).

## Method

The pipeline has three empirical stages and two additional validation analyses.

1. **Interview study (§4):** 19 university students, aged 19–39, used DALL·E 2 through a researcher-mediated Zoom session. Each completed ten rounds, with extra editing iterations in the first two. Think-aloud interviews and edited texts informed features. Strategies included emphasizing emotion, simplifying text, increasing concreteness, and describing an imagined image in third person. Interview ratings were not reused as independent outcome evaluation because of possible ownership bias.
2. **Proxy model (§5):** generate one VQGAN-CLIP image for each of 10,000 emotional texts. Extract 20 word-level features based on part-of-speech counts and mean word concreteness. Binarize each alignment score as above its mean or not, then train classifiers. LightGBM performed best among tested models; five-fold cross-validation AUC was 0.60 for image–emotion alignment (IEA) and 0.73 for image–text alignment (ITA).
3. **Rule derivation and editing (§§5.4–5.5):** use SHAP and partial dependence plots of the IEA proxy to select salient, tunable features and ranges. Reduce excess nouns/verbs using CLIP-based word saliency, add relevant concrete adjectives from ConceptNet, and append the target emotion label. See [[Explainable prompt editing]].
4. **Evaluation (§6):** compare Original, Manually Edited, Label Appended, and RePrompt prompts using DALL·E 2 images. Compute alignment scores and collect independent human ratings/rankings. The human study uses 146 groups, each containing one randomly selected image from each condition’s four DALL·E 2 outputs.
5. **Additional checks (§6.4.3; Appendix A.5):** compare CLIP emotion scores with Emotion6 human distributions, and apply the rubric to another emotional-text dataset using VQGAN-CLIP.

The editing rubric limits nouns to three and verbs to two when those counts are exceeded. If fewer than two adjectives occur or their mean concreteness is below 2.0, it adds three relevant adjectives with concreteness above 2.0. Noun/verb concreteness ranges were analyzed but not directly enforced, to avoid changing core context. Table 2’s verb rule says “reduce nouns” while targeting two verbs; this appears to be a typo and is interpreted as reducing verbs in the method note.

## Datasets

- **EmpatheticDialogues:** approximately 25,000 emotionally grounded conversations; the study uses situation descriptions and emotion labels, not subsequent dialogue. The proxy dataset contains 10,000 texts covering 32 emotions.
- **Interview/evaluation subset:** initially 200 texts across ten emotions. Removing trusting for label mismatch, anxious due to generation restrictions, and 14 strongly negative texts leaves 146 texts across eight labels: joyful, sad, angry, afraid, lonely, excited, proud, and surprised (§4.1).
- **Word concreteness:** human ratings for approximately 40,000 English lemmas from Brysbaert and colleagues, used for feature construction and adjective filtering.
- **ConceptNet:** related-word source for candidate adjectives.
- **Emotion6:** 1,980 images with distributions over six emotions; used to assess the correspondence between CLIP scores and human emotion annotations.
- **External emotional-text dataset:** Twitter-derived data cited to Saravia et al.; 200 texts per category for sadness, joy, anger, love, surprise, and fear, totaling 1,200. Appendix A.5 compares Original, Label Appended, and RePrompt using VQGAN-CLIP and computational IEA.

The paper does not clearly document whether the 146 evaluation descriptions are disjoint from the 10,000 proxy-training texts. The external dataset provides a separate computational check, not a second human evaluation.

## Models

- **VQGAN-CLIP:** ImageNet-pretrained VQGAN with codebook size 16,384; CLIP ViT-B/16 guidance; 256×256 images; maximum 300 iterations. Used for proxy-data generation and the external-dataset experiment. The proxy-generation workstation had an NVIDIA GeForce RTX 3090.
- **DALL·E 2:** used in the interview and main evaluation; images generated manually through the website under the access available during the study, four outputs per prompt. These historical access details are not current product guidance.
- **Evaluation CLIP:** ViT-B/32; distinct from the ViT-B/16 guidance backbone used for VQGAN-CLIP.
- **Proxy candidates:** Random Forest, XGBoost, LightGBM, and multilayer perceptron; LightGBM selected by cross-validation.
- **Explanations:** SHAP feature importance and partial dependence plots. No generative-model fine-tuning is required by the editing pipeline.

## Metrics

- **IEA:** cosine similarity between the image and target emotion-label embeddings.
- **ITA:** cosine similarity between the image and original situation-text embeddings in the evaluation of context preservation.
- **Human judgments:** 0–100 ratings for text–emotion, image–emotion, and image–text alignment, plus rankings of the four conditions for IEA and ITA.
- **Proxy performance:** AUC for classifying above-mean versus other alignment scores, not image-generation accuracy.
- **Statistics:** linear mixed-effects regression, ANOVA, and post-hoc contrasts. Prompt ID is a random effect for simulation; participant ID is used for the human evaluation. The authors use $p<.001$ as significant and $p<.005$ as marginal.

The paper calls its raw cosine measure “CLIP Score”; its explicit formula should be retained rather than assuming all variants called CLIPScore are interchangeable. See [[CLIP-based alignment evaluation]]. Aesthetic quality and output diversity are not measured outcomes.

## Main findings

- **Computational IEA improves:** all three editing methods outperform Original; RePrompt outperforms the other editing methods. Manual editing scores below simply appending the label (§6.3).
- **Computational ITA declines for RePrompt and manual editing:** both score below Original, whereas Label Appended scores above Original. Thus, improvement in emotion similarity does not imply improved original-text similarity (§6.3).
- **Human ratings favor RePrompt mainly for negative emotions:** 197 of 721 responding Mechanical Turk workers passed screening and completed the survey. Each rated 15 groups, giving 2,955 group evaluations, approximately 20.24 per group. RePrompt had higher overall IEA ratings than the other methods, but the authors describe overall practical differences as very small. Modeling emotion valence showed advantages over the other conditions for negative emotions, not positive emotions (§6.4).
- **Human ITA and computational ITA disagree:** edited conditions received higher overall human ITA ratings than Original. The authors regard context-preservation evidence as mixed: edits may retain key meanings, but earlier IEA questions may influence later ITA ratings. IEA and ITA ratings correlate strongly ($r=.764$), and participants spent less time on ITA (27.4 seconds versus 35.7 seconds).
- **Rankings do not corroborate the rating differences:** no significant condition differences were found for either IEA or ITA rankings, including models that account for emotion type. Rating–rank correlations were weak (IEA $r=-.114$; ITA $r=-.110$).
- **CLIP emotion validity varies by label:** Emotion6 correlations are anger .2420, disgust .3481, fear .4232, sadness .6117, joy .0761, and surprise −.1586 (Appendix Table 8). This supports emotion-dependent metric validity, not an equally reliable emotion measure for all labels.
- **Some transfer evidence:** a rubric derived from VQGAN-CLIP data is useful in the DALL·E 2 evaluation, and the separate 1,200-text experiment supports computational IEA gains on another dataset. Broader transfer remains untested.

Average aggregate-judge correlations were .311 for text–emotion alignment, .394 for IEA, and .380 for ITA. These are the paper’s reported agreement-related statistics, not Cohen’s kappa. Precise mean effect sizes are not tabulated in the main text; no numerical means have been inferred from plot heights in this note.

## Limitations

**Authors’ discussion (§8):** word-level editing can destroy meaningful phrases—for example, interpreting “old friends” as elderly people. Features omit richer syntax and image properties such as style and color. CLIP has uneven emotion sensitivity; text-alignment findings are mixed. Other generative models, expression domains, and user experiences need evaluation.

**Critical reading for the thesis:**

- IEA proxy AUC of 0.60 indicates modest predictive ability. SHAP/PDP patterns describe that proxy, not causal laws of the generator.
- The selected rubric combines deletion, adjective addition, and label appending; the comparisons do not isolate every component’s contribution.
- Heavy participant screening (27.3% pass rate), filtered emotional texts, and a student interview sample constrain generalizability.
- Fixed ordering of IEA before ITA may contaminate supposedly separate judgments. Random selection of one image per condition does not quantify variation across seeds.
- Ratings and rankings support different conclusions; statistical significance should not obscure small practical effects.
- CLIP-derived guidance, proxy targets, saliency, and evaluation share representational assumptions, despite different guidance/evaluation backbones. Human validation remains necessary.
- Emotion expression is not equivalent to aesthetic appeal or diversity. Proposed wellbeing applications are future work, not tested benefits.

## Relevance to my thesis

RePrompt provides an interpretable alternative to [[Genetic optimization of prompt keywords]]: derive context-sensitive editing rules from a proxy instead of searching a universal suffix through crowd preference. It extends [[Design Guidelines for Prompt Engineering Text-to-Image Generative Models]] from subject/style keywords to natural emotional descriptions and word-level concreteness.

For the thesis, it is particularly useful evidence for separating [[Prompt alignment]] from [[Aesthetic quality]], and for checking whether an automated metric agrees with humans within each outcome category. Emotion-targeted edits may improve one aspect of alignment while changing the depicted context.

**Proposed thesis extensions:** validate metrics on the target model and prompt categories; measure aesthetics, alignment, and diversity separately; counterbalance rating-task order; report effect sizes and uncertainty; and ablate deletion, adjective additions, and emotion-label additions using repeated generations.

## Related pages

- [[Prompt engineering]]
- [[Prompt modifiers]]
- [[Prompt alignment]]
- [[Emotional expression in generated images]]
- [[Explainable prompt editing]]
- [[CLIP-based alignment evaluation]]
- [[Human evaluation of generated images]]
- [[Design Guidelines for Prompt Engineering Text-to-Image Generative Models]]
- [[Best Prompts for Text-to-Image Models and How to Find Them]]
