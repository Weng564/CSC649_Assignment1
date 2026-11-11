# Part B: Requirements

## B1. Functional Requirements (FRs)

| ID | Requirement | Testability Criterion |
| :--- | :--- | :--- |
| **FR1** | When someone uploads a new Pin, the system will compute its perceptual image hash and metadata similarity scores by comparing it against existing records. | Upload a sample image and check the processing log to confirm the feature vector was generated within 2 seconds. |
| **FR2** | The system will use a supervised Decision Tree Classifier to label each new Pin as Original, Near-Duplicate, or Exact Duplicate based on those similarity features. | Run validation feature sets through the model and confirm each one gets the correct label. |
| **FR3** | Pins labeled Exact Duplicate will be kept out of public search feeds. | Upload an identical copy of an existing image and confirm that search queries return no public impressions for it. |
| **FR4** | Pins labeled Near-Duplicate will show a provenance badge that links back to the original creator’s Pin. | Check the UI metadata for a flagged near-duplicate and confirm the link to the original creator is there. |
| **FR5** | If an account uploads more than 10 Near-Duplicate Pins within an hour, the system will send an alert to the Trust & Safety dashboard right away. | Simulate a bot uploading 11 slightly edited images and confirm an alert appears on the admin dashboard. |

---

## B2. Non-Functional Requirements (NFRs)

| ID | Category | Requirement | Target Metric |
| :--- | :--- | :--- | :--- |
| **NFR1** | **Performance** | Feature extraction and model prediction for a newly uploaded Pin will finish in 1.5 seconds or less. | Execution time $\le 1.5$ seconds |
| **NFR2** | **Accuracy** | When tested on validation data, the Decision Tree model will be right at least 90% of the time when it flags a Pin as duplicate content. | Precision $\ge 90\%$ |
| **NFR3** | **Scalability** | The backend feature evaluation service will handle 500 Pin classification requests at once without losing any. | Throughput $\ge 500$ req/sec (Error Rate $< 0.1\%$) |
