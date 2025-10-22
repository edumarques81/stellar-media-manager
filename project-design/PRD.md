# Product Requirements Document (PRD)
## Stellar Media Manager

**Version:** 1.0
**Date:** October 22, 2025
**Project Owner:** Alexander Polizzi
**Document Prepared by:** Eduardo Marques
**Status:** Draft for Review

---

## 1. Executive Summary

### 1.1 Product Vision
Stellar Media Manager is an AI-powered photography management and distribution platform designed to revolutionize how photographers, event organizers, and customers manage, identify, distribute, and monetize event photos. The platform eliminates manual photo sorting through advanced facial recognition, jersey number detection, and OCR technology while providing seamless print fulfillment and e-commerce capabilities.

### 1.2 Business Objectives
- **Automate** photo recognition and distribution using AI (face, jersey, number analysis)
- **Streamline** photographer workflows from capture to sale
- **Eliminate** third-party platform dependencies for photography businesses
- **Integrate** print lab fulfillment for hybrid digital-physical revenue models
- **Ensure** compliance with Australian data privacy regulations
- **Provide** competitive advantage through customization and white-label capabilities
- **Enable** future licensing to third-party photographers and eventual business sale

### 1.3 Target Market
**Primary Users:**
- Professional photographers specializing in:
  - Youth sports photography
  - School portraits and events
  - Marathons and endurance events
  - General event photography
- Event organizers (sports clubs, schools, camps)

**Secondary Users:**
- Parents and guardians purchasing photos of children
- Athletes and event participants
- Print lab partners

**Geographic Focus:** Australia (with potential for global expansion)

---

## 2. Product Overview

### 2.1 Core Value Propositions

**For Photographers:**
- Own your platform without vendor lock-in
- Automated photo matching saving hours of manual work
- Multi-revenue streams (digital downloads + print sales)
- Advanced analytics for business optimization
- White-label customization capabilities

**For Event Organizers:**
- Simplified photo distribution to participants
- Fundraising opportunities through photo sales
- Professional branded galleries
- Reduced administrative burden

**For Customers (Parents/Participants):**
- Effortless photo discovery via selfie upload
- Secure, privacy-protected galleries
- Convenient digital and print ordering
- Real-time notifications when photos are available

### 2.2 Key Differentiators
1. **Multi-modal Recognition Fusion**: Combines facial recognition, jersey numbers, and OCR with confidence scoring
2. **Intelligent Print Lab Routing**: Geography and preference-based automated lab selection
3. **Continuous Learning AI**: Improves accuracy through manual correction feedback loops
4. **Australian Compliance First**: Built for Australian privacy regulations and data sovereignty
5. **Photographer Ownership**: Open architecture with API access vs. platform dependency
6. **Advanced Analytics**: Sponsorship visibility, conversion metrics, engagement tracking
7. **No QR/Barcode Dependency**: Focus on seamless AI-driven identification

---

## 3. Functional Requirements

### 3.1 AI Recognition System

#### 3.1.1 Facial Recognition
**Requirements:**
- FR-001: System shall accept participant selfie uploads for facial profile creation
- FR-002: System shall achieve minimum 99% facial recognition accuracy
- FR-003: System shall handle challenging conditions: blurry images, groups, side profiles, partial faces
- FR-004: System shall create unique facial templates that persist across events
- FR-005: System shall support opt-in/opt-out controls for participants
- FR-006: System shall process facial recognition in near-real-time (<5 minutes from upload)
- FR-007: System shall work with both front-facing and action photography

#### 3.1.2 Jersey/Number Recognition
**Requirements:**
- FR-010: System shall recognize jersey numbers via OCR technology
- FR-011: System shall identify participants when faces are obscured (helmets, turned away)
- FR-012: System shall support configurable jersey number formats per event
- FR-013: System shall maintain accuracy on action shots with motion blur
- FR-014: System shall allow manual jersey number assignment and correction

