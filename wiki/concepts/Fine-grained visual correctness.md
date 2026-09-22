# Fine-grained visual correctness

Fine-grained visual correctness concerns whether depicted details match the intended class or entity: for example, a species’ tail pattern, feather color, or plant structure. An image may look photographic and depict the broad object category while getting diagnostic traits wrong.

## REAL operationalization

[[REAL - Realism Evaluation of Text-to-Image Generation Models for Effective Data Augmentation]] builds part/description schemas from Wikipedia with GPT-4 for iNaturalist and common binary class annotations for Birds. GPT-4o checks visible parts and their described appearances. [[Schema-based realism evaluation]] computes the fraction of visible attributes that match, with zero when no part is visible.

This extends evaluation beyond broad [[Prompt alignment]], but remains dependent on reference knowledge and class variation. Traits absent from the written prompt can still be implied by the named species. A class-level schema may not capture age, sex, seasonal, or individual variation; these are evaluation concerns to examine, not failures quantified by the source.

## Thesis implications

Separate [[Photorealism]] from factual detail and record visibility coverage. Camera/framing or detail modifiers may change which attributes can be judged, so a higher correctness ratio need not mean more correct information is shown. [[Anatomical realism]] concerns plausible structure; fine-grained correctness additionally asks whether the structure/appearance belongs to the intended entity.

## Related pages

- [[Prompt modifiers]]
- [[Realism-based data augmentation filtering]]
