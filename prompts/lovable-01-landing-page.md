# Lovable Prompt 01: Landing Page & Gallery Access

## Prompt for Lovable AI

Create a modern, responsive landing page for **Stellar Media Manager**, a photography event gallery platform.

### Page Structure

**Hero Section:**
- Large hero image or gradient background (use purple/blue gradient: #667eea to #764ba2)
- Headline: "Find Your Photos Instantly"
- Subheadline: "AI-powered photo discovery - Upload a selfie or search by name"
- Prominent gallery access code input field with "Access Gallery" button
- Example text below: "Have a code? Enter it above. Don't have one? Check your email or contact the photographer."

**Two-Path Discovery Section:**
Two large, visually distinct cards side-by-side (stacked on mobile):

**Card 1: Upload Selfie (Primary Path)**
- Icon: Camera or face outline
- Title: "Find Your Photos with a Selfie"
- Description: "Upload a photo of yourself and our AI will instantly find all your event photos"
- Button: "Upload Selfie to Find Photos" (purple, prominent)

**Card 2: Search by Name (Secondary Path)**
- Icon: Search magnifying glass
- Title: "Search by Name or Number"
- Description: "Browse all photos or search by participant name, team, or jersey number"
- Button: "Search Gallery" (outlined, less prominent)

**How It Works Section:**
Three-step visual guide with icons:
1. **Upload**: "Enter your gallery code or upload a selfie"
2. **Discover**: "AI finds all your photos in seconds"
3. **Purchase**: "Buy digital downloads or order prints"

**Footer:**
- Privacy link: "Your Privacy Matters"
- Contact photographer link
- Copyright: "Powered by Stellar Media Manager"

### Design Requirements

**Technology:**
- React with TypeScript
- Tailwind CSS for styling
- Responsive design (mobile-first)
- Use Shadcn UI components

**Colors:**
- Primary: Purple gradient (#667eea to #764ba2)
- Accent: Orange (#f59e0b)
- Background: Light gray (#f3f4f6)
- Text: Dark gray (#1f2937)

**Typography:**
- Headings: Bold, modern sans-serif (Inter or Poppins)
- Body: Regular sans-serif (Inter)

**Mobile Responsiveness:**
- Single column on mobile (<768px)
- Two columns on tablet (768px-1024px)
- Full layout on desktop (>1024px)

**Interactions:**
- Smooth transitions on hover (300ms ease)
- Button hover: slight scale up (1.05) and shadow
- Input focus: purple border glow
- Loading state for "Access Gallery" button

### Functional Requirements

**Gallery Code Input:**
- Input field: 8-character alphanumeric code (auto-uppercase)
- Validation: show error if invalid format
- On submit: redirect to `/gallery/{code}` route
- Show loading spinner during validation

**Navigation to Upload Flow:**
- "Upload Selfie" button → navigate to `/selfie-upload` route
- "Search Gallery" button → navigate to `/search` route

**Form Validation:**
- Gallery code: required, exactly 8 characters, alphanumeric
- Display inline error messages
- Disable submit button while loading

### Accessibility

- Proper heading hierarchy (h1 for main headline, h2 for section titles)
- Alt text for all images and icons
- ARIA labels for interactive elements
- Keyboard navigation support
- Focus indicators on all interactive elements
- Minimum contrast ratio 4.5:1 for text

### Assets Needed

Use placeholder images or icons from:
- Lucide React icons (camera, search, user, check)
- Unsplash API for hero image (photography/event theme)
- Or use gradient backgrounds

### Component Structure

```
<LandingPage>
  <HeroSection>
    <Headline />
    <GalleryCodeInput />
  </HeroSection>
  <DiscoveryPathsSection>
    <SelfieUploadCard />
    <SearchCard />
  </DiscoveryPathsSection>
  <HowItWorksSection>
    <Step1 />
    <Step2 />
    <Step3 />
  </HowItWorksSection>
  <Footer />
</LandingPage>
```

### Example Text Content

**Hero Headline:** "Find Your Photos Instantly"
**Hero Subheadline:** "Your event memories are ready. Enter your gallery code to get started."

**Selfie Card Title:** "Smart Photo Discovery"
**Selfie Card Description:** "Upload a selfie and let AI find all your photos from the event. No searching required."

**Search Card Title:** "Browse All Photos"
**Search Card Description:** "Prefer to explore? Search by name, team, or number to find your photos."

**How It Works:**
- Step 1: "Enter your unique gallery code from email or SMS"
- Step 2: "Upload a selfie or search by name to find your photos"
- Step 3: "Preview, favorite, and purchase your favorite moments"

### Next Steps After This Page

This landing page will be the entry point. After completing this:
- User enters code → Gallery Display Page (next prompt)
- User clicks "Upload Selfie" → Selfie Upload & Match Page (subsequent prompt)
- User clicks "Search" → Search & Browse Page (subsequent prompt)

---

**Priority:** High (MVP Sprint 4)
**Related User Story:** US-030
**Deliverables:** Fully responsive React component with Tailwind CSS, TypeScript types, basic routing setup
