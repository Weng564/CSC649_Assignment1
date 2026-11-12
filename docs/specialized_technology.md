# Part C: Specialized Technology Brief — Supervised Machine Learning

## C1. Fundamental Concepts

Supervised machine learning trains a model on examples that already have the right answers attached. The model learns the link between input features ($X$) and labels ($Y$), then predicts labels for new data.

For Pinterest deduplication, the inputs are Hamming distance between perceptual hashes ($X_1$), title text similarity ($X_2$), and account age ($X_3$). The model sorts each upload into one of three classes:

$$Y \in \{\text{Original}, \text{Near-Duplicate}, \text{Exact Duplicate}\}$$

### Worked Example
A new Pin has a hash distance of `3` and a title similarity of `0.88`:
* Hash distance $\le 5$? **Yes.**
* Title similarity $> 0.85$? **Yes.**
* **Prediction:** `Exact Duplicate`, so **FR3** hides it from search.

---

## C2. Tools and Methods

1. **Decision Tree Classifier (`scikit-learn`):** Learns simple if-then splits from labeled data. It’s fast and easy to explain (scikit-learn developers, 2026).
2. **Perceptual Hashing (`ImageHash`):** Turns an image into a short fingerprint that stays similar for similar-looking images. Cryptographic hashes like SHA-256 can’t do this (Buchner, 2021; MojoAuth, 2026).

---

## C3. Fit, Limitations, and Alternative

### Fit
The classifier replaces slow manual reporting with automatic checks that take milliseconds. That lets the platform screen millions of uploads a day.

### Limitations
* **Evasion:** Heavy cropping, rotation, or noise can fool perceptual hashes (MojoAuth, 2026; Struppek et al., 2021).
* **Bad labels:** If annotators mislabel creative remixes as spam, the model will unfairly penalize genuine creators.

### Alternative
Fixed rule-based thresholds are slightly faster, but they break when spammers tweak an image. A decision tree can weigh visual similarity together with account behavior, so I chose it.

---

## References

* Buchner, J. (n.d.). *ImageHash: A Python perceptual image hashing module* [Computer software]. GitHub. https://github.com/JohannesBuchner/imagehash
* MojoAuth. (n.d.). *pHash vs SHA-256: Perceptual hash explained*. https://mojoauth.com/security-guides/sha-256-vs-phash
* scikit-learn developers. (n.d.). *sklearn.tree.DecisionTreeClassifier*. https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html
* Struppek, L., Hintersdorf, D., Neider, D., & Kersting, K. (2021). *Learning to break deep perceptual hashing: The use case NeuralHash*. arXiv. https://arxiv.org/pdf/2111.06628
