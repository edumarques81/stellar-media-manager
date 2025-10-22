# Stellar Media Manager - Complete Feature List

**Project:** AI-Powered Photography Management & Distribution Platform
**Last Updated:** October 22, 2025
**Status:** Planning Complete, Ready for Development

---

## Core Features Overview

Stellar Media Manager is divided into **8 major feature areas** (Epics) with 87 total user stories. Below is a comprehensive list of all features organized by category.

---

## 1. AI Recognition System (Epic 1)

### Facial Recognition
- **Selfie Upload for Matching**: Customers upload a selfie to instantly find their photos
- **Participant Profile Creation**: Photographers can request selfies from participants before events
- **99%+ Accuracy Target**: High-precision facial recognition using pre-trained models (FaceNet/ArcFace)
- **Challenging Conditions Support**: Works with blurry images, side profiles, group photos, partial faces
- **Front-Facing & Action Photos**: Recognizes faces in both portrait and action photography scenarios
- **Real-Time Processing**: Matches photos within 5 minutes of upload
- **Opt-In/Opt-Out Controls**: Participants can choose not to use facial recognition

### Jersey Number Recognition
- **OCR for Sports Jerseys**: Automatically reads jersey numbers from sports photography
- **Obscured Face Handling**: Identifies athletes even when faces aren't visible (helmets, turned away)
- **Configurable Number Formats**: Supports numeric-only, alphanumeric, or custom patterns per event
- **Action Shot Accuracy**: Maintains recognition accuracy on photos with motion blur
- **Manual Correction**: Photographers can manually assign jersey numbers if AI is uncertain

### Race Bib & Identifier Recognition
- **Bib Number Detection**: Recognizes race bibs for marathon and running events
- **Name Tag Reading**: Extracts text from visible name tags and identifiers
- **Angled Text Extraction**: Handles bibs at angles or partially obscured
- **Multiple Identifier Types**: Supports various identifier formats per event type

### Multi-Modal Fusion Engine
- **Combined Recognition**: Merges facial, jersey, and OCR results with weighted confidence scoring
- **Configurable Weights**: Administrators can adjust fusion weights per event type (e.g., face 70%, jersey 25%, OCR 5%)
- **Conflict Resolution**: Flags photos for review when different methods disagree
- **Confidence Scoring**: Each photo gets a combined confidence score (0-100%)

### Continuous Learning System
- **Manual Correction Learning**: AI improves from photographer corrections in review queue
- **Accuracy Tracking**: Monitors improvement over time across events
- **Pattern Recognition**: Identifies recurring errors and adjusts models
- **Cross-Event Learning**: Applies learning from one event to similar future events

### Review Queue
- **Low-Confidence Review**: Photos below 80% confidence go to manual review queue
- **Sorted by Confidence**: Queue sorted with lowest confidence first for efficient review
- **Keyboard Shortcuts**: Fast review with Y (approve), N (reject), arrow keys (navigate)
- **Bulk Actions**: Approve all photos above a certain confidence threshold at once
- **Top Match Suggestions**: Shows top 3 possible participant matches for uncertain photos

---

## 2. Gallery & Media Management (Epic 2)

### Gallery Creation & Organization
- **Event-Based Galleries**: Create galleries for events, clients, teams, or seasons
- **Hierarchical Structure**: Organize as Event → Teams → Individuals
- **Bulk Photo Upload**: Drag-and-drop interface for uploading thousands of photos
- **FTP Import Support**: (Phase 2) Upload via FTP for large batches
- **Gallery Templates**: Reuse templates for recurring event types
- **Metadata Preservation**: Maintains original EXIF data, timestamps, and location info

### Auto-Tagging & Sorting
- **AI-Powered Tagging**: Photos automatically tagged with participant names based on recognition
- **Team & Individual Sorting**: Auto-sort into participant-specific and team galleries
- **Time-Based Organization**: Sort photos chronologically by capture time
- **Custom Criteria Sorting**: Flexible sorting by photographer-defined criteria

### Access Control
- **Public/Private Galleries**: Toggle gallery visibility (public link or access code required)
- **Unique Access Codes**: Generate 8-character alphanumeric codes per gallery
- **Password Protection**: Additional password layer for sensitive galleries
- **Gallery Expiration**: Set expiration dates for time-limited access
- **Download Permissions**: Control who can download photos (vs. view only)

### Media Storage
- **Cloud Storage**: Photos stored on AWS S3 with redundancy
- **CDN Delivery**: CloudFront CDN for fast global photo delivery
- **Original Quality Preservation**: High-resolution originals maintained
- **Semi-Annual Backup**: Automated backup to external storage every 6 months (per client spec)

---

## 3. Customer Portal (Epic 3)

