# econ3916-lab18-model-evaluation
# Model Evaluation: The Curve, and What It Cannot Tell You

## Objective
I used simulated rare-outcome data to show what ROC and precision-recall curves reveal and hide, why one AUC cannot rank two models, and how stated costs turn an evaluation into a decision.

## Methodology
- Simulated 8,000 cases of a rare outcome, and found that 11.8% of the test rows were positive.
- Drew a ROC curve and a precision-recall curve for a logistic regression: ROC AUC 0.8468 and average precision 0.4651.
- Compared it with a boosted-tree model (ROC AUC 0.8431), and put a 95% interval on the AUC difference with a paired bootstrap over 500 resamples of the test rows.
- Built an expected-cost curve with a miss costing ten times a false alarm, chose the cheapest threshold on the training rows, and priced it once on the test rows.
- Swept the cost ratio from 2:1 to 50:1 for both models, choosing each threshold the same way, and checked whether the cheaper model changes.

## Key Findings
- The AUC difference on the full test set was +0.0038, and its 95% interval over 500 resamples was -0.0020 to +0.0094, so the two models cannot be told apart by AUC.
- The cheapest threshold on the training rows was 0.0905. On the test rows it cost 0.4692 per case, against 0.9437 at the default 0.5.
- The logistic model was the cheaper one at most of the cost ratios and the boosted model at only one, but the gaps are small and I did not put intervals on them.
