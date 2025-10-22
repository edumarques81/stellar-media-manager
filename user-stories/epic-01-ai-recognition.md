# Epic 1: AI Recognition System

**Epic Goal:** Enable automated photo recognition using facial recognition, jersey numbers, and OCR to match photos with participants.

**Business Value:** Eliminates hours of manual photo tagging for photographers, provides instant photo discovery for customers.

**Target Release:** MVP (Phase 1)

---

## US-001: Participant Selfie Upload

**As a** customer (parent/participant)
**I want** to upload a selfie to find my photos
**So that** I can quickly see all photos of myself/my child without searching manually

**Priority:** High
**Estimated Effort:** M
**Dependencies:** None

### Acceptance Criteria

1. **Given** I am on the gallery landing page
   **When** I click "Upload Selfie to Find Your Photos"
   **Then** I see a file upload interface or camera capture option

2. **Given** I have selected a selfie image
   **When** I upload the file (max 10MB, JPG/PNG)
   **Then** the system displays a progress indicator and processes the image

3. **Given** facial recognition processing is complete (<5 minutes)
   **When** matches are found
   **Then** I see "We found X photos of [detected person]!" with photo gallery

4. **Given** no matches are found
   **When** processing completes
   **Then** I see "No photos found. Try another photo or browse all photos" with helpful suggestions

5. **Given** I upload an invalid file (too large, wrong format, no face detected)
   **When** validation fails
   **Then** I see a clear error message with guidance

### Technical Notes
- Support mobile camera capture and file upload
- Client-side image validation before upload
- Image preprocessing: face detection, quality check
- Async processing with WebSocket or polling for results
- Store uploaded selfie temporarily (deleted after session)

### Related Requirements
- FR-001: System shall accept participant selfie uploads for facial profile creation
- FR-002: System shall achieve minimum 99% facial recognition accuracy
- FR-006: System shall process facial recognition in near-real-time (<5 minutes from upload)

---

## US-002: Photographer Upload Participant Roster

**As a** photographer
**I want** to upload a participant roster with names, teams, and contact info
**So that** the system knows who to match photos against and can notify participants

**Priority:** High
**Estimated Effort:** M
**Dependencies:** US-010 (Event Creation)

### Acceptance Criteria

1. **Given** I have created an event
   **When** I navigate to "Upload Participant Roster"
   **Then** I see options to upload CSV/Excel file or manually add participants

2. **Given** I upload a CSV file with columns: Name, Team, Jersey Number, Age, Parent Email, Parent Phone
   **When** the file is valid
   **Then** the system previews imported data with row count and validation status

3. **Given** the CSV has errors (missing required fields, invalid email format)
   **When** I upload the file
   **Then** I see specific error messages with row numbers and correction suggestions

4. **Given** I confirm the import preview
   **When** I click "Import Participants"
   **Then** all participants are added to the event with success confirmation

5. **Given** I want to download a template
   **When** I click "Download CSV Template"
   **Then** I receive a pre-formatted CSV with correct column headers and example data

### Technical Notes
- Support CSV and Excel (.xlsx) formats
- Validate email addresses (regex), phone numbers (Australian formats)
- Handle encoding issues (UTF-8)
- Provide clear error messages with row numbers
- Allow partial imports (skip error rows, import valid ones)

### Related Requirements
- FR-182: Dashboard shall allow uploading participant rosters (CSV, Excel)
- FR-183: Dashboard shall manage team assignments and participant data

---

## US-003: Request Participant Selfies via Email

**As a** photographer
**I want** to send email requests for participants to submit selfies
**So that** the AI has facial profiles to match against event photos

**Priority:** High
**Estimated Effort:** M
**Dependencies:** US-002

### Acceptance Criteria

1. **Given** I have uploaded a participant roster
   **When** I click "Request Selfies from Participants"
   **Then** I see a preview of the email to be sent with customization options

2. **Given** I customize the email (subject, message, branding)
   **When** I click "Send Selfie Requests"
   **Then** emails are queued and sent to all participants with email addresses

3. **Given** an email is sent to a participant
   **When** the participant receives it
   **Then** the email contains a unique link to upload their selfie, event name, and instructions