### Photo Discovery
- **Selfie Upload Search**: Upload selfie to instantly find all matched photos
- **Name Search**: Search by participant name, team name, or event name
- **Number Search**: Search by jersey number or bib number
- **Event Browsing**: Browse all photos from an event
- **Results Within 5 Seconds**: Fast display of matched photos after selfie upload

### Browsing & Viewing
- **Responsive Grid Layout**: 4 columns (desktop), 3 (tablet), 2 (mobile)
- **Lightbox Viewer**: Full-screen photo viewing with navigation
- **Keyboard & Swipe Navigation**: Arrow keys and swipe gestures for photo browsing
- **Photo Metadata Display**: Event name, date, time, and photo number shown
- **Zoom Capability**: Zoom in on watermarked previews

### Watermarked Previews
- **Pre-Purchase Watermarks**: All preview images have configurable watermark overlays
- **Logo or Text Watermarks**: Photographer can use logo image or text watermark
- **40% Opacity Overlay**: Semi-transparent watermark centered on image
- **Screenshot Prevention**: Basic protection against screen capture (where technically possible)
- **Watermark Removal**: Purchased photos have no watermark

### Favoriting
- **Heart Icon Favorites**: Click heart to save favorite photos
- **Persistent Favorites**: Favorites stored in browser localStorage
- **Favorites Filter**: View only favorited photos in gallery
- **Favorites Count**: Display count of favorited photos

---

## 4. E-Commerce & Checkout (Epic 3 Continued)

### Shopping Cart
- **Add to Cart**: Add photos to cart from gallery or lightbox
- **Cart Item Management**: Update quantities, change product types, remove items
- **Product Selection**: Choose between digital downloads and various print sizes
- **Price Calculation**: Real-time calculation of subtotal, shipping, tax, and total
- **Cart Persistence**: Cart saved in localStorage across sessions

### Digital Downloads
- **Instant Download**: Immediate high-resolution download after purchase
- **Email Delivery**: Download links sent via email
- **Unlimited Re-Downloads**: Re-download for 1 year after purchase
- **Batch Download**: Download all purchased photos as ZIP file
- **Pricing**: Configurable per photographer (default: $4.99)

### Print Products (Phase 2)
- **Print Sizes**: 4x6, 5x7, 8x10, 11x14, 16x20, custom sizes
- **Finish Options**: Glossy, matte, metallic (metallic +$5)
- **Merchandise**: (Future) Mugs, calendars, photo books, canvas prints
- **Product Preview**: See customer's photo in print format before ordering
- **Quantity Selection**: Order multiple copies (1-10) per photo

### Payment Processing
- **Stripe Integration**: Secure credit card processing via Stripe Elements
- **PayPal Support**: PayPal as alternative payment method
- **Australian Tax Calculation**: 10% GST calculated automatically
- **Multiple Currencies**: (Future) Support for international customers
- **Secure Checkout**: PCI-compliant payment handling

### Order Management
- **Order Confirmation**: Email confirmation with order number immediately after purchase
- **Order History**: Customers can view past orders
- **Order Tracking**: Track print orders from production to delivery
- **Receipt Generation**: PDF receipts emailed to customers

---

## 5. Print Fulfillment (Epic 4 - Phase 2)

### Print Lab Integration
- **API Integrations**: Connect with Bay Photo Lab and local Australian print labs
- **Custom Lab Integrations**: Support for non-standard lab APIs
- **High-Resolution Transmission**: Send full-resolution images to selected lab
- **Product Specifications**: Include size, finish, quantity, and shipping info in orders

### Intelligent Routing Engine
- **Geography-Based Selection**: Route orders to nearest lab based on customer location
- **Pricing Consideration**: Factor in lab pricing when selecting vendor
- **Photographer Preferences**: Allow manual override and preferred lab settings
- **Load Balancing**: Distribute high-volume events across multiple labs
- **Lab Partner Profiles**: Maintain capabilities, pricing, and geography data per lab

### Order Tracking
- **Real-Time Status Updates**: Receive updates from print labs (submitted, printing, shipped)
- **Customer Notifications**: Automatic emails/SMS when order status changes
- **Tracking Numbers**: Provide shipping tracking numbers when available
- **Estimated Delivery Dates**: Display expected delivery date range
- **Order Modifications**: Handle cancellations and changes (if lab supports)

### Invoicing & Reconciliation
- **Lab Cost Tracking**: Record actual costs from print labs
- **Revenue Calculation**: Calculate photographer profit (sale price - lab cost - platform fee)
- **Invoice Generation**: Auto-generate invoices for lab partner billing
- **Reconciliation Reports**: Financial reports for accounting purposes

---

## 6. Admin Dashboard (Epic 5)

### Dashboard Overview
- **Key Metrics Cards**: Total events, photos uploaded, revenue (30 days), pending reviews
- **Recent Events Display**: Visual cards showing recent events with stats
- **Quick Actions Panel**: Fast access to create event, upload photos, review queue
- **Activity Feed**: Timeline of recent actions (purchases, AI processing, new events)

