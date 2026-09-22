# Anatomical defect evaluation

Source: [[Evaluating Text-to-Image Generative Models - An Empirical Study on Human Image Synthesis]], §§3.3–3.4, §5.2, Appendix §3.

## Labels and data

The dataset contains 79,908 images, including 10,000 SDXL generations and real images from AISegment, CelebAMask-HQ, and DeepFashion. Generated samples receive professional annotations: face/body boxes and good, bad, or invisible labels for eye, nose, mouth, hair, cheek, hand, arm, foot, leg, and trunk. Real-image labels are derived from existing annotations or VQA, then manually refined.

Coarse face/body/whole labels are bad if any constituent is bad; invisible if all constituents are invisible; otherwise good. This makes large groups more likely to be labeled defective and must be retained when comparing rates.

## Evaluation

ViT classifiers predict component and face labels. The appendix specifies 2,000 generated images for testing and the rest for training. Reported average component accuracy is 88%; face accuracy is 86%. Additional face tests on SD1.5/SD2.1/SDXL/Midjourney give 85.0%/84.3%/87.2%/86.3% accuracy.

Predicted face defect rates are 86%/79%/61%/29% in that same model order. They are classifier outputs, not directly observed population prevalence. Detection/pose confidence and FID/IS fail to reliably identify local defects in the authors’ diagnostic experiments.

## Limits and adaptation

Borderline defects have subjective labels; dramatic expressions, extreme lighting, and subtle eye details produce errors. The paper does not fully specify the visible-component denominator for every reported rate. For thesis use, define denominators, document visibility, validate precision/recall by component and condition, and check transfer beyond SDXL-generated training data. Report [[Anatomical realism]] separately from concept presence; the source’s strict human coverage combines them.

## Related schema-based realism checks

[[REAL - Realism Evaluation of Text-to-Image Generation Models for Effective Data Augmentation]] evaluates fine-grained class traits and entity/relation realism using VQA, rather than dedicated human-component classifiers. Both approaches distinguish visibility from correctness, but REAL’s attribute ratio excludes invisible parts from the denominator. See [[Schema-based realism evaluation]] and [[Fine-grained visual correctness]] for that coverage limitation.

## Related pages

- [[VQA-based concept coverage]]
- [[Human evaluation of generated images]]
- [[Aesthetic quality]]
