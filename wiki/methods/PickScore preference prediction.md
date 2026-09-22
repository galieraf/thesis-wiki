# PickScore preference prediction

Source: [[Pick-a-Pic - An Open Dataset of User Preferences for Text-to-Image Generation]], §§3–5 and appendix “Training a Scoring Function.”

PickScore fine-tunes CLIP-H to predict prompt-conditioned [[Human preference in image generation]]. It is not an unmodified CLIP similarity metric or a dedicated aesthetic predictor.

## Scoring and training

For prompt $x$ and image $y$, the paper defines $s(x,y)=E_{txt}(x)\cdot E_{img}(y)\cdot T$, where $T$ is CLIP’s learned scalar temperature parameter. Pairwise probabilities are $\hat p_i=\exp(s(x,y_i))/\sum_{j=1}^2\exp(s(x,y_j))$.

Training targets are $(1,0)$ or $(0,1)$ for a winner and $(0.5,0.5)$ for a tie. The loss is $D_{KL}(p\Vert\hat p)$, averaged using inverse prompt-frequency weights so frequently repeated prompts do not dominate. Adding in-batch negatives reduces reported test accuracy to 65.2 versus 70.5 for the main objective.

The experiment uses 583,747 training comparisons; validation and test contain 500 each with disjoint prompts. Checkpoint selection uses validation accuracy without ties; automatic tie thresholds are subsequently selected on validation data. These are separate selection steps.

## Tie-aware evaluation

Predict a tie when $|\hat p_1-\hat p_2|<t$, with $t$ selected separately for each scoring model. Accuracy gives 1 for agreement, 0.5 if exactly one label is a tie, and 0 for opposing winners. Thus the reported random baseline is 56.8%, not a conventional 50% binary baseline.

PickScore achieves 70.5%, compared with 68.0% for external experts, 66.7% for HPS, 61.1% for ImageReward, 60.8% for CLIP-H, and 56.8% for the aesthetic predictor. The reported $\pm0.142$ over three seeds is described as variance in the source footnote, not an established confidence interval.

## Aggregate generator evaluation

On roughly 14,000 comparisons for test prompts and 45 backbone–guidance configurations, PickScore/user Elo rankings have Spearman correlation $0.790\pm0.054$. The spread comes from 50 shuffled comparison orders. On nine configurations with 100 MS-COCO captions, its win-ratio correlation with expert rankings is 0.917 versus −0.900 for FID-derived rankings. Neither result is per-image agreement or a guarantee for other models.

## Use and limits

The learned score mixes preference considerations and sometimes sacrifices faithfulness for aesthetic appeal. Raw scores are not calibrated absolute image quality; pairwise probabilities depend on the candidate pair. State the checkpoint, scoring reference, tie rule, and aggregation procedure. In a modifier experiment, score against the original request when evaluating preservation of intent and validate on independent human judgments.

## Related pages

- [[CLIP-based alignment evaluation]]
- [[Aesthetic quality]]
- [[Prompt alignment]]
- [[Best-of-N image selection]]
