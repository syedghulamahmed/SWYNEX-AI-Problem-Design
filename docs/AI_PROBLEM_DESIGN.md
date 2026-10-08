# AI Problem Design — Student Feedback Classification

## 1. Problem Statement
Internship and student-support programs receive many short feedback messages. These messages can be difficult to organize manually because they arrive as unstructured text and may require different responses.

The proposed AI problem is **multi-class text classification**: given a short student/internship feedback message, predict which category best describes its primary intent.

### Classification labels
1. **Positive Feedback** — praise, appreciation, or a report that something worked well.
2. **Negative Feedback** — dissatisfaction or a negative experience that does not primarily request action.
3. **Question** — a request for information or clarification.
4. **Suggestion** — an idea or recommendation for improvement.
5. **Complaint** — a specific grievance or problem requiring attention.

The classifier is a support tool for organizing feedback. It is not intended to make disciplinary, employment, academic, medical, or other high-stakes decisions.

## 2. Target User
The primary user is an **internship-program coordinator or student-support team**.

The user needs to:
- sort incoming feedback quickly;
- identify messages requiring attention;
- separate questions from general comments;
- identify recurring improvement suggestions; and
- reduce repetitive manual categorization.

## 3. Data Source
The initial dataset will be a small, manually labeled CSV dataset created specifically for this project.

Each record will contain:
| Field | Description |
|---|---|
| `text` | Short feedback message |
| `label` | Human-assigned category |

Illustrative examples:
| text | label |
|---|---|
| "The weekly mentoring sessions were very helpful." | Positive Feedback |
| "When will the next task be unlocked?" | Question |
| "It would be useful to receive a sample submission." | Suggestion |
| "The task instructions were difficult to understand." | Negative Feedback |
| "I submitted my work but the portal still shows it as pending." | Complaint |

These examples are illustrative. A real dataset should be labeled consistently according to the category definitions.

## 4. Data Requirements
Before training:
- remove duplicate records;
- remove unnecessary personal information;
- normalize obvious formatting problems;
- inspect class distribution;
- manually review ambiguous labels; and
- keep a separate held-out test set.

No personally identifying information is necessary for the classification task.

## 5. Constraints
### Technical
- Small dataset.
- Ordinary consumer hardware.
- No large language model required for the first version.
- Reproducible training and evaluation.

### Scope
- English short-form feedback.
- One primary label per message.
- Mixed-intent messages may be flagged for human review.
- Classification only; not automated response generation.

### Ethical
The system should not infer sensitive personal characteristics. Predictions should support human organization and review rather than replace responsible human judgment.

## 6. Proposed AI Approach
A suitable first implementation is:
1. text preprocessing;
2. TF-IDF feature extraction;
3. Logistic Regression or Linear SVM;
4. evaluation on held-out test data.

This approach fits a small dataset because it is inexpensive, interpretable, and effective for short text classification. A transformer-based model can be investigated if the dataset grows.

## 7. Baseline
The baseline will be a **majority-class classifier**, which always predicts the most frequent category.

The proposed model should outperform this baseline by a meaningful margin.

## 8. Evaluation Approach
The dataset will be split into training and held-out test data. Where the dataset permits, stratified splitting will be used.

Metrics:
- **Accuracy:** overall percentage of correct predictions.
- **Precision:** correctness of predictions for each category.
- **Recall:** coverage of messages belonging to each category.
- **Macro-F1:** equal-weight average across all categories.
- **Confusion matrix:** identifies categories that are frequently confused.

Macro-F1 is particularly important because it prevents a model from appearing strong merely by performing well on the most common class.

## 9. Success Criteria
| Criterion | Target |
|---|---:|
| Test accuracy | **≥ 85%** |
| Test macro-F1 | **≥ 0.80** |
| Comparison with baseline | **Meaningfully better** |
| Evaluation coverage | Precision, recall, F1, confusion matrix |

These are target thresholds, not claims about results before the model is trained.

If the targets are not reached, the result will be analyzed honestly and causes such as insufficient data, class imbalance, ambiguous labels, or overlapping categories will be documented.

## 10. Example User Flow
1. Coordinator receives a feedback message.
2. Message is passed to the classifier.
3. Classifier predicts a category and confidence score.
4. High-confidence predictions organize the feedback queue.
5. Low-confidence or ambiguous messages are flagged for human review.
6. Coordinator inspects the original message before taking action.

## 11. Risks and Limitations
### Ambiguous language
A message can contain multiple intents.

**Mitigation:** define a primary-label policy and flag uncertain predictions.

### Class imbalance
A model can appear accurate while performing poorly on rare categories.

**Mitigation:** report macro-F1 and per-class metrics.

### Dataset quality
Incorrect or inconsistent labels limit performance.

**Mitigation:** define labeling rules and review ambiguous examples.

### Distribution shift
Real feedback may differ from training examples.

**Mitigation:** periodically evaluate on newly collected representative samples.

### Overreliance on predictions
A classifier can make mistakes.

**Mitigation:** keep a human in the loop for ambiguous or consequential cases.

## 12. Future Monitoring
A future deployed version should monitor:
- macro-F1 over time;
- per-category recall;
- low-confidence prediction rate;
- class distribution changes; and
- human correction rate.

## 13. Future Improvements
- multilingual feedback classification;
- confidence-based routing;
- recurring-theme clustering;
- feedback summarization;
- dashboard-based trend analysis; and
- periodic human-reviewed retraining.

## 14. Final Problem Definition
**AI task:** Multi-class text classification.

**Input:** A short student/internship feedback message.

**Output:** One of five feedback categories plus a confidence estimate.

**Primary user:** Internship-program coordinator/student-support team.

**Data:** Small, anonymized, manually labeled feedback dataset.

**Primary constraints:** Small data, English short text, limited compute, human review for uncertainty, and avoidance of unnecessary personal data.

**Evaluation:** Accuracy, precision, recall, macro-F1, confusion matrix, and comparison against a majority-class baseline.

**Target:** At least 85% test accuracy and 0.80 macro-F1, while outperforming the baseline.

**Responsible-use principle:** The classifier organizes information; it does not replace human judgment for consequential decisions.