### Event Management
- **Event Creation Wizard**: Multi-step form (basic info, AI settings, gallery settings, participants)
- **Event Templates**: Pre-configured templates for recurring event types
- **Participant Roster Upload**: CSV/Excel import with validation
- **Selfie Request Emails**: Bulk email participants asking for selfie uploads
- **Event Duplication**: Copy existing events for series/seasons
- **Event Deletion**: With confirmation dialog

### Photo Upload
- **Bulk Upload Interface**: Upload thousands of photos with drag-and-drop
- **Progress Indicators**: Real-time upload progress (X of Y files, percentage)
- **Resume-able Uploads**: (Future) Pause and resume large uploads
- **Cloud Import**: (Future) Import from Dropbox, Google Drive
- **Lightroom Integration**: (Post-MVP) Direct export from Lightroom

### AI Review Queue Management
- **Queue Dashboard**: Display all photos needing manual review
- **Confidence Scores**: Show AI confidence for each photo and match suggestion
- **Keyboard Shortcuts**: Fast review with hotkeys
- **Productivity Metrics**: Track reviewer speed and accuracy

### Settings & Configuration
- **Account Settings**: Photographer profile, business name, contact info
- **Pricing Configuration**: Set default prices for digital downloads and prints
- **Watermark Settings**: Upload logo or configure text watermark
- **Payment Setup**: Connect Stripe account for revenue deposits
- **Notification Preferences**: Configure email/SMS notification settings

---

## 7. Analytics & Reporting (Epic 6)

### Event Analytics
- **Total Photos**: Count of photos uploaded per event
- **Gallery Views**: Unique visitor count to galleries
- **Photos Favorited**: Count of photos marked as favorites
- **Sales Metrics**: Digital downloads sold, prints ordered, total revenue
- **Conversion Rate**: Percentage of viewers who make purchases
- **Average Order Value**: Mean purchase amount per transaction

### Photo Performance
- **Popularity Rankings**: Most viewed, most favorited, most purchased photos
- **Best Matches Algorithm**: (Waldo-inspired) Rank photos by predicted quality/appeal
- **Low Performers**: Identify photos with no engagement

### Financial Reports
- **Revenue Breakdown**: Digital vs. print revenue
- **Cost Analysis**: Print lab costs, platform fees
- **Profit Margins**: Photographer net revenue per event
- **Date Range Filtering**: Last 7 days, 30 days, custom ranges
- **CSV Export**: Download reports for accounting software

### Customer Insights
- **Engagement Metrics**: Views, time on site, photos browsed
- **Repeat Customer Rate**: Percentage buying from multiple events
- **Customer Acquisition**: New vs. returning customers
- **Geographic Distribution**: Where customers are located

### Sponsorship Visibility (Phase 4)
- **Logo Detection**: AI identifies sponsor logos/brands in photos
- **Visibility Reporting**: Metrics on sponsor logo appearances
- **Engagement by Sponsor**: Views and purchases of photos featuring sponsors

---

## 8. Privacy, Security & Compliance (Epic 7)

### Data Privacy
- **Australian Privacy Principles (APPs) Compliance**: Full compliance with Australian data protection laws
- **GDPR Support**: Compliance for international customers
- **PII Encryption**: All personally identifiable information encrypted (AES-256)
- **Data Encryption in Transit**: TLS 1.3 for all network communication
- **Audit Logs**: Comprehensive logging of data access and modifications

### Consent Management
- **Parental Consent**: Required for children under 18 for facial recognition
- **Opt-In Facial Recognition**: Explicit consent required before facial profile creation
- **Marketing Consent Toggles**: Separate consent for marketing communications
- **Consent Timestamps**: Record when and how consent was obtained
- **Withdrawal of Consent**: Easy opt-out with facial profile deletion

### Authentication & Access Control
- **Strong Password Requirements**: Minimum 8 characters with complexity rules
- **Multi-Factor Authentication (MFA)**: Optional MFA for photographer accounts
- **Session Management**: Automatic timeout after 24 hours of inactivity
- **Unique Access Codes**: Gallery access via codes (no account required for customers)
- **Failed Login Tracking**: Monitor and alert on suspicious authentication attempts

### Data Retention & Deletion
- **Configurable Retention**: Photographers set photo retention periods per event
- **Right to be Forgotten**: Customers can request complete data deletion
- **Data Export**: Portable data export in standard formats (CSV, JSON)
- **Anonymization**: Analytics data anonymized after participant deletion
- **Backup Retention**: 6-month backup retention policy

