# Style modifiers

A style modifier is prompt text that specifies how a subject should be visually represented, such as a medium, art movement, rendering style, or aesthetic. In the source paper, the STYLE slot in `SUBJECT in the style of STYLE` acts as this modifier.

## Evidence in this wiki

[[Design Guidelines for Prompt Engineering Text-to-Image Generative Models]] (§6) tests 51 styles in VQGAN+CLIP. Successful generations evoke palettes, textures, line/stroke patterns, lighting, spatial organization, and distinctive motifs. Figurative styles receive higher mean style ratings than abstract styles in the evaluated set (3.16 versus 2.63).

Failures include ambiguous names (mola interpreted as a fish rather than an art form), incomplete stylistic representation, mismatched photorealistic details, text appearing in the image, and repetitive default motifs. A successful visual imitation does not demonstrate faithful representation of cultural meaning.

## Scope and thesis use

Style fidelity should be distinguished from subject alignment and overall preference: Experiment 4 explicitly asks annotators to ignore subject quality. The paper does not test generic quality/realism modifiers such as `4k` or `2048px`; it identifies them as future work (§8.2).

A useful thesis question is whether modifiers improve style representation while weakening the requested subject. This is an implication to test, rather than an effect measured with separate alignment scores in the paper.

## Related evidence on broader modifiers

[[Best Prompts for Text-to-Image Models and How to Find Them]] evaluates combinations of style, lighting, detail, and other [[Prompt modifiers]] in Stable Diffusion v1.4. Its optimized combination ranks above a popular-keyword baseline in aesthetic preference, but the experiment does not isolate style fidelity or individual modifier effects. See [[Aesthetic quality]].

## Taxonomy and overlapping functions

[[A taxonomy of prompt modifiers for text-to-image generation]] places style modifiers among six categories and explicitly notes overlap with [[Quality boosters]]. Artist names, for example, may be used for perceived finish or detail as well as style. Annotate the intended role in context instead of inferring a single role from the phrase alone.

## Related pages

- [[Prompt engineering]]
- [[Subject-style interaction]]
- [[Human evaluation of generated images]]