#### 3.1.3 OCR for Bibs and Identifiers
**Requirements:**
- FR-020: System shall recognize race bibs, name tags, and other visible identifiers
- FR-021: System shall extract text from angled or partially obscured numbers
- FR-022: System shall support multiple identifier types per event

#### 3.1.4 Recognition Fusion Engine
**Requirements:**
- FR-030: System shall combine multiple recognition methods (face + jersey + OCR) with weighted confidence scoring
- FR-031: System shall use fusion results to improve match accuracy beyond single-method recognition
- FR-032: System shall allow administrators to configure fusion weights per event type
- FR-033: System shall display confidence scores for manual review queue

#### 3.1.5 Continuous Learning System
**Requirements:**
- FR-040: System shall accept manual corrections to AI matches
- FR-041: System shall use corrections to retrain and improve recognition models
- FR-042: System shall track accuracy improvements over time
- FR-043: System shall apply learning across similar events/participants

---

### 3.2 Gallery and Media Management

#### 3.2.1 Gallery Creation and Organization
**Requirements:**
- FR-050: System shall support creating galleries for events, clients, teams, and seasons
- FR-051: System shall support hierarchical organization (Event > Team > Individual)
- FR-052: System shall allow bulk photo upload via web interface, drag-and-drop, and FTP
- FR-053: System shall process uploads asynchronously with progress indicators
- FR-054: System shall support gallery templates for recurring event types
- FR-055: System shall maintain original photo metadata (EXIF, timestamp, location)

#### 3.2.2 Auto-tagging and Sorting
**Requirements:**
- FR-060: System shall automatically tag photos based on AI recognition results
- FR-061: System shall sort photos by participant, team, time, and custom criteria
- FR-062: System shall create participant-specific sub-galleries automatically
- FR-063: System shall group team photos separately from individual portraits

#### 3.2.3 Manual Review Tools
**Requirements:**
- FR-070: System shall provide review queue for low-confidence matches (<80% confidence)
- FR-071: System shall allow reviewers to approve, reject, or reassign photo matches
- FR-072: System shall support bulk actions on review queue items
- FR-073: System shall highlight confidence scores and recognition method used
- FR-074: System shall allow adding manual tags to unrecognized photos

#### 3.2.4 Access Control
**Requirements:**
- FR-080: System shall support public and private gallery visibility settings
- FR-081: System shall generate unique access codes for private galleries
- FR-082: System shall allow password protection for sensitive galleries
- FR-083: System shall support gallery expiration dates
- FR-084: System shall control download permissions per gallery

---

### 3.3 Customer Portal

#### 3.3.1 Photo Discovery
**Requirements:**
- FR-090: System shall allow customers to search by name, number, event, team
- FR-091: System shall support selfie upload for automatic photo matching
- FR-092: System shall display customer's matched photos within 5 seconds of selfie submission
- FR-093: System shall group customer's photos by event and date
- FR-094: System shall show confidence scores for matches (optional display)

#### 3.3.2 User Interface
**Requirements:**
- FR-100: Portal shall be fully responsive (mobile, tablet, desktop)
- FR-101: Portal shall support touch gestures for mobile browsing
- FR-102: Portal shall provide grid and detail view modes
- FR-103: Portal shall support photo favoriting and shopping cart
- FR-104: Portal shall display photo metadata (event, date, photographer credit)

#### 3.3.3 Preview and Watermarking
**Requirements:**
- FR-110: System shall display watermarked previews before purchase
- FR-111: System shall support configurable watermark styles (logo, text, pattern)
- FR-112: System shall prevent screenshot capture on preview images (where technically possible)
- FR-113: System shall provide zoom capability on watermarked previews

#### 3.3.4 Purchase and Checkout
**Requirements:**
- FR-120: System shall support secure checkout for digital downloads
- FR-121: System shall support checkout for print products (sizes, finishes, quantities)
- FR-122: System shall integrate payment gateways (Stripe, PayPal, local Australian options)
- FR-123: System shall calculate taxes based on customer location
- FR-124: System shall send order confirmation emails
- FR-125: System shall provide order history and tracking

