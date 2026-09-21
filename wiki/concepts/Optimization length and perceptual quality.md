# Optimization length and perceptual quality

Optimization length is the number of update steps used to generate an image in an iterative procedure. Better optimization of a model objective does not necessarily mean greater human preference for the resulting image.

## Evidence in this wiki

[[Design Guidelines for Prompt Engineering Text-to-Image Generative Models]] (§5) evaluates 72 VQGAN+CLIP trajectories: six subjects crossed with 12 styles, using a constant seed. Annotators choose a preferred image among checkpoints at 100, 200, …, 1,000 steps.

Preferences differ significantly across checkpoints ($p=0.01$); 200, 100, and 500 steps are the most frequently preferred. Agreement is fair ($\kappa=0.33$). The authors propose 100–500 steps for fast exploration and 300 as a default, noting that at 100 steps a subject may not yet have emerged.

## Interpretation and limits

This supports separating human preference from assumptions about longer optimization. It does not provide a measured correlation between an automated loss curve and human ratings. Early soft or abstract images can be preferred even when content is not yet recognizable.

The numerical step recommendations belong to this VQGAN+CLIP configuration. They cannot be directly transferred to diffusion sampling steps or another model’s optimization schedule.

## Related pages

- [[Prompt engineering]]
- [[Human evaluation of generated images]]
