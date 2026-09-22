# Photorealism

Photorealism concerns whether an image looks like a real photograph. It is distinct from [[Aesthetic quality]], [[Prompt alignment]], and [[Anatomical realism]]. A stylized image can be attractive and faithful while intentionally non-photorealistic; photographic appearance can coexist with anatomical errors.

## HEIM operationalization

[[Holistic Evaluation of Text-to-Image Models]] uses photorealism as its image-quality aspect. Human raters see a mix of 100 real and 100 generated images and use five response categories from confidently AI-generated to confidently real, with intermediate uncertainty/appearance anchors. Five different annotators evaluate each sample. The appendix describes the protocol as using HYPE∞, but the recorded response is a five-category judgment rather than a simple binary response.

Real MS-COCO images average 4.48/5, while none of the tested models averages above 3. This is an aggregate result from the 2023 comparison, not a claim about every image or current systems.

The source also computes FID with 30,000 MS-COCO prompt–image pairs resized to 512×512. FID measures feature-distribution similarity to reference photographs; it is not a direct human judgment or prompt-conditioned image-level measure.

## Thesis implications

Use photorealism when realism is intended. For artistic modifier conditions, report it separately rather than treating a reduction as universal quality loss. HEIM’s Promptist comparison illustrates the distinction: aesthetic win rate improves while the table’s quality/photorealism win rate is much lower than unmodified SD1.4.

## Photographic style in REAL

[[REAL - Realism Evaluation of Text-to-Image Generation Models for Effective Data Augmentation]] fine-tunes CLIP to classify photo versus illustration and combines this style score with attribute correctness for augmentation filtering. Photographic appearance is only one component: [[Fine-grained visual correctness]] and realistic relations can fail even when an image looks photographic. The real-photo/generated-illustration training setup may confound image origin with style; generalization requires validation. See [[Schema-based realism evaluation]].

## Related pages

- [[Human evaluation of generated images]]
- [[Style modifiers]]
- [[Holistic text-to-image evaluation]]