---

### 3.4 Print Fulfillment Integration

#### 3.4.1 Print Lab API Integration
**Requirements:**
- FR-130: System shall integrate with major print lab APIs (Bay Photo, local Australian labs)
- FR-131: System shall support custom integration for non-standard lab APIs
- FR-132: System shall transmit high-resolution images to selected lab
- FR-133: System shall include customer shipping and product specifications in orders

#### 3.4.2 Intelligent Routing Engine
**Requirements:**
- FR-140: System shall select print lab based on customer geography
- FR-141: System shall consider lab pricing in routing decisions
- FR-142: System shall support manual override of lab selection
- FR-143: System shall support photographer-configured lab preferences
- FR-144: System shall load-balance across labs for high-volume events
- FR-145: System shall maintain lab partner profiles (capabilities, pricing, geography)

#### 3.4.3 Order Tracking
**Requirements:**
- FR-150: System shall receive real-time status updates from print labs
- FR-151: System shall notify customers of order status changes
- FR-152: System shall provide tracking numbers when available
- FR-153: System shall display estimated delivery dates
- FR-154: System shall handle order cancellations and modifications (if lab supports)

#### 3.4.4 Print Product Catalog
**Requirements:**
- FR-160: System shall support multiple print sizes (4x6, 5x7, 8x10, 11x14, 16x20, custom)
- FR-161: System shall support finish options (glossy, matte, metallic, canvas)
- FR-162: System shall support merchandise (mugs, calendars, photo books, etc.)
- FR-163: System shall maintain product pricing per lab and photographer markup
- FR-164: System shall display product previews with customer photos

#### 3.4.5 Invoicing and Reconciliation
**Requirements:**
- FR-170: System shall track costs from print labs
- FR-171: System shall calculate photographer revenue (sale price - lab cost - platform fee)
- FR-172: System shall generate invoices for lab partner billing
- FR-173: System shall support reconciliation reports for accounting

---

### 3.5 Administrative Dashboard

#### 3.5.1 Event and Gallery Management
**Requirements:**
- FR-180: Dashboard shall provide event creation wizard
- FR-181: Dashboard shall support event templates for recurring event types
- FR-182: Dashboard shall allow uploading participant rosters (CSV, Excel)
- FR-183: Dashboard shall manage team assignments and participant data
- FR-184: Dashboard shall track gallery publication status
- FR-185: Dashboard shall support event duplication for series/seasons

#### 3.5.2 AI Recognition Review Queue
**Requirements:**
- FR-190: Dashboard shall display pending recognition matches requiring review
- FR-191: Dashboard shall sort queue by confidence score (lowest first)
- FR-192: Dashboard shall show original photo, participant profile, and confidence score
- FR-193: Dashboard shall support keyboard shortcuts for fast review
- FR-194: Dashboard shall track reviewer productivity metrics

#### 3.5.3 Print Lab Configuration
**Requirements:**
- FR-200: Dashboard shall manage print lab partner integrations
- FR-201: Dashboard shall configure routing rules and preferences
- FR-202: Dashboard shall test lab API connections
- FR-203: Dashboard shall monitor lab fulfillment performance
- FR-204: Dashboard shall manage product catalog per lab

#### 3.5.4 Analytics and Reporting
**Requirements:**
- FR-210: Dashboard shall display key metrics (views, downloads, sales, revenue)
- FR-211: Dashboard shall show conversion funnel (views → cart → purchase)
- FR-212: Dashboard shall track photo popularity rankings
- FR-213: Dashboard shall report on sponsorship visibility (if logos/brands tagged)
- FR-214: Dashboard shall generate financial reports (revenue, costs, profit by event)
- FR-215: Dashboard shall export data to CSV/Excel
- FR-216: Dashboard shall provide date range filtering for all reports
- FR-217: Dashboard shall track customer engagement metrics