4. **Given** a participant clicks the selfie upload link
   **When** they arrive at the upload page
   **Then** they see the event name, their name, and simple upload interface

5. **Given** I want to resend requests to participants who haven't responded
   **When** I click "Resend to Non-Responders" after 3 days
   **Then** only participants without selfies receive reminder emails

### Technical Notes
- Generate unique upload links per participant (tokenized URLs)
- Track email delivery status (sent, opened, clicked)
- Rate-limit email sending to avoid spam triggers
- Support email templates with variable substitution ({{participant_name}}, {{event_name}})
- Store selfie submission status per participant

### Related Requirements
- FR-001: System shall accept participant selfie uploads for facial profile creation
- FR-230: System shall send email notification when new photos are available
- FR-242: System shall support email templates with branding customization

---

## US-004: Facial Recognition Processing

**As a** the system
**I want** to automatically match uploaded event photos with participant facial profiles
**So that** photos are tagged with the correct people

**Priority:** High
**Estimated Effort:** XL
**Dependencies:** US-001, US-003

### Acceptance Criteria

1. **Given** a photographer uploads event photos
   **When** photos are uploaded successfully
   **Then** the system queues facial recognition processing for each photo

2. **Given** facial recognition processing begins
   **When** a face is detected in a photo
   **Then** the system compares it against all participant facial profiles

3. **Given** a face matches a participant profile with high confidence (>90%)
   **When** the match is confirmed
   **Then** the photo is automatically tagged with that participant's name

4. **Given** a face matches a participant profile with medium confidence (70-90%)
   **When** the match is identified
   **Then** the photo is added to the review queue for manual confirmation

5. **Given** a face matches a participant profile with low confidence (<70%)
   **When** the match is weak
   **Then** the photo is flagged for manual review with top 3 possible matches shown

6. **Given** no face is detected in a photo
   **When** facial recognition completes
   **Then** the photo is marked as "no face detected" and falls back to jersey/OCR recognition

### Technical Notes
- Use pre-trained facial recognition model (FaceNet, ArcFace, or similar)
- Implement face detection pipeline (detect → align → extract embedding → compare)
- Store facial embeddings (128/512-d vectors) for efficient comparison
- Support multiple faces per photo
- Process asynchronously with job queue (e.g., AWS SQS, Redis Queue)
- Optimize for GPU acceleration if available
- Track processing time and accuracy metrics

### Related Requirements
- FR-002: System shall achieve minimum 99% facial recognition accuracy
- FR-003: System shall handle challenging conditions: blurry images, groups, side profiles
- FR-006: System shall process facial recognition in near-real-time (<5 minutes from upload)
- FR-007: System shall work with both front-facing and action photography

---

## US-005: Jersey Number Recognition

**As a** the system
**I want** to recognize jersey numbers in sports photos using OCR
**So that** participants can be identified even when faces are obscured

**Priority:** High
**Estimated Effort:** L
**Dependencies:** US-004

### Acceptance Criteria

1. **Given** a photo is uploaded with a visible jersey number
   **When** OCR processing runs
   **Then** the system extracts the number from the jersey

2. **Given** a jersey number is detected (e.g., "7")
   **When** compared with participant roster
   **Then** the photo is matched to the participant with that jersey number on that team

3. **Given** a photo has both face and jersey number detected
   **When** both match the same participant
   **Then** confidence score increases (fusion boost)

4. **Given** a photo has both face and jersey number detected
   **When** they match different participants
   **Then** the match with higher individual confidence is used, flagged for review

5. **Given** a jersey number is partially obscured or blurry
   **When** OCR confidence is low (<70%)
   **Then** the detection is flagged for manual review

6. **Given** no jersey number is detected
   **When** OCR processing completes
   **Then** the photo relies solely on facial recognition

### Technical Notes
- Use OCR engine (Tesseract, Google Vision API, AWS Textract)
- Preprocess images for OCR: contrast enhancement, edge detection, region of interest detection
- Train/fine-tune OCR for jersey number fonts and angles
- Handle multi-digit numbers, letters (e.g., "7A")
- Support configurable jersey number formats per event (numeric only, alphanumeric)
- Store OCR confidence scores

