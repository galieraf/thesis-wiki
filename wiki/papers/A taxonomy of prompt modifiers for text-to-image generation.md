# A taxonomy of prompt modifiers for text-to-image generation

**Authors:** Jonas Oppenlaender  
**Year:** 2024 (journal issue); first published online 28 November 2023  
**Source:** [[raw/papers/A taxonomy of prompt modifiers for text-to-image generation.pdf]]; Behaviour & Information Technology, 43(15), 3763–3776. DOI: [10.1080/0144929X.2023.2286532](https://doi.org/10.1080/0144929X.2023.2286532)  
**Last updated:** 2026-09-21

## Research question

What types of prompt modifiers do text-to-image practitioners use, and how are they applied in iterative prompt engineering? The goal is to organize community practice into a conceptual taxonomy for HCI research, rather than rank modifiers by experimentally measured effectiveness.

## Motivation

Prompt-writing knowledge is often tacit, scattered across community resources, and learned through trial and error. Some practitioners do not disclose complete prompts. A common vocabulary can structure research on this practice and support learning and interface design (§§1–2).

## Method

The author combines autoethnographic experimentation, online community ethnography, and review of mainly gray literature (§3).

- **Personal practice:** three months, October–December 2021; on average at least one free-tier Google Colab session per workday from October 4 to December 31, with roughly two hours available per day depending on resources. The author generated 885 images with VQGAN–CLIP.
- **Community observation:** participant-as-observer on Twitter, following hashtags, engaging in discussions, and posting generated images. Shared prompts and exchanges informed the experimentation.
- **Resource review:** community guides, documents, blog posts, articles, and experiment reports, alongside emerging scholarly work.
- **Inductive analysis:** compile and group candidate modifiers; revisit categories when encountering new instances; document examples and interpretations in a PowerPoint presentation; perform a final review of completeness and consistency. The author reports that the categories stopped expanding after some weeks.

The author discloses a computer-science background focused on HCI/social computing and does not identify as an artist. The paper does not report an independent coding team, inter-coder reliability, or a controlled quantitative validation of the taxonomy. See [[Ethnographic analysis of prompt modifiers]].

## Datasets

- 885 images created during the author’s autoethnographic practice.
- Twitter posts and discussions from practitioners who shared prompts; the paper describes this material as sparse and does not report a full corpus size or sampling frame.
- Community resources and literature used to refine categories; no fixed benchmark dataset or train/test split.

The main fieldwork is dated to 2021, while the published article also discusses later systems and sources. Treat the study period and later contextual discussion as distinct.

## Models

**Primary hands-on system:** Crowson and collaborators’ VQGAN–CLIP notebook, run on Google Colab. Accessibility, memory requirements, community adoption, and reproducibility motivated its selection (§3.1).

Figure 3 specifies one illustrative sequence: 175 iterations, CLIP ViT-B/32, VQGAN `wikiart_16384`, and seed `6087304447281500163`. These are example-specific settings, not documented settings for all 885 images.

Figures also show Midjourney and DALL-E 2 examples; Figure 2 uses DISCO Diffusion. These examples and discussion of other models do not constitute a comparative benchmark. Weight syntax and image-prompt behavior described in the paper belong to the systems discussed, not a universal interface contract.

## Metrics

No quantitative image-quality, diversity, prompt-alignment, or aesthetic-preference metric is reported for validating the taxonomy. There are no effect sizes or significance tests comparing modifier categories. The 885-image count describes research activity, not evidence of an average improvement.

The author treats the stabilization of categories as evidence of completeness within the observed material. This is qualitative saturation claimed by the author, not proof of exhaustive coverage across models and communities.

## Main findings

The published taxonomy contains **six categories** (§4, Table 1):

| Category | Intended function | Examples or form |
| --- | --- | --- |
| Subject terms | Specify what should be depicted | A landscape; an old car in a meadow |
| Style modifiers | Specify an artistic style, medium, technique, or artist-associated appearance | Oil painting; pixel art; Cubism |
| Image prompts | Supply a visual subject or style target | One or several reference images, provided through URLs or another supported input |
| Quality boosters | Request improved perceived quality or detail | Highly detailed; award-winning; trending on artstation |
| Repeating terms | Reinforce a subject or style by repetition or rephrasing | Repeating the same subject using a different word order |
| Magic terms | Introduce semantically distant or nonvisual ideas to encourage surprise | Control the soul; feel the sound |

**Functions overlap.** An artist name may be used as both a style cue and a quality booster. Image prompts can convey subject and style together. The categories concern practitioner intentions and are not mutually exclusive causal mechanisms.

**Image prompts and initial images differ in the paper’s account.** Image prompts serve as visual targets; an initial image supplies a starting state for generation. The author describes multiple image prompts versus a single initial image for the discussed systems. This distinction should not be turned into a claim about all present-day implementations.

**Iterative practice has five purposes** (§5, Table 2): define, modify, solidify, vary, and mix/exclude. Subject specification anchors controlled generation; additional style/detail cues, repetition, and unusual terms are optional. Weights can mix or exclude concepts in supported systems. Weighting and initial images are discussed as operations/resources, not additional categories in the six-part taxonomy.

**Effectiveness claims remain qualitative.** The paper describes quality boosters as potentially increasing detail, verbosity as potentially reducing subject control, repetition as reinforcing concepts, and magic terms as encouraging variation. These observations and examples do not quantify benefit, reliability, or diversity preservation.

**Research implications:** investigate community learning, practitioner beliefs, co-creation workflows, bias, computational aesthetics, and human–AI interaction (§6). The paper explicitly notes that some practitioner choices may be folk theories rather than established causal knowledge.

## Limitations

- One researcher’s experience, sparse voluntarily shared prompts, and Twitter-centered observation may omit private practices and other communities.
- The method supports a conceptual account of use, not causal claims that a phrase improves quality or increases diversity.
- Categories can overlap, so applying the taxonomy requires documenting intended function and ambiguity rather than assuming one category per phrase.
- Fieldwork reflects early text-to-image practice. Transfer to later generators, negative-prompt interfaces, or different multimodal workflows needs testing.
- Example-specific generation settings do not define a standardized evaluation protocol for the corpus.
- The article’s mechanistic explanations of repetition and latent activation are not experimentally isolated here; they should not be cited as proven mechanisms across architectures.
- This published version lists six types. [[RePrompt]] refers to an earlier Oppenlaender work with five types; do not conflate that earlier description with this version.

## Relevance to my thesis

The taxonomy supplies a grounded vocabulary for organizing [[Prompt modifiers]] before measuring their effects on quality, diversity, and [[Prompt alignment]]. It complements the controlled experiments in [[Design Guidelines for Prompt Engineering Text-to-Image Generative Models]] and the keyword-set optimization in [[Best Prompts for Text-to-Image Models and How to Find Them]].

**Proposed thesis use:** code candidate modifiers by intended function, allow overlapping labels, separate image inputs from textual interventions, and test each category across subjects and seeds. Treat claimed quality improvement and variation as hypotheses requiring separate measures. In particular, “magic terms” motivate a diversity experiment but do not themselves establish a diversity metric or improvement.

## Related empirical study of modifier knowledge

[[Prompting AI Art]] examines whether crowd participants recognize, write, and revise prompts, finding sparse spontaneous use of specialist modifiers. The attached version is the 2025 journal article (online 2024), whereas this taxonomy’s bibliography cites its earlier 2023 preprint. The studies provide complementary evidence about practice and skill, not a direct test of all six categories.

## Related pages

- [[Prompt modifiers]]
- [[Style modifiers]]
- [[Quality boosters]]
- [[Repeating and magic terms]]
- [[Image prompts and initial images]]
- [[Ethnographic analysis of prompt modifiers]]
- [[RePrompt]]