#### 3.5.5 Role-Based Access Control
**Requirements:**
- FR-220: System shall support roles: Administrator, Photographer, Organizer, Reviewer
- FR-221: Administrators shall have full system access
- FR-222: Photographers shall access only their events and galleries
- FR-223: Organizers shall view events they manage (read-only)
- FR-224: Reviewers shall access only recognition review queue
- FR-225: System shall support custom role creation with granular permissions

---

### 3.6 Notifications and Communication

#### 3.6.1 Automated Notifications
**Requirements:**
- FR-230: System shall send email notification when new photos are available
- FR-231: System shall send SMS notification for photo availability (optional)
- FR-232: System shall notify customers of order status updates
- FR-233: System shall send gallery access codes via email
- FR-234: System shall notify photographers of new purchases
- FR-235: System shall allow customers to configure notification preferences

#### 3.6.2 Communication Channels
**Requirements:**
- FR-240: System shall integrate with email service provider (SendGrid, AWS SES)
- FR-241: System shall integrate with SMS gateway (Twilio, local Australian providers)
- FR-242: System shall support email templates with branding customization
- FR-243: System shall track email open rates and click-through rates

#### 3.6.3 Marketing Campaigns
**Requirements:**
- FR-250: System shall support optional marketing campaigns to previous customers
- FR-251: System shall require explicit opt-in for marketing communications
- FR-252: System shall provide easy unsubscribe mechanism
- FR-253: System shall segment audiences for targeted campaigns
- FR-254: System shall track campaign performance metrics

---

### 3.7 Data Privacy and Security

#### 3.7.1 Compliance Requirements
**Requirements:**
- FR-260: System shall comply with Australian Privacy Principles (APPs)
- FR-261: System shall support GDPR compliance for international customers
- FR-262: System shall store personally identifiable information (PII) securely
- FR-263: System shall encrypt data in transit (TLS 1.3)
- FR-264: System shall encrypt data at rest (AES-256)
- FR-265: System shall maintain audit logs of data access

#### 3.7.2 Consent Management
**Requirements:**
- FR-270: System shall capture parental consent for children's photos (<18 years)
- FR-271: System shall allow participants to opt out of facial recognition
- FR-272: System shall support marketing consent toggles
- FR-273: System shall allow participants to request data deletion
- FR-274: System shall maintain consent records with timestamps

#### 3.7.3 Access Control and Authentication
**Requirements:**
- FR-280: System shall require strong passwords (min 8 characters, complexity rules)
- FR-281: System shall support multi-factor authentication (MFA) for administrators
- FR-282: System shall implement session timeout after inactivity
- FR-283: System shall use unique access codes for gallery access (no account required for basic viewing)
- FR-284: System shall log authentication attempts and failures

#### 3.7.4 Data Retention and Deletion
**Requirements:**
- FR-290: System shall support configurable photo retention periods
- FR-291: System shall provide data export in portable format
- FR-292: System shall permanently delete data upon customer request (right to be forgotten)
- FR-293: System shall anonymize analytics data after participant deletion
- FR-294: System shall maintain backup retention policy (6 months)

---

## 4. Non-Functional Requirements

### 4.1 Performance

**Requirements:**
- NFR-001: System shall process facial recognition within 5 minutes of upload
- NFR-002: Customer portal shall load galleries within 2 seconds
- NFR-003: System shall support concurrent upload of 10,000+ photos
- NFR-004: Dashboard shall load analytics within 3 seconds
- NFR-005: System shall handle 10,000 concurrent customer sessions
- NFR-006: API response time shall be <500ms for 95% of requests

### 4.2 Scalability

**Requirements:**
- NFR-010: System shall scale horizontally for compute-intensive AI processing
- NFR-011: Storage shall support petabyte-scale photo archives
- NFR-012: System shall partition data by photographer/event for performance
- NFR-013: System shall support CDN for global photo delivery

