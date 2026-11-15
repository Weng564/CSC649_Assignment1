# CSC649_Assignment1
CSC649 Assignment 1: Pinterest Visual Content Duplicate and Re-pin Detection System using Decision Tree Classifier.

# Pinterest Visual Content Duplicate and Re-pin Detection System

> CSC649 Special Topics in Computer Science | Individual Assignment 1

**Summary:** This project studies how duplicate and near-duplicate image uploads degrade search discovery and creator attribution on Pinterest, and proposes a requirements-driven Supervised Machine Learning (Decision Tree) classification system to filter exact duplicates and preserve creator provenance.

---

## Problem Statement

Visual search platforms face severe feed redundancy due to unchecked visual content duplication. Regular Pinterest users and original content creators are affected when automated accounts scrape high-performing Pins, apply minor visual edits (such as cropping, color filters, or text overlays), and re-upload them to divert referral traffic. In a platform review of visual discovery feeds, identical or slightly modified versions of popular DIY and home decor Pins frequently appear across multiple accounts without linking back to the original creator. This matters because repetitive search results reduce user trust, deprive original creators of traffic and attribution, and increase server indexing overhead.

---

## Documents

| Document | Description |
| :--- | :--- |
| [Problem statement](docs/problem_statement.md) | Problem, evidence, Fishbone analysis, users, stakeholders, and scope (Part A) |
| [Requirements](docs/requirements.md) | Functional and non-functional requirements (Part B) |
| [User stories](docs/user_stories.md) | Three user stories with linked requirements and acceptance criteria (Part B) |
| [Specialized technology](docs/specialized_technology.md) | Supervised ML concepts, worked example, tools, fit, limitations, and references (Part C) |

---

## Specialized Technology

**Supervised Machine Learning (Decision Tree Classification):** Multi-feature classification combining perceptual image hashing (`ImageHash` Hamming distance), title cosine similarity, and account behavior metrics (`scikit-learn` `DecisionTreeClassifier`) to categorize uploads into *Original*, *Near-Duplicate*, or *Exact Duplicate*.

---

## Proposed Users and Scope

The main users and stakeholders are:
* **Regular Pinterest Users:** Browse feeds and search for visual inspiration without repetitive clutter.
* **Content Creators:** Publish original visual artwork and rely on proper attribution and referral traffic.
* **Trust & Safety Moderators:** Monitor platform quality and suppress automated spam/re-pin networks.

**Scope Summary:**
* **In Scope:** Feature vector extraction (perceptual hashing and metadata similarity), Decision Tree classification into 3 novelty tiers, search feed suppression of exact duplicates, attribution badges for near-duplicates, and moderator spike alerts.
* **Out of Scope:** Full-scale production deployment, live scraping of proprietary Pinterest servers, and copyright legal enforcement.

---

## Status

Completed

---

## Author

* **Name:** MUHAMMAD IZWAN BIN MOHD SHARIL
* **Student ID:** 2025240964
* **Class:** CS2305E

---

## Disclaimer

Pinterest is a trademark of Pinterest, Inc. This repository is a non-commercial academic exercise for CSC649 at Universiti Teknologi MARA (UiTM) and is not affiliated with or endorsed by Pinterest, Inc[cite: 5].