### Security Measures
- **Annual Security Audits**: Third-party penetration testing
- **Rate Limiting**: Prevent abuse and DDoS attacks
- **OWASP Top 10 Protection**: Defense against common web vulnerabilities
- **Content Security Policy (CSP)**: Prevent XSS attacks
- **DDoS Protection**: CloudFlare or AWS Shield

---

## 9. Notifications & Communication (Epic 8)

### Automated Notifications
- **Photo Availability Emails**: Notify customers when new photos are published
- **SMS Notifications**: (Optional) Text messages when photos available
- **Order Status Updates**: Emails for order confirmation, shipping, delivery
- **Gallery Access Codes**: Email unique codes for private gallery access
- **Photographer Purchase Alerts**: Real-time notifications of new sales

### Email Integration
- **SendGrid / AWS SES**: Reliable email delivery service
- **Branded Templates**: Customizable email templates with photographer branding
- **Tracking**: Monitor email open rates and click-through rates
- **Deliverability Optimization**: SPF, DKIM, DMARC configuration

### SMS Integration
- **Twilio**: SMS delivery for time-sensitive notifications
- **Australian Numbers Support**: SMS to Australian mobile numbers
- **Opt-In Required**: Customers must opt-in for SMS notifications
- **Cost-Effective**: Only send SMS for high-value notifications

### Marketing Campaigns (Phase 4)
- **Re-Engagement Campaigns**: Email past customers about new events
- **Audience Segmentation**: Target specific customer groups
- **Campaign Performance Metrics**: Track opens, clicks, conversions
- **Easy Unsubscribe**: One-click unsubscribe from marketing emails
- **Explicit Opt-In**: Marketing consent separate from transactional emails

---

## 10. White-Label & API (Epic - Phase 4)

### White-Label Customization
- **Custom Domain**: Use photographer's own domain (e.g., photos.marcussports.com.au)
- **Color Scheme**: Customize primary colors, fonts, button styles
- **Logo Replacement**: Replace platform logo with photographer's brand
- **Email Templates**: Branded email templates matching photographer's identity
- **No Platform Branding**: Customers see photographer's brand, not Stellar Media Manager

### API Access
- **RESTful API**: Full API access for third-party integrations
- **API Documentation**: OpenAPI/Swagger specification
- **Authentication**: API keys and OAuth 2.0 support
- **Rate Limits**: Fair usage policies to prevent abuse
- **Webhooks**: Real-time notifications for events (new photo, new purchase, etc.)

### Third-Party Integrations
- **Club Management Systems**: Integrate with TeamSnap, LeagueApps, etc.
- **Accounting Software**: Export data to QuickBooks, Xero
- **Marketing Tools**: Integrate with Mailchimp, HubSpot
- **Social Media**: Auto-post to Facebook, Instagram

---

## Technology Features

### Performance
- **Processing Speed**: <5 minutes for facial recognition on 1000 photos
- **Page Load Time**: <2 seconds for customer portal
- **Concurrent Users**: Support 10,000 concurrent customer sessions
- **API Response Time**: <500ms for 95% of requests (P95)
- **Uptime SLA**: 99.9% availability

### Scalability
- **Horizontal Scaling**: Auto-scale compute resources for AI processing
- **Petabyte Storage**: Support massive photo archives
- **Data Partitioning**: Partition by photographer/event for performance
- **CDN Integration**: Global photo delivery via CloudFront

### Mobile Experience
- **Responsive Design**: Fully functional on mobile, tablet, desktop
- **Touch Gestures**: Swipe navigation for photo browsing
- **Mobile Camera**: Use device camera for selfie uploads
- **Progressive Web App**: (Future) Install as app on mobile devices

---

## Summary Statistics

- **Total Features**: 87 user stories across 8 epics
- **MVP Features**: 28 high-priority stories (Phase 1)
- **Post-MVP Features**: 59 stories (Phases 2-4)
- **Functional Requirements**: 294 in PRD
- **Target Accuracy**: 99% for AI recognition
- **Processing Time**: <5 minutes for 1000 photos
- **Uptime Target**: 99.9%

---

## Feature Prioritization

### Must-Have (MVP - Phase 1)
- Facial recognition with selfie upload
- Gallery management (upload, organize, access control)
- Customer portal (browse, search, preview, cart)
- Digital downloads with Stripe checkout
- Admin dashboard (events, review queue, basic analytics)
- Privacy controls (consent, opt-out, data deletion)

### Important (Phase 2)
- Print product catalog
- Print lab integrations
- Order routing and tracking
- Advanced analytics

### Nice-to-Have (Phases 3-4)
- Jersey and bib number recognition
- Multi-modal fusion engine
- Continuous AI learning
- White-label customization
- API access
- Marketing campaigns

---

**For detailed requirements, see:** [Product Requirements Document](../project-design/PRD.md)
**For user stories with acceptance criteria, see:** [User Stories](../user-stories/README.md)