### 4.3 Availability and Reliability

**Requirements:**
- NFR-020: System shall maintain 99.9% uptime SLA
- NFR-021: System shall implement automated failover for critical services
- NFR-022: System shall perform daily automated backups
- NFR-023: System shall support disaster recovery with <4 hour RTO
- NFR-024: System shall monitor services with alerting for downtime

### 4.4 Security

**Requirements:**
- NFR-030: System shall undergo annual security audit
- NFR-031: System shall implement rate limiting to prevent abuse
- NFR-032: System shall protect against common vulnerabilities (OWASP Top 10)
- NFR-033: System shall use Content Security Policy (CSP) headers
- NFR-034: System shall implement DDoS protection

### 4.5 Usability

**Requirements:**
- NFR-040: Customer portal shall be usable by individuals aged 12+
- NFR-041: Dashboard shall require <1 hour training for basic operations
- NFR-042: System shall follow WCAG 2.1 Level AA accessibility guidelines
- NFR-043: System shall support English (primary) and other languages (future)

### 4.6 Maintainability

**Requirements:**
- NFR-050: System shall use containerized architecture (Docker)
- NFR-051: System shall implement comprehensive logging
- NFR-052: System shall maintain API versioning for backward compatibility
- NFR-053: System shall document all APIs with OpenAPI specification
- NFR-054: Codebase shall maintain minimum 80% test coverage

---

## 5. Technical Architecture

### 5.1 Technology Stack

#### Backend
- **Language:** Go (Golang)
- **Framework:** Chi, Gin, or Echo (to be determined during design)
- **API:** RESTful with GraphQL consideration for complex queries
- **Authentication:** JWT tokens with refresh mechanism

#### Frontend
- **Language:** TypeScript
- **Framework:** React
- **State Management:** Redux Toolkit or Zustand
- **UI Library:** Material-UI or Tailwind CSS
- **Build Tool:** Vite

#### AI/ML
- **Facial Recognition:** TensorFlow or PyTorch with pre-trained models (FaceNet, ArcFace)
- **OCR:** Tesseract or cloud-based (AWS Textract, Google Vision API)
- **Image Processing:** OpenCV, ImageMagick

#### Infrastructure
- **Cloud Provider:** AWS (primary) with Azure/GCP consideration
- **Compute:** ECS/EKS for containerized services
- **Storage:** S3 for photos, RDS/Aurora for relational data
- **CDN:** CloudFront for global delivery
- **Message Queue:** SQS/SNS for async processing
- **Cache:** Redis for session and query caching

#### Database
- **Primary DB:** PostgreSQL (relational data, transactional)
- **Document Store:** MongoDB or DynamoDB (photo metadata, flexible schema)
- **Search:** Elasticsearch (photo and participant search)

#### Third-Party Integrations
- **Payment:** Stripe, PayPal
- **Email:** SendGrid, AWS SES
- **SMS:** Twilio
- **Print Labs:** Custom integrations per lab

### 5.2 System Architecture Diagram
*(To be created during technical design phase)*

Key components:
1. **API Gateway** - Entry point for all client requests
2. **Authentication Service** - User and access management
3. **AI Recognition Service** - Face, jersey, OCR processing
4. **Gallery Management Service** - Media upload and organization
5. **Order Processing Service** - Checkout and fulfillment
6. **Print Lab Integration Service** - Routing and order transmission
7. **Notification Service** - Email/SMS delivery
8. **Analytics Service** - Metrics and reporting
9. **Admin Dashboard** - Photographer/organizer interface
10. **Customer Portal** - Public-facing photo browsing and purchase

---

## 6. User Stories Summary

*(Detailed user stories with acceptance criteria provided in separate user-stories/ folder)*

### Epic 1: AI Recognition
- US-001: As a photographer, I want to upload participant selfies so the system can recognize them in event photos
- US-002: As a customer, I want to upload my selfie and instantly see all my photos
- US-003: As a reviewer, I want to review low-confidence matches and correct errors

