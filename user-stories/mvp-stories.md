# MVP User Stories
## Stellar Media Manager - Phase 1

**Target:** Minimum Viable Product (Months 1-4)
**Goal:** Core facial recognition, gallery management, customer portal, digital downloads, basic admin dashboard

---

## Sprint 1: Foundation & Event Setup (Weeks 1-2)

### US-010: Create Event
**As a** photographer
**I want** to create an event with basic details
**So that** I can start organizing photos for a specific shoot

**Acceptance Criteria:**
- Event creation form with fields: name, date, type, description
- Event saved to database with unique ID
- Event appears in photographer's event list

**Priority:** High | **Effort:** M | **PRD:** FR-180

---

### US-002: Upload Participant Roster
*(See [epic-01-ai-recognition.md](epic-01-ai-recognition.md#us-002) for full details)*

**Priority:** High | **Effort:** M | **PRD:** FR-182, FR-183

---

### US-003: Request Participant Selfies
*(See [epic-01-ai-recognition.md](epic-01-ai-recognition.md#us-003) for full details)*

**Priority:** High | **Effort:** M | **PRD:** FR-001, FR-230

---

## Sprint 2: Photo Upload & Basic Gallery (Weeks 3-4)

### US-020: Bulk Photo Upload
**As a** photographer
**I want** to upload multiple photos at once
**So that** I can efficiently add all event photos to the platform

**Acceptance Criteria:**
- Drag-and-drop interface for multiple files
- Progress indicator showing upload status (X of Y files, %)
- Support for JPEG files up to 50MB each
- Batch upload of up to 10,000 photos
- Success confirmation with thumbnail preview

**Priority:** High | **Effort:** L | **PRD:** FR-052, FR-053

---

### US-021: Create Gallery Structure
**As a** photographer
**I want** to organize photos into galleries by event and team
**So that** customers can browse organized collections

**Acceptance Criteria:**
- Auto-create gallery hierarchy: Event → Teams
- Manual gallery creation option
- Move photos between galleries (drag-and-drop)
- Set gallery visibility (public/private)
- Generate unique access codes for private galleries

**Priority:** High | **Effort:** M | **PRD:** FR-050, FR-051, FR-080, FR-081

---

### US-022: Gallery Access Control
**As a** photographer
**I want** to control who can access my galleries
**So that** only authorized viewers see photos

**Acceptance Criteria:**
- Toggle gallery visibility: public (anyone with link) or private (access code required)
- Generate unique access code per gallery (8-character alphanumeric)
- Access code entry page with validation
- Regenerate access code option
- Set gallery expiration date (optional)

**Priority:** High | **Effort:** S | **PRD:** FR-080-084

---

## Sprint 3: AI Facial Recognition Core (Weeks 5-6)

### US-001: Customer Selfie Upload
*(See [epic-01-ai-recognition.md](epic-01-ai-recognition.md#us-001) for full details)*

**Priority:** High | **Effort:** M | **PRD:** FR-001, FR-002, FR-006

---

### US-004: Facial Recognition Processing
*(See [epic-01-ai-recognition.md](epic-01-ai-recognition.md#us-004) for full details)*

**Priority:** High | **Effort:** XL | **PRD:** FR-002, FR-003, FR-006, FR-007

---

### US-010-opt: Opt-in/Opt-out Controls
*(See [epic-01-ai-recognition.md](epic-01-ai-recognition.md#us-010) for full details)*

**Priority:** High | **Effort:** M | **PRD:** FR-005, FR-270, FR-271

---

## Sprint 4: Customer Portal Browsing (Weeks 7-8)

### US-030: Customer Photo Discovery
**As a** customer
**I want** to search for photos by name or upload a selfie
**So that** I can find photos of myself or my child

**Acceptance Criteria:**
- Landing page with two options: "Upload Selfie" or "Search by Name/Number"
- Selfie upload triggers facial recognition (see US-001)
- Name search shows list of matching participants
- Select participant to view their photo gallery
- Display count: "47 photos found"

**Priority:** High | **Effort:** M | **PRD:** FR-090-093

---

### US-031: Browse Photo Gallery
**As a** customer
**I want** to browse photos in an organized gallery
**So that** I can view all matched photos easily

**Acceptance Criteria:**
- Grid view of photos (responsive: 3 columns desktop, 2 tablet, 1 mobile)
- Click photo to open lightbox view
- Navigate photos with arrow keys or swipe gestures
- Display watermarked previews
- Show photo metadata: event name, date, team

**Priority:** High | **Effort:** M | **PRD:** FR-100-104

---

### US-032: Watermarked Previews
**As a** photographer
**I want** to display watermarked previews before purchase
**So that** customers can evaluate photos without downloading them for free

**Acceptance Criteria:**
- Apply configurable watermark (text or logo) to previews
- Watermark overlays center of image with 40% opacity
- Preview resolution: max 1200px width
- Prevent right-click save (basic protection)
- No watermark on purchased photos

**Priority:** High | **Effort:** M | **PRD:** FR-110-113

---

## Sprint 5: Digital Download Purchase (Weeks 9-10)

### US-040: Add Photos to Cart
**As a** customer
**I want** to add photos to a shopping cart
**So that** I can purchase multiple photos in one transaction

**Acceptance Criteria:**
- "Add to Cart" button on each photo
- Cart icon shows item count
- View cart page with thumbnail, price per item
- Remove items from cart
- Update quantities (digital downloads: qty 1 only)
- Display subtotal, tax, total

**Priority:** High | **Effort:** M | **PRD:** FR-103, FR-120

---

### US-041: Digital Download Checkout
**As a** customer
**I want** to purchase digital photo downloads
**So that** I can download high-resolution photos without watermarks

**Acceptance Criteria:**
- Checkout form: email address (required for delivery)
- Payment via Stripe: credit card or digital wallets
- Order summary: itemized list, taxes, total
- Successful payment confirmation page
- Email with download links sent immediately
- Download links valid for 1 year

**Priority:** High | **Effort:** L | **PRD:** FR-120-125

---

### US-042: Download Purchased Photos
**As a** customer
**I want** to download my purchased photos
**So that** I have high-resolution copies without watermarks

**Acceptance Criteria:**
- Email contains individual download links per photo
- Click link to download full-resolution JPEG (no watermark)
- Download page shows photo preview and file size
- "Download All as ZIP" option for multi-photo orders
- Re-download capability (unlimited within 1 year)

**Priority:** High | **Effort:** M | **PRD:** FR-120

---

## Sprint 6: Admin Dashboard Core (Weeks 11-12)

### US-050: Photographer Dashboard Overview
**As a** photographer
**I want** to see an overview dashboard of my events
**So that** I can quickly access events and see key metrics

**Acceptance Criteria:**
- Dashboard displays all events (sorted by date, most recent first)
- Event cards show: name, date, photo count, view count, sales count, revenue
- Quick actions: View Gallery, Upload Photos, Review Queue, Analytics
- Create New Event button prominently displayed
- Filter events: Upcoming, Past, Draft

**Priority:** High | **Effort:** M | **PRD:** FR-180, FR-210

---

### US-008: Manual Review Queue
*(See [epic-01-ai-recognition.md](epic-01-ai-recognition.md#us-008) for full details)*

**Priority:** High | **Effort:** M | **PRD:** FR-070-074, FR-190-194

---

### US-051: Basic Event Analytics
**As a** photographer
**I want** to see basic analytics for each event
**So that** I understand performance and customer engagement

**Acceptance Criteria:**
- Analytics page per event showing:
  - Total photos uploaded
  - Gallery views (unique visitors)
  - Photos favorited
  - Digital downloads sold (count + revenue)
  - Conversion rate (purchases / views)
- Date range filter (last 7 days, 30 days, all time)
- Export data as CSV

**Priority:** High | **Effort:** M | **PRD:** FR-210-217

---

## Sprint 7: Polish & Security (Weeks 13-14)

### US-060: Secure Authentication
**As a** photographer
**I want** to log in securely to my account
**So that** only I can access my events and data

**Acceptance Criteria:**
- Registration: email, password (min 8 chars, complexity requirements)
- Email verification required before first login
- Login with email + password
- JWT token-based session management
- Session timeout after 24 hours of inactivity
- Password reset via email link

**Priority:** High | **Effort:** M | **PRD:** FR-280, FR-281

---

### US-061: Data Encryption
**As a** the system
**I want** to encrypt all data in transit and at rest
**So that** customer data is protected from unauthorized access

**Acceptance Criteria:**
- All HTTP traffic uses TLS 1.3 (HTTPS only)
- Database connections encrypted
- Stored photos encrypted at rest (AES-256)
- Sensitive PII (emails, phone numbers) encrypted in database
- Encryption keys managed securely (AWS KMS or similar)

**Priority:** High | **Effort:** M | **PRD:** FR-263, FR-264

---

### US-062: Consent Management
**As a** parent
**I want** to consent to facial recognition for my child's photos
**So that** I have control over how their data is used

**Acceptance Criteria:**
- Selfie upload page includes consent checkbox (required)
- Consent language: "I consent to facial recognition to identify photos of [Name]. I understand data is used only for photo matching."
- Parental consent for minors (<18 years) explicitly marked
- Consent timestamp recorded
- Opt-out option to withdraw consent and delete facial profile

**Priority:** High | **Effort:** S | **PRD:** FR-270-273

---

## Sprint 8: MVP Testing & Launch (Weeks 15-16)

### US-070: End-to-End Testing
**As a** QA tester
**I want** to test the complete user flow
**So that** MVP is ready for pilot launch

**Test Scenarios:**
1. Photographer creates event, uploads roster, requests selfies
2. Customer receives email, uploads selfie, finds photos
3. Customer purchases digital downloads, receives download links
4. Photographer reviews AI queue, publishes gallery, views analytics
5. Privacy: customer opts out, data is deleted

**Priority:** High | **Effort:** L

---

### US-071: Pilot Program Launch
**As a** product owner
**I want** to onboard 10 pilot photographers
**So that** we validate MVP with real users

**Acceptance Criteria:**
- 10 photographers onboarded with training sessions
- Each photographer runs 1-2 real events
- Collect feedback via surveys and interviews
- Track success metrics: recognition accuracy, customer conversion, photographer satisfaction
- Iterate based on feedback before public launch

**Priority:** High | **Effort:** XL

---

## MVP Success Criteria

### Technical Metrics
- ✅ Facial recognition accuracy: ≥95% (target: 99%+)
- ✅ Processing time: <5 minutes for 1000 photos
- ✅ System uptime: 99%+
- ✅ Page load time: <2 seconds
- ✅ Zero critical security vulnerabilities

### Business Metrics
- ✅ 10 pilot photographers onboarded
- ✅ 20+ events processed
- ✅ 1000+ customer transactions
- ✅ Customer conversion rate: ≥25%
- ✅ Photographer satisfaction: 8/10+

### Feature Completeness
- ✅ Facial recognition with selfie upload
- ✅ Basic gallery management
- ✅ Customer portal (browse, search, preview)
- ✅ Digital download purchases
- ✅ Admin dashboard (event management, review queue, basic analytics)
- ✅ Privacy controls (opt-in/opt-out, consent, data deletion)
- ✅ Email notifications (selfie requests, purchase confirmations)

---

## Post-MVP (Phase 2 & Beyond)

### Phase 2: Print Integration (Months 5-6)
- US-080: Print product catalog
- US-081: Print lab API integration
- US-082: Print order routing
- US-083: Order tracking
- US-084: Shipping & fulfillment

### Phase 3: Advanced Recognition (Months 7-9)
- US-005: Jersey number recognition
- US-006: OCR for race bibs
- US-007: Recognition fusion engine
- US-009: Continuous learning
- US-012: Challenging conditions handling

### Phase 4: Enterprise Features (Months 10-12)
- US-090: White-label customization
- US-091: API access for integrations
- US-092: Advanced analytics
- US-093: Multi-language support
- US-094: Marketing campaign tools
- US-095: Role-based permissions

---

**End of MVP User Stories**
