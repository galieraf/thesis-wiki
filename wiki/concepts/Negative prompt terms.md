# Negative prompt terms

Negative terms specify concepts a user wants a supported generation system to avoid. Their implementation and syntax depend on the model/interface; they should not be treated as universally reliable logical negation.

## Evidence in this wiki

[[Prompting AI Art]] (§5) offers an optional negative-term field during one revision round. Nineteen of 50 participants provide 39 entries, targeting subjects, style, text, or watermarks. Some edits succeed and others fail, including cases where positive and negative inputs conflict. The study does not isolate negative conditioning from simultaneous changes to the main prompt.

[[A taxonomy of prompt modifiers for text-to-image generation]] (§5) discusses negatively weighted terms as an exclusion operation and positively weighted terms for mixing. Weighting is not a seventh modifier category in that taxonomy. A separate negative-prompt field and a signed weight are related interface strategies, not necessarily identical mechanisms.

## Thesis use

Record negative inputs independently from positive modifiers. Test exclusion success, collateral changes, aesthetics, and alignment with an otherwise fixed prompt and sampling procedure. These are proposed controls rather than an evaluation completed by the cited papers.

## Related pages

- [[Prompt modifiers]]
- [[Prompt alignment]]
- [[Evaluation of prompt revision]]