### Epic 2: Gallery Management
- US-010: As a photographer, I want to bulk upload event photos
- US-011: As a photographer, I want to create organized galleries by event and team
- US-012: As a photographer, I want to control who can access my galleries

### Epic 3: Customer Experience
- US-020: As a customer, I want to search for my photos by name or number
- US-021: As a customer, I want to preview photos before purchasing
- US-022: As a customer, I want to order digital downloads and prints
- US-023: As a customer, I want to receive notifications when new photos are available

### Epic 4: Print Fulfillment
- US-030: As a photographer, I want print orders automatically sent to labs
- US-031: As a customer, I want to track my print order status
- US-032: As an administrator, I want to configure print lab routing rules

### Epic 5: Analytics and Reporting
- US-040: As a photographer, I want to see sales and engagement metrics
- US-041: As a photographer, I want to understand which photos are most popular
- US-042: As an organizer, I want to track sponsorship visibility

### Epic 6: Privacy and Compliance
- US-050: As a parent, I want to consent to facial recognition for my child
- US-051: As a customer, I want to delete my data from the platform
- US-052: As an administrator, I want to ensure compliance with privacy regulations

---

## 7. Success Metrics (KPIs)

### Business Metrics
- **Revenue per Event**: Average revenue generated per event
- **Photographer Adoption Rate**: Number of photographers using the platform
- **Customer Conversion Rate**: % of gallery viewers who make purchases
- **Average Order Value**: Mean purchase amount per transaction
- **Repeat Customer Rate**: % of customers who purchase from multiple events

### Technical Metrics
- **Recognition Accuracy**: % of photos correctly matched to participants (target: 99%+)
- **Processing Time**: Time from upload to recognition completion (target: <5 min)
- **System Uptime**: % availability (target: 99.9%)
- **API Response Time**: P95 latency (target: <500ms)
- **Error Rate**: % of failed requests (target: <0.1%)

### User Experience Metrics
- **Time to First Photo**: How quickly customers find their first photo (target: <30 seconds)
- **Cart Abandonment Rate**: % of customers who add items but don't complete purchase (target: <20%)
- **Customer Satisfaction**: Net Promoter Score (target: 50+)
- **Mobile vs Desktop Usage**: % of traffic by device type

---

## 8. Risks and Mitigation

### Technical Risks
| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|
| AI accuracy below target (99%) | High | Medium | Use ensemble models, continuous learning, manual review queue |
| Print lab API downtime | Medium | Medium | Multi-lab routing, fallback to manual processing |
| Scalability issues during peak events | High | Low | Load testing, auto-scaling, CDN implementation |
| Data breach or security incident | Critical | Low | Security audits, encryption, access controls, incident response plan |

### Business Risks
| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|
| Insufficient photographer adoption | High | Medium | Pilot program, white-label options, competitive pricing |
| Competition from established players | Medium | High | Focus on differentiators, Australian market, customization |
| Print lab partnership issues | Medium | Low | Multi-lab relationships, contract SLAs |
| Regulatory compliance changes | Medium | Low | Monitor legal landscape, flexible architecture for compliance changes |

### Operational Risks
| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|
| Delayed development timeline | Medium | Medium | Agile methodology, MVP approach, phased rollout |
| Key personnel departure | Medium | Low | Documentation, knowledge sharing, code reviews |
| Infrastructure costs exceed budget | Medium | Medium | Cost monitoring, usage optimization, tiered pricing model |

---

## 9. Assumptions and Dependencies

### Assumptions
- Photographers have reliable internet for photo uploads
- Customers are willing to upload selfies for recognition
- Print labs maintain API availability and SLAs
- Australian market is ready for AI-powered photography solutions
- Participants (or parents) will consent to facial recognition

### Dependencies
- Third-party print lab API availability and documentation
- Cloud infrastructure provider (AWS) service reliability
- Payment gateway (Stripe/PayPal) integration success
- AI/ML model availability and licensing
- Email/SMS provider deliverability rates

