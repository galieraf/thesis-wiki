# Prompt alignment

Prompt alignment concerns whether a generated image expresses the requested content or intent. It can have multiple dimensions: depicted objects and context, requested style, or intended emotion. These should not be collapsed automatically into [[Aesthetic quality]].

## Evidence in this wiki

[[RePrompt]] (§§5–6) distinguishes image–text alignment (ITA), concerning the original situation, from image–emotion alignment (IEA), concerning the target emotion label. RePrompt improves computational emotion alignment while reducing computational original-text alignment relative to the unedited baseline. Human ITA ratings instead improve, leaving context-preservation evidence mixed.

[[Design Guidelines for Prompt Engineering Text-to-Image Generative Models]] separately evaluates style fidelity and, in another experiment, joint subject–style representation. Its failure cases show that a recognizable style can coexist with a missing subject. [[Best Prompts for Text-to-Image Models and How to Find Them]] measures aesthetic preference and does not separately establish alignment gains.

## Use in the thesis

Specify which reference is being used: the original user request, the edited prompt, an emotion label, or a style. Scoring against an edited prompt alone can miss loss of original intent. Evaluate distinct dimensions separately and check automated judgments against human perception.

## Single-concept coverage in Chen et al. (2024)

[[Evaluating Text-to-Image Generative Models - An Empirical Study on Human Image Synthesis]] estimates concept success across 500 generations per concept using [[VQA-based concept coverage]]. Closed questions correspond more closely to loose human concept judgments than the tested thresholded CLIP baseline. Open questions add answer-consistency filtering and correlate with strict human judgments, but those judgments also require defect-free humans. Thus strict coverage mixes alignment with [[Anatomical realism]] and does not establish full compositional prompt fulfillment.

## Preference does not guarantee faithfulness

[[Pick-a-Pic - An Open Dataset of User Preferences for Text-to-Image Generation]] reports that PickScore sometimes chooses more aesthetically pleasing images at the cost of faithfulness. Its ranking experiment’s CLIP-based alignment checks remain automatic proxies. Use [[PickScore preference prediction]] as a preference outcome alongside explicit alignment measurements, rather than treating higher preference as proof of preserved intent.

## Broad alignment and compositional reasoning in HEIM

[[Holistic Evaluation of Text-to-Image Models]] uses five-point human alignment judgments across general, knowledge, and reasoning scenarios, alongside CLIPScore and diagnostic object detection. The best PaintSkills detection result is 47.2%, illustrating why strong general alignment does not guarantee correct counts or relations. [[Prompt perturbation evaluation]] separately checks changes across wording, demographic terms, and translations.

## Related pages

- [[Emotional expression in generated images]]
- [[CLIP-based alignment evaluation]]
- [[Human evaluation of generated images]]
- [[Subject-style interaction]]
