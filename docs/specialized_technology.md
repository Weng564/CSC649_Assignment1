# Part C: Specialized Technology Brief — Supervised Machine Learning

## C1. Fundamental Concepts

Supervised machine learning is a branch of AI where algorithms learn from labeled training data. The model is given input features ($X$) along with the correct labels ($Y$), and it picks up the patterns that connect them, so it can make accurate predictions on data it hasn’t seen before.

For Pinterest content deduplication, the system works with tabular feature vectors built from image processing and account behavior. It looks at inputs such as the perceptual hash Hamming distance ($X_1$), text similarity ($X_2$), and account age ($X_3$), and uses them to sort each upload into one of three classes:

$$Y \in \{\text{Original}, \text{Near-Duplicate}, \text{Exact Duplicate}\}$$

```
+------------------------+       +-------------------------+       +------------------------+
| Input Features (X)     |       | Decision Tree Engine    |       | Predicted Target (Y)   |
| • Perceptual Hash Dist | ----> | • Split: Hash Dist <= 5 | ----> | [Exact Duplicate]      |
| • Title Cosine Sim     |       | • Split: Text Sim > 0.8 |       | [Near-Duplicate]       |
| • Account Age (Days)   |       | • Gini Impurity Check   |       | [Original]             |
+------------------------+       +-------------------------+       +------------------------+
```

### Worked Classification Example

A new Pin comes in for evaluation.

1. **Feature extraction**
   - Perceptual hash Hamming distance: 3 (scale 0–64; low means nearly identical images)
   - Title similarity: 0.88 (cosine similarity)
   - Aspect ratio difference: 0.00
2. **Decision tree walk-through**
   - Hamming distance ≤ 5? Yes → go to the right branch.
   - Title similarity > 0.85? Yes → leaf node reached.
3. **Prediction:** Exact Duplicate. The system triggers FR3 to suppress the Pin from public indexing.

---

## C2. Frameworks, Models, Methods, and Tools

**Decision Tree Classifier (scikit-learn):** A supervised method that splits data on feature thresholds to separate classes as cleanly as possible. It's the main inference engine because it's fast and easy to interpret.
2. **Perceptual Hashing (ImageHash):** Turns an image into a short binary string. Unlike cryptographic hashes such as MD5, similar-looking images get similar hashes, so they can be compared by simple numerical distance.
3. **scikit-learn (Python):** An open-source machine learning library we use for splitting data, scaling features, training, tuning, and evaluating the model (precision, recall, F1-score).

---

## C3. Fit to Problem, Limitations, and Alternative Analysis

### Addressing the problem

Duplicate Pins are currently caught mostly through slow, manual user reports. A supervised model classifies each Pin automatically in well under a second, so the platform can handle millions of daily uploads and separate genuine creative variations from automated spam re-posts.

### Limitations and risks

1. **Adversarial evasion:** Spammers can add noise, borders, rotations, or color inversions to raise the hash distance, causing duplicates to be labeled `Original` (false negatives).
2. **Dataset bias and label noise:** Training needs thousands of hand-labeled Pin pairs. If annotators mislabel legitimate remixes as spam, the model will unfairly penalize creators.

### Comparison with an alternative approach

| Criteria | Chosen: Supervised Decision Tree | Alternative: Rule-Based Thresholds |
| :--- | :--- | :--- |
| **How it works** | Multi-feature tree learned from data | Fixed IF-THEN rules (e.g., IF hash distance = 0) |
| **Adaptability** | High; retrains as spam patterns change | Low; breaks when spammers crop slightly differently |
| **Inference speed** | Very fast (< 5 ms) | Faster (< 1 ms) |
| **Why chosen** | Static rules can't weigh interactions between signals; a decision tree can. | |
---

## References

* Beskow, D. M., & Carley, K. M. (2022). *Dataset and case studies for visual near-duplicates detection in social media*. arXiv. https://arxiv.org/html/2203.07167
* Buchner, J. (n.d.). *ImageHash: A Python perceptual image hashing library* [Computer software]. GitHub. https://github.com/JohannesBuchner/imagehash
* Kislyuk, D. (2016, June 28). *Introducing automatic object detection to visual search*. Pinterest Engineering. https://medium.com/pinterest-engineering/introducing-automatic-object-detection-to-visual-search-e57c29191c30
* scikit-learn developers. (n.d.-a). *1.10. Decision trees*. Scikit-learn Documentation. https://scikit-learn.org/stable/modules/tree.html
* scikit-learn developers. (n.d.-b). *sklearn.tree.DecisionTreeClassifier*. Scikit-learn Documentation. https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html