### Related Requirements
- FR-010: System shall recognize jersey numbers via OCR technology
- FR-011: System shall identify participants when faces are obscured
- FR-013: System shall maintain accuracy on action shots with motion blur

---

## US-006: OCR for Race Bibs and Identifiers

**As a** the system
**I want** to recognize race bibs, name tags, and other visible identifiers
**So that** participants in non-jersey events (marathons, etc.) can be identified

**Priority:** Medium
**Estimated Effort:** M
**Dependencies:** US-005

### Acceptance Criteria

1. **Given** a photo from a marathon/race event
   **When** a race bib with number is visible
   **Then** the system extracts the bib number using OCR

2. **Given** a bib number is extracted (e.g., "1523")
   **When** matched against participant roster
   **Then** the photo is tagged with the participant assigned that bib number

3. **Given** a photo has visible name tag or text identifier
   **When** OCR detects the text
   **Then** the system attempts to match the text with participant names

4. **Given** multiple text regions are detected
   **When** OCR processes all regions
   **Then** the system prioritizes numeric identifiers (bib numbers) over text

5. **Given** bib is angled or partially obscured
   **When** OCR confidence is sufficient (>70%)
   **Then** the match is accepted; otherwise flagged for review

### Technical Notes
- Extend OCR pipeline to detect multiple text regions per photo
- Implement region-of-interest (ROI) detection for bibs (typically chest/abdomen area)
- Support various bib formats (large numbers, QR codes on bibs - optional)
- Handle perspective transformation for angled bibs
- Fuzzy text matching for name tags

### Related Requirements
- FR-020: System shall recognize race bibs, name tags, and other visible identifiers
- FR-021: System shall extract text from angled or partially obscured numbers
- FR-022: System shall support multiple identifier types per event

---

## US-007: Recognition Fusion Engine

**As a** the system
**I want** to combine facial recognition, jersey recognition, and OCR results with confidence scoring
**So that** identification accuracy exceeds any single method alone

**Priority:** High
**Estimated Effort:** L
**Dependencies:** US-004, US-005, US-006

### Acceptance Criteria

1. **Given** a photo has results from multiple recognition methods (face + jersey)
   **When** both methods match the same participant
   **Then** the combined confidence score is higher than either individual score (e.g., face 85% + jersey 80% = combined 95%)

2. **Given** a photo has results from multiple recognition methods
   **When** methods match different participants
   **Then** the system flags the photo for manual review with all candidate matches shown

3. **Given** a photo has high-confidence face match (95%) but low-confidence jersey match (60%) to different participants
   **When** fusion engine calculates combined result
   **Then** the face match is prioritized due to higher individual confidence

4. **Given** an administrator configures fusion weights per event
   **When** weights are set (e.g., face 60%, jersey 30%, OCR 10%)
   **Then** the fusion engine uses those weights to calculate combined confidence

5. **Given** the fusion engine processes all photos in an event
   **When** processing completes
   **Then** each photo has a final match with combined confidence score from all available methods

### Technical Notes
- Implement weighted scoring algorithm: `combined_confidence = (w_face * conf_face) + (w_jersey * conf_jersey) + (w_ocr * conf_ocr)`
- Default weights: face 70%, jersey 25%, OCR 5% (configurable per event)
- Conflict resolution: if methods disagree, flag for review if confidence delta < 20%
- Store individual method scores and combined score for transparency
- Track fusion performance metrics (accuracy improvement over single-method)

### Related Requirements
- FR-030: System shall combine multiple recognition methods with weighted confidence scoring
- FR-031: System shall use fusion results to improve match accuracy beyond single-method recognition
- FR-032: System shall allow administrators to configure fusion weights per event type

---

## US-008: Manual Review Queue for Low-Confidence Matches

**As a** photographer or reviewer
**I want** to review photos with low-confidence AI matches
**So that** I can correct errors and ensure all photos are correctly tagged

**Priority:** High
**Estimated Effort:** M
**Dependencies:** US-007

### Acceptance Criteria

1. **Given** AI processing completes for an event
   **When** some photos have confidence scores <80%
   **Then** those photos are added to the review queue