---

## 10. Roadmap and Phasing

### Phase 1: MVP (Months 1-4)
**Core Features:**
- Facial recognition with selfie upload
- Basic gallery management (upload, organize)
- Customer portal (browse, search, preview)
- Digital download purchases
- Admin dashboard (event management, basic analytics)
- Australian data compliance

**Success Criteria:**
- 95%+ facial recognition accuracy
- 10 pilot photographers onboarded
- 1000+ customer transactions
- System uptime 99%+

### Phase 2: Print Integration (Months 5-6)
**Features:**
- Print lab API integrations (2-3 labs)
- Print product catalog
- Order routing engine
- Order tracking and fulfillment
- Invoicing and reconciliation

**Success Criteria:**
- 100+ print orders processed
- <5% order error rate
- Lab fulfillment satisfaction 90%+

### Phase 3: Advanced Recognition (Months 7-9)
**Features:**
- Jersey number recognition
- OCR for bibs and numbers
- Recognition fusion engine
- Continuous learning system
- Enhanced review queue tools

**Success Criteria:**
- 99%+ combined recognition accuracy
- 50% reduction in manual review time
- Recognition accuracy improvement over time demonstrated

### Phase 4: Enterprise Features (Months 10-12)
**Features:**
- White-label customization
- API access for integrations
- Advanced analytics and reporting
- Multi-language support
- Marketing campaign tools
- Role-based permissions expansion

**Success Criteria:**
- 50+ active photographers
- 2+ white-label deployments
- API adoption by 10+ integrators

### Phase 5: Scale and Optimize (Months 13+)
**Features:**
- Global expansion (beyond Australia)
- Mobile apps (iOS, Android)
- Advanced AI models (pose recognition, etc.)
- Sponsorship visibility tools
- Marketplace features
- Third-party photographer licensing

---

## 11. Open Questions

1. **Pricing Model**: What is the pricing structure for photographers? (Subscription, per-event, transaction fee, or hybrid?)
2. **Print Lab Contracts**: Which Australian print labs should we prioritize for partnerships?
3. **Data Residency**: Do we need Australian-only data storage, or can we use global AWS regions?
4. **Mobile Apps**: Are native mobile apps required in Phase 1, or is responsive web sufficient?
5. **AI Model Selection**: Should we build custom models or use pre-trained models with fine-tuning?
6. **White-label Branding**: How deep should customization go (colors only, or full design system)?
7. **Consent Flow**: Should consent be captured per-event or system-wide?
8. **Jersey Recognition Training**: Do we need photographers to provide training data for jersey styles?

---

## 12. Approval and Sign-off

| Role | Name | Signature | Date |
|------|------|-----------|------|
| Project Owner | Alexander Polizzi | | |
| Product Manager | Eduardo Marques | | |
| Technical Lead | TBD | | |
| UX Designer | TBD | | |

---

## 13. Appendices

### Appendix A: Glossary
- **AI Recognition**: Automated identification using computer vision and machine learning
- **Fusion Engine**: System combining multiple recognition methods with confidence scoring
- **Gallery**: Collection of photos from an event organized for viewing and purchase
- **Selfie Match**: Process of customers uploading selfie to find their photos
- **Watermark**: Overlay on preview images to prevent unauthorized use
- **Print Lab Routing**: Automated selection of print partner based on rules
- **Confidence Score**: Numerical representation of recognition certainty (0-100%)

### Appendix B: References
- [Client Specifications](alex_specs.md)
- [Meeting Summary (English)](first_meeting_summary-en.md)
- [Meeting Summary (Portuguese)](first_meeting_summary-pt.md)
- [Competitive Analysis](research/competitive-analysis.md)

### Appendix C: Change Log
| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2025-10-22 | Eduardo Marques | Initial draft based on client specs and research |

---

**End of Product Requirements Document**
