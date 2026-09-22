# VQA-based concept coverage

Source: [[Evaluating Text-to-Image Generative Models - An Empirical Study on Human Image Synthesis]], §§4.1–4.2, §5.3, Appendix §4 and Tables 10, 12–14.

The method estimates how frequently a generator depicts one target concept across repeated generations. It evaluates concept success, not the number of distinct concepts or general image diversity.

## Closed and open questions

For $n$ images targeting concept $c$, closed coverage asks a BLIP-based VQA model whether the action is present:

$\mathrm{cov}_{closed}=\frac{1}{n}\sum_{i=1}^n \mathbf{1}[a_i=\mathrm{yes}]$.

Open coverage instead asks what action is occurring, samples multiple answers per image, and clusters semantically equivalent answers. ChatGPT checks equivalence through bidirectional entailment. The largest cluster provides the final answer; cluster entropy expresses answer uncertainty:

$\mathrm{cov}_{open}=\frac{1}{n}\sum_{i=1}^n \mathbf{1}[H_i\leq\delta\;\land\;\mathrm{sem\_eq}(a_i,c)]$.

The study uses $\delta=0.8$. A lower threshold demands more consistent answers. Exact answer-sampling count and evaluator versions are not adequately specified in the text. Fix these settings and the entropy convention before attempting reproduction.

## Validation and results

Thirty concepts (10 actions, 20 interactions) receive 500 images each for SD1.5, SD2.1, and SDXL. Human loose judgments ask whether the concept is present; strict judgments additionally require no human defects.

| Concept-level Spearman correlation | SD1.5 | SD2.1 | SDXL |
| --- | --- | --- | --- |
| Closed coverage versus human loose | 0.61 | 0.71 | 0.48 |
| Thresholded CLIP versus human loose | 0.12 | 0.19 | 0.17 |
| Open coverage versus human strict | 0.51 | 0.58 | 0.69 |
| Thresholded CLIP versus human strict | 0.32 | 0.24 | 0.27 |

The CLIP baseline uses threshold 0.2. These comparisons concern this thresholded implementation, not every possible use of CLIP. Overall VQA action-classification accuracy is reported as 95.9% closed and 96.0% open.

Table 5 open-coverage means disagree with arithmetic means of the 30 appendix rows: SDXL 86.50% reported versus 81.83% recomputed; SD2.1 76.27% versus 74.49%; SD1.5 77.19% versus 75.85%. Closed means reproduce correctly. The reason for the discrepancy is unresolved.

## Use and limits

The approach offers an interpretable complement to [[CLIP-based alignment evaluation]]. However, answer consistency is not proof of truth, and open coverage does not explicitly inspect anatomical defects. Its agreement with strict judgments does not make it a pure [[Prompt alignment]] measure or a substitute for [[Anatomical defect evaluation]]. The source tests one target concept at a time; multi-concept relationships require additional validation.

For modifier experiments, fix the original target concept across conditions and report concept presence and defect freedom separately. Human calibration and sensitivity to question wording remain necessary.

## Related pages

- [[Human evaluation of generated images]]
- [[Prompt modifiers]]
- [[Demographic diversity and bias]]