2. **Given** I open the review queue
   **When** the queue loads
   **Then** photos are sorted by confidence score (lowest first) with thumbnails and suggested matches

3. **Given** I am reviewing a photo in the queue
   **When** I see the photo, confidence score, and top 3 suggested matches
   **Then** I can approve, reject, or manually reassign the match

4. **Given** I approve a suggested match
   **When** I click "Approve"
   **Then** the photo is tagged with that participant and removed from queue (keyboard shortcut: "Y" or "Enter")

5. **Given** I need to manually assign a different participant
   **When** I search for and select the correct participant
   **Then** the photo is tagged and removed from queue

6. **Given** I cannot identify the participant in a photo
   **When** I click "Unable to Identify"
   **Then** the photo is marked as unidentified and removed from queue

7. **Given** I have reviewed all photos in the queue
   **When** the queue is empty
   **Then** I see "All photos reviewed! X photos approved, Y photos corrected"

### Technical Notes
- Implement keyboard shortcuts for efficiency (Y=approve, N=reject, arrow keys=navigate)
- Lazy load images for performance
- Track reviewer actions for AI retraining
- Support bulk actions (approve all >X% confidence)
- Show photo metadata (timestamp, filename, detection methods used)

### Related Requirements
- FR-070: System shall provide review queue for low-confidence matches (<80% confidence)
- FR-071: System shall allow reviewers to approve, reject, or reassign photo matches
- FR-072: System shall support bulk actions on review queue items
- FR-193: Dashboard shall support keyboard shortcuts for fast review

---

## US-009: Continuous Learning from Manual Corrections

**As a** the system
**I want** to learn from manual corrections made in the review queue
**So that** AI accuracy improves over time for future events

**Priority:** Medium
**Estimated Effort:** L
**Dependencies:** US-008

### Acceptance Criteria

1. **Given** a reviewer corrects an AI match (changes participant assignment)
   **When** the correction is saved
   **Then** the system logs the correction with original suggestion, final assignment, and photo features

2. **Given** corrections accumulate over multiple events
   **When** the learning system analyzes patterns
   **Then** the AI model is retrained or fine-tuned using correction data

3. **Given** the same participant appears in a subsequent event
   **When** their photos are processed
   **Then** recognition accuracy is measurably higher than the first event (track improvement metric)

4. **Given** an administrator views AI performance metrics
   **When** they access the analytics dashboard
   **Then** they see accuracy trends over time showing continuous improvement

5. **Given** a specific recognition error pattern is identified (e.g., confusing two similar-looking participants)
   **When** multiple corrections address this pattern
   **Then** the system adjusts to distinguish between those participants more accurately

### Technical Notes
- Implement feedback loop: corrections → feature extraction → model retraining
- Use online learning or periodic batch retraining
- Track metrics: accuracy before/after correction, error patterns, improvement rate
- Consider privacy: anonymize learning data, retain only facial embeddings and metadata
- Schedule retraining jobs (e.g., nightly, after N corrections)

### Related Requirements
- FR-040: System shall accept manual corrections to AI matches
- FR-041: System shall use corrections to retrain and improve recognition models
- FR-042: System shall track accuracy improvements over time
- FR-043: System shall apply learning across similar events/participants

---

## US-010: Opt-in/Opt-out Facial Recognition

**As a** customer (parent/participant)
**I want** to opt out of facial recognition if I have privacy concerns
**So that** my photos are not matched using AI (manual search only)

**Priority:** High
**Estimated Effort:** M
**Dependencies:** US-003

### Acceptance Criteria

1. **Given** I receive a selfie request email
   **When** I click the upload link
   **Then** I see an option: "I prefer not to use facial recognition (I'll search manually)"

2. **Given** I opt out of facial recognition
   **When** I submit my preference
   **Then** my facial profile is not created, and I am not included in AI matching

3. **Given** I have opted out
   **When** I visit the gallery
   **Then** I can search for photos using my name, team, or jersey number (manual search)

4. **Given** I initially opted in but want to opt out later
   **When** I access my privacy settings
   **Then** I can disable facial recognition and delete my facial profile

