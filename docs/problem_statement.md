# Part A: Problem Formulation

## A1. Problem Statement

Visual discovery platforms like Pinterest have a copycat problem. Bots and commercial accounts routinely grab popular original artwork and infographics, tweak them just enough to look different (a slight crop, a color filter), and re-upload them with links pointing to their own ad-heavy sites. Picture an independent artist who shares a one-of-a-kind home decor design. Before long, hundreds of spam accounts have posted copies of it, and the original gets buried in search results.

The fallout is real. People searching for fresh ideas keep seeing the same image over and over. Creators lose the traffic and credit they’ve earned. And the platform pays to store countless near-identical files. A machine learning classifier that catches these duplicates before they reach the feed would go a long way toward fixing this.

```mermaid
flowchart LR
    %% Main Spine
    Sub1 --- Spine
    Sub2 --- Spine
    Sub3 --- Spine
    Spine ===> Effect["<b>EFFECT / PROBLEM</b><br/>High Feed Redundancy &<br/>Creator Traffic Theft on Pinterest"]
    Sub4 --- Spine
    Sub5 --- Spine
    Sub6 --- Spine

    %% Upper Causes
    subgraph Sub1["1. Information Presentation"]
        C1["• Duplicate images saturate feeds<br/>• Lack of original creator attribution<br/>• Fragmented pin provenance data"]
    end

    subgraph Sub2["2. Content Ingestion & Filtering"]
        C2["• Ineffective text-only search filters<br/>• Deeply buried reporting options<br/>• Delayed post-indexing removal"]
    end

    subgraph Sub3["3. System & Data Gaps"]
        C3["• Passive activity log storage<br/>• Lack of automated hash indexing<br/>• Unchecked bot re-uploading"]
    end

    %% Lower Causes
    subgraph Sub4["4. User & Creator Impact"]
        C4["• Loss of creator web traffic<br/>• High search friction for users<br/>• User churn due to repetitive feeds"]
    end

    subgraph Sub5["5. Malicious & Commercial Intent"]
        C5["• Affiliate URL hijacking<br/>• Automated image scraping bots<br/>• Mass spam campaign creation"]
    end

    subgraph Sub6["6. Algorithm & Technology"]
        C6["• Lack of supervised ML classifier<br/>• Absence of perceptual hashing<br/>• Static metadata rule cutoffs"]
    end

    %% Styling for clean B&W look
    classDef default fill:#ffffff,stroke:#000000,stroke-width:1px,color:#000000;
    classDef effect fill:#ffffff,stroke:#000000,stroke-width:2px,color:#000000;
    class Effect effect;
```

---

## A2. Users, Stakeholders, and Project Scope

### Target Users and Stakeholders
* **Everyday Pinterest users:** People hunting for inspiration, whether it’s recipes, home decor, or something else, who want varied results instead of the same pin repeated.
* **Content creators and artists:** Original publishers who need credit for their work and want the traffic to land on their own sites.
* **The Trust & Safety team:** The engineers who keep the catalog clean, fight spam, and keep storage costs under control.

### Project Scope

#### In-Scope:
* Pulling together tabular metadata and visual similarity signals, such as perceptual hash distance, aspect ratio, title similarity score, and account age.
* Using a Decision Tree Classifier to sort each new pin into one of three groups: Original, Near-Duplicate, or Exact Duplicate.
* Turning those labels into feed actions: let the pin through, flag it so it can be linked back to the creator, or keep it out of the index.
* Measuring how well the model works using Precision, Recall, and System Response Time.

#### Out-of-Scope:
* Detecting duplicates in video or animated GIFs.
* Generating DMCA takedown notices or handling copyright disputes.
* Building a browser extension from start to finish.
