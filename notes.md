**Community name:** r/artificial — https://www.reddit.com/r/artificial/

**Candidate distinctions:**
- Some posts link to news articles or research papers, while others make claims without sources.
- Some posts include detailed explanations and personal experiences, while others are short opinions or headlines.
- Some posts discuss AI benefits and breakthroughs, while others focus on risks, job losses, or industry disruption.
- Some posts include specific numbers or evidence, while others use broad or exaggerated claims.

## Initial Model Evaluation

The initial model achieved 70% accuracy on a held-out test set of 30 posts. However, its macro F1 score was approximately 0.275. The model predicted every test post as `personal_opinion`, resulting in an F1 score of 0 for both `sourced_information` and `unsupported_claim`.

These results show that overall accuracy alone does not adequately represent performance across all three labels. Further evaluation and improvement are needed before determining whether the model meets the project's acceptance criteria.

## Three Hard Cases

1. **A linked article with an opinionated headline:** The post links to an article but also uses language that expresses a strong opinion. I need to decide whether the main purpose is to report external information or express a personal take.

2. **A factual-sounding claim without a source:** The post states that an AI tool or technology has a particular effect, but provides no link or supporting evidence. I need to distinguish an unsupported claim from an ordinary opinion or prediction.

3. **A reaction to AI news:** The post responds to a recent AI announcement and includes both a factual reference and the author's judgment. I need to use the primary purpose of the post to make a consistent label decision.
## Baseline evaluation diagnostic

The initial evaluation used 30 held-out test posts. Accuracy was 0.70 and macro F1 was approximately 0.275. The model predicted personal_opinion for all 30 posts, correctly classifying 21 personal_opinion posts but missing all 5 sourced_information posts and all 4 unsupported_claim posts. The accuracy target was met, but the per-label F1 target was not met. These results indicate a strong prediction bias toward the majority class. The results are recorded honestly; labels and acceptance criteria were not changed to improve the scores.