5. **Given** I am a parent opting out on behalf of a minor child
   **When** I submit the opt-out
   **Then** the child's facial profile is deleted and they are excluded from future facial matching

### Technical Notes
- Store opt-in/opt-out preference per participant
- Delete facial embeddings immediately upon opt-out
- Ensure opt-out status is respected in all AI processing jobs
- Provide alternative search methods (name, number, team, date)
- Maintain audit log of opt-in/opt-out actions with timestamps

### Related Requirements
- FR-005: System shall support opt-in/opt-out controls for participants
- FR-271: System shall allow participants to opt out of facial recognition
- FR-270: System shall capture parental consent for children's photos (<18 years)

---

## US-011: Display Confidence Scores (Admin Only)

**As a** photographer or administrator
**I want** to see confidence scores for AI matches
**So that** I understand how certain the AI is about each match

**Priority:** Medium
**Estimated Effort:** S
**Dependencies:** US-007

### Acceptance Criteria

1. **Given** I am viewing the event dashboard
   **When** I select a photo with AI matches
   **Then** I see the confidence score (0-100%) and which methods contributed (face/jersey/OCR)

2. **Given** I am in the review queue
   **When** I view a photo requiring review
   **Then** I see individual scores: Face: 75%, Jersey: 62%, Combined: 73%

3. **Given** I want to filter photos by confidence level
   **When** I apply a filter (e.g., "Show only <80% confidence")
   **Then** the dashboard displays only photos meeting that criteria

4. **Given** I export event data
   **When** I download the CSV report
   **Then** confidence scores are included in the export for analysis

### Technical Notes
- Display confidence as percentage with color coding (green >90%, yellow 70-90%, red <70%)
- Show breakdown of fusion components (face %, jersey %, OCR %)
- Include confidence scores in all admin views, hide from customer portal
- Support filtering and sorting by confidence score

### Related Requirements
- FR-033: System shall display confidence scores for manual review queue
- FR-073: System shall highlight confidence scores and recognition method used

---

## US-012: Facial Recognition on Challenging Conditions

**As a** the system
**I want** to handle challenging photo conditions (blur, side profiles, groups, partial faces)
**So that** recognition accuracy remains high even with non-ideal photos

**Priority:** High
**Estimated Effort:** L
**Dependencies:** US-004

### Acceptance Criteria

1. **Given** a photo is blurry due to motion
   **When** facial recognition processes it
   **Then** the system applies deblurring preprocessing and achieves >85% accuracy

2. **Given** a photo shows a participant's side profile (not front-facing)
   **When** facial recognition runs
   **Then** the system detects the side profile and matches with >90% accuracy

3. **Given** a group photo with 5+ people
   **When** facial recognition processes it
   **Then** the system detects and matches all visible faces

4. **Given** a photo where a participant's face is partially obscured (helmet, hand, etc.)
   **When** facial recognition runs
   **Then** the system matches based on visible facial features with appropriate confidence score

5. **Given** a photo with poor lighting (backlit, shadows)
   **When** facial recognition processes it
   **Then** the system applies brightness/contrast adjustments and achieves >85% accuracy

### Technical Notes
- Implement robust preprocessing pipeline: deblurring, contrast enhancement, face alignment
- Use models trained on diverse angles and conditions
- Support multi-face detection in group photos
- Apply confidence penalties for challenging conditions (e.g., blur reduces confidence by 10%)
- Log challenging condition types for model improvement

### Related Requirements
- FR-003: System shall handle challenging conditions: blurry images, groups, side profiles, partial faces
- FR-007: System shall work with both front-facing and action photography
- FR-013: System shall maintain accuracy on action shots with motion blur

---

## US-013: Configure Recognition Settings per Event

**As a** photographer
**I want** to configure AI recognition settings for each event
**So that** I can optimize recognition based on event type (e.g., jerseys vs. bibs vs. faces only)

**Priority:** Medium
**Estimated Effort:** M
**Dependencies:** US-007

### Acceptance Criteria

1. **Given** I am creating a new event
   **When** I reach the AI settings step
   **Then** I see options to enable/disable: Facial Recognition, Jersey Recognition, Bib/OCR Recognition

