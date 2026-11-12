# Part B3: User Stories and Acceptance Criteria

## User Story 1 (Linked to FR3)
* **As a** regular Pinterest user,  
* **I want** exact duplicate images filtered out of my search results,  
* **So that** I see fresh ideas instead of the same re-posted Pin over and over.

### Acceptance Criteria
1. **Given** I search for visual inspiration, when my feed loads, **then** none of the Pins on the first 5 pages share the same perceptual image hash (i.e. none are Exact Duplicates).
2. **Given** the ML classifier flags a Pin as an Exact Duplicate, **when** the indexing pipeline runs, **then** the duplicate is hidden from search results and the original Pin keeps its ranking.

---

## User Story 2 (Linked to FR4)
* **As a** content creator,  
* **I want** near-duplicate copies of my artwork to show a badge that links back to my profile,  
* **So that** I still get referral traffic when someone re-uploads a slightly edited version of my work.

### Acceptance Criteria
1. **Given** an uploaded image is classified as a Near-Duplicate, **when** someone views it, **then** a clearly visible “Original Creator” badge linking to the original Pin appears on the Pin details page.
2. **Given** a user clicks the attribution link on a near-duplicate Pin, **when** the page loads, **then** they land on the original creator’s verified board or website without any errors.

---

## User Story 3 (Linked to FR5)
* **As a** Trust & Safety moderator,  
* **I want** a real-time dashboard alert when an account starts mass-duplicating content automatically,  
* **So that** I can shut down spam bot networks before they hurt the quality of the catalog.

### Acceptance Criteria
1. **Given** an account uploads more than 10 Near-Duplicate Pins within 60 minutes, **when** that threshold is crossed, **then** a high-priority ticket is automatically created in the admin queue within 30 seconds.
2. **Given** I open an alert ticket as an admin, **when** it loads, **then** I see a table comparing the account’s upload hashes against the original Pins they match.
