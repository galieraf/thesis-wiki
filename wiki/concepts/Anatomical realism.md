# Anatomical realism

Anatomical realism concerns whether depicted human parts and their arrangement appear plausible, including faces, hands, limbs, and torso. It is distinct from [[Aesthetic quality]] and [[Prompt alignment]]: an appealing image can contain extra fingers, and a recognizable action can contain malformed anatomy.

## Evidence

[[Evaluating Text-to-Image Generative Models - An Empirical Study on Human Image Synthesis]] (§§3.3–3.4) labels ten components as good, bad, or invisible and combines them into face, body, and whole-person labels. Its trained evaluators predict lower facial defect rates for newer tested SD models, but hand defects remain frequent. These are task- and evaluator-dependent estimates; see [[Anatomical defect evaluation]].

## Thesis implications

Keep invisibility separate from correct anatomy. Modifier conditions that hide hands or use close framing can alter what is assessable. Report visibility and the scoring denominator alongside defect rates. Define what counts as an unintended defect for stylized images rather than assuming photorealistic anatomy is always the artistic goal. These are proposed evaluation safeguards, not tested modifier effects in the source.

## Related pages

- [[Human evaluation of generated images]]
- [[VQA-based concept coverage]]
