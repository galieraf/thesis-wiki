# CAN aesthetic assessment

Source: [[Evaluating Text-to-Image Generative Models - An Empirical Study on Human Image Synthesis]], §§3.1–3.2, §5.1, Appendix §§2.1–2.4.

CAN combines CLIP-derived style features, ResNet-34 generic aesthetic features, and attention-based fusion to predict aesthetic scores. Its training objective combines score regression with a classification task identifying distortions such as brightness changes, blur, downsampling, or composition changes. It assesses image aesthetics, not the attractiveness of the depicted individual.

## Training and validation

The main model is trained on AVA. CAN/TANet SRCC is 0.754/0.755 on AVA, 0.751/0.721 on PARA, and 0.643/0.640 on TAD66K; pairwise ranking accuracy is 0.780/0.780, 0.681/0.614, and 0.431/0.420. The evidence supports cross-dataset gains, particularly on PARA, rather than a uniform large improvement.

Removing the distortion task changes AVA SRCC from 0.754 to 0.751; removing the generic module gives 0.744 and removing the style module gives 0.644 (Table 7).

The described released predictor adds PARA fine-tuning of fully connected layers with the rest frozen, for attributes including object emphasis, composition, color, content, and light. Distinguish that variant from the AVA-only model in the cross-dataset comparison.

## Interpretation for the thesis

CAN can supply an automatic [[Aesthetic quality]] outcome, but training-dataset agreement does not guarantee agreement on all generated images or modifier conditions. Validate it on a relevant human-rated subset. The “content” aesthetic attribute is not a substitute for text-conditioned [[Prompt alignment]]. Lower variation in aesthetic scores does not establish lower or higher visual diversity.

## Related pages

- [[Human evaluation of generated images]]
- [[Anatomical realism]]
- [[Prompt modifiers]]