2. **Given** I select which recognition methods to enable
   **When** I configure fusion weights (Face: X%, Jersey: Y%, OCR: Z%)
   **Then** the system validates weights sum to 100% and saves configuration

3. **Given** I am configuring a sports event with jerseys
   **When** I enable Jersey Recognition
   **Then** I can specify jersey number format (numeric only, alphanumeric, custom pattern)

4. **Given** I am configuring a marathon event
   **When** I enable Bib/OCR Recognition
   **Then** I can specify bib number ranges (e.g., 1000-5000)

5. **Given** I am configuring a school portrait event
   **When** I enable only Facial Recognition
   **Then** Jersey and OCR methods are disabled for that event

### Technical Notes
- Store event-specific recognition configuration in database
- Apply configuration during AI processing job initialization
- Provide preset templates: "Sports Event", "Marathon", "School Portraits", "Custom"
- Validate configuration before allowing event photo upload

### Related Requirements
- FR-032: System shall allow administrators to configure fusion weights per event type
- FR-012: System shall support configurable jersey number formats per event

---

## US-014: Track Recognition Accuracy Metrics

**As a** an administrator
**I want** to see recognition accuracy metrics for each event
**So that** I can monitor AI performance and identify improvement opportunities

**Priority:** Medium
**Estimated Effort:** M
**Dependencies:** US-007, US-009

### Acceptance Criteria

1. **Given** an event has completed AI processing
   **When** I view the event analytics dashboard
   **Then** I see overall recognition accuracy: X% auto-matched, Y% manual review, Z% unidentified

2. **Given** I want to compare recognition methods
   **When** I view method-specific accuracy
   **Then** I see: Facial Recognition: 94%, Jersey: 87%, OCR: 78%

3. **Given** I want to track improvement over time
   **When** I view the AI performance trends chart
   **Then** I see accuracy increasing across events (e.g., Event 1: 87%, Event 5: 94%)

4. **Given** I want to identify problem areas
   **When** I view error analysis
   **Then** I see common error types: "Confused Participant A with B (12 times)", "Missed faces (8 photos)"

5. **Given** I export a performance report
   **When** I download the CSV
   **Then** it includes: event name, total photos, accuracy %, method breakdown, error count, review time

### Technical Notes
- Calculate accuracy: (auto_matched + manual_confirmed) / total_photos
- Track per-method accuracy for comparison
- Implement error categorization (false positives, false negatives, mismatches)
- Store historical metrics for trend analysis
- Generate reports with charts/visualizations

### Related Requirements
- FR-042: System shall track accuracy improvements over time
- FR-214: Dashboard shall generate financial reports (revenue, costs, profit by event)

---

## US-015: Fallback to Manual Tagging

**As a** photographer
**I want** to manually tag photos that AI cannot identify
**So that** every photo can be assigned to a participant even if recognition fails

**Priority:** High
**Estimated Effort:** S
**Dependencies:** US-008

### Acceptance Criteria

1. **Given** a photo has no AI match and is in the review queue
   **When** I select the photo
   **Then** I see an option "Manually Tag Participant"

2. **Given** I click "Manually Tag Participant"
   **When** a search dialog appears
   **Then** I can search participants by name, team, or number

3. **Given** I search and select a participant
   **When** I confirm the assignment
   **Then** the photo is tagged with that participant and removed from review queue

4. **Given** I want to tag multiple photos with the same participant
   **When** I select multiple photos in the queue
   **Then** I can bulk-assign them to one participant

5. **Given** a photo genuinely contains no identifiable participant (e.g., landscape shot)
   **When** I mark it as "No Participant / Group/Scenery Photo"
   **Then** it is categorized separately and not included in participant galleries

### Technical Notes
- Implement participant search with autocomplete
- Support batch tagging for efficiency
- Allow adding custom tags (e.g., "Team Photo", "Award Ceremony")
- Store manual tags separately from AI tags for learning purposes

### Related Requirements
- FR-074: System shall allow adding manual tags to unrecognized photos
- FR-014: System shall allow manual jersey number assignment and correction

---

**End of Epic 1: AI Recognition System**
