# SWYNEX AI Problem Design

## Task 1 — Student Feedback Classification

This repository contains the AI problem design for Task 1 of the SWYNEX Technologies internship.

### Problem
Student and internship-program feedback often arrives as short, unstructured messages. Manually sorting every message into useful categories takes time and can produce inconsistent labeling.

The proposed AI system classifies a short feedback message into one of five categories:
- Positive Feedback
- Negative Feedback
- Question
- Suggestion
- Complaint

The system supports human review and organization; it does not make high-stakes decisions automatically.

### Target User
Internship-program coordinators or student-support teams who need to organize incoming feedback and identify messages requiring attention.

### Data Source
A small, manually labeled CSV dataset of anonymized student/internship feedback. Each record contains `text` and `label`.

### Constraints
- Small dataset and limited computing resources.
- English-language short text is the initial scope.
- Labels must be defined consistently.
- Ambiguous messages may require human review.
- The system should not infer sensitive personal attributes.
- Predictions are decision support, not unquestionable truth.

### Success Criteria
- Accuracy: at least 85%
- Macro-F1: at least 0.80
- Meaningfully better than a majority-class baseline
- Reasonably balanced precision and recall across categories

### Evaluation
Accuracy, precision, recall, macro-F1, and a confusion matrix will be reported on held-out test data.

### Deliverable
See [docs/AI_PROBLEM_DESIGN.md](docs/AI_PROBLEM_DESIGN.md) for the complete problem definition.

**Task:** SWYNEX Technologies — Task 1: AI Problem Design
