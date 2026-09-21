# Image prompts and initial images

[[A taxonomy of prompt modifiers for text-to-image generation]] (§§4–5) distinguishes two visual-input roles:

- **Image prompt:** a reference providing a target subject or style, potentially through multiple images.
- **Initial image:** an image supplying the starting state to be transformed during generation.

In the systems discussed, image prompts can convey both subject and style and may reinforce or vary textual instructions. The author describes one initial image versus potentially several image prompts. This is a description of those workflows, not a universal limitation of image-conditioned generation.

The taxonomy includes image prompts among its six modifier types; initial images are additional resources in the iterative workflow rather than a seventh taxonomy category. This is broader than the common use of “modifier” to mean only text appended to a description.

## Thesis use

Record reference-image conditioning separately from text changes and generation initialization. Otherwise an apparent modifier effect may come from the visual input. The paper does not provide a controlled comparison of these conditioning routes.

## Related pages

- [[Prompt modifiers]]
- [[Style modifiers]]
- [[Prompt alignment]]
