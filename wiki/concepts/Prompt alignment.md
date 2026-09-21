# Prompt alignment

Prompt alignment concerns whether a generated image expresses the requested content or intent. It can have multiple dimensions: depicted objects and context, requested style, or intended emotion. These should not be collapsed automatically into [[Aesthetic quality]].

## Evidence in this wiki

[[RePrompt]] (§§5–6) distinguishes image–text alignment (ITA), concerning the original situation, from image–emotion alignment (IEA), concerning the target emotion label. RePrompt improves computational emotion alignment while reducing computational original-text alignment relative to the unedited baseline. Human ITA ratings instead improve, leaving context-preservation evidence mixed.

[[Design Guidelines for Prompt Engineering Text-to-Image Generative Models]] separately evaluates style fidelity and, in another experiment, joint subject–style representation. Its failure cases show that a recognizable style can coexist with a missing subject. [[Best Prompts for Text-to-Image Models and How to Find Them]] measures aesthetic preference and does not separately establish alignment gains.

## Use in the thesis

Specify which reference is being used: the original user request, the edited prompt, an emotion label, or a style. Scoring against an edited prompt alone can miss loss of original intent. Evaluate distinct dimensions separately and check automated judgments against human perception.

## Related pages

- [[Emotional expression in generated images]]
- [[CLIP-based alignment evaluation]]
- [[Human evaluation of generated images]]
- [[Subject-style interaction]]
