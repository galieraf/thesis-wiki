# Human preference in image generation

Human preference is a comparative judgment about which generated image a person wants or likes more in a given context. It may combine aesthetics, prompt fulfillment, style, personal intent, and other considerations. A general preference label does not reveal the contribution of each dimension.

## Evidence from Pick-a-Pic

[[Pick-a-Pic - An Open Dataset of User Preferences for Text-to-Image Generation]] (§§2–4) collects a prompt author’s choice between two images, including ties. Unlike external annotators, the author may know intentions not expressed fully in the text. Experts predict original user choices at 68.0% under the paper’s tie-aware metric, while PickScore reaches 70.5%. This supports distinguishing prompt-author preference from external judgments; it does not establish universal superiority of learned taste.

The interaction retains the preferred image and replaces the rejected one, producing repeated comparisons linked by user, prompt, and image. Authentication, monitoring, and filtering reduce some misuse but do not eliminate biased or inattentive labels. Prompt-disjoint testing does not ensure user-disjoint evaluation.

## Relation to other wiki outcomes

[[Pairwise aesthetic preference ranking]] asks specifically about aesthetic appeal of image sets. Pick-a-Pic asks for general preference between individual images. [[Aesthetic quality]], [[Prompt alignment]], [[Anatomical realism]], and [[Demographic diversity and bias]] remain separate constructs even when they influence a choice.

## Thesis use

Specify whose preference is measured, the question asked, the compared unit, tie handling, and the intended population. If modifier experiments use external raters, describe this as external preference rather than access to the prompt author’s full intent. Record independent alignment and diversity outcomes instead of inferring them from preference gains.

## Related pages

- [[Human evaluation of generated images]]
- [[PickScore preference prediction]]
- [[Best-of-N image selection]]
