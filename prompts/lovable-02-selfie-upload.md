# Lovable Prompt 02: Selfie Upload & AI Matching

## Prompt for Lovable AI

Create a **Selfie Upload and AI Matching** page for Stellar Media Manager that allows customers to upload a selfie and receive their matched photos via facial recognition.

### Page Structure

**Header:**
- Back button (top-left) to return to landing page
- Page title: "Find Your Photos"
- Subtitle: "Upload a photo of yourself to see all your event photos"

**Upload Section (Initial State):**
Large central upload area with:
- Dashed border rectangle (400px x 500px on desktop, full-width on mobile)
- Camera icon (large, centered)
- Primary text: "Upload a Selfie"
- Secondary text: "For best results, use a clear, front-facing photo"
- Two buttons:
  - "Take Photo" (camera icon) - triggers device camera on mobile
  - "Choose from Library" (image icon) - file picker
- Accepted formats note: "JPG, PNG up to 10MB"

**Upload Section (Photo Selected):**
- Display selected photo as preview (max 400px width)
- "Change Photo" button (secondary style)
- "Find My Photos" button (primary style, prominent, purple)
- Loading state during AI processing

**Processing State:**
- Overlay the upload area with semi-transparent background
- Centered spinner animation
- Progress text: "Analyzing your photo... This takes about 30 seconds"
- Animated dots (...)

**Results State:**
Replace upload section with:
- Success icon (checkmark, green)
- Results headline: "We found 47 photos of you!" (number dynamic)
- Preview of first 3 matched photos (thumbnails)
- "View All Photos" button → navigates to gallery
- "Try Another Photo" link (if results seem wrong)

**No Results State:**
- Info icon (blue)
- Message: "We couldn't find any photos matching this selfie"
- Suggestions:
  - "Try another photo with better lighting"
  - "Make sure you're looking at the camera"
  - "Search by name instead"
- Buttons:
  - "Try Another Photo" (primary)
  - "Search by Name" (secondary)

**Privacy Notice (Bottom of Page):**
- Lock icon
- Text: "Your privacy matters. We only use your photo to find your event images. It's deleted after matching."
- Link: "Learn more about our privacy policy"

### Design Requirements

**Technology:**
- React with TypeScript
- Tailwind CSS
- Shadcn UI components (Button, Card, Dialog)
- React Dropzone for file upload
- Lucide React for icons

**Colors:**
- Use same palette from landing page
- Success: Green (#10b981)
- Info: Blue (#3b82f6)
- Loading: Purple (#667eea)

**File Upload Handling:**
- Accept: image/jpeg, image/png
- Max size: 10MB
- Client-side validation before upload
- Show file size and name after selection
- Image preview with aspect ratio maintained

**Responsive Design:**
- Mobile (<768px): Full-width upload area, stacked buttons
- Tablet (768px-1024px): Centered upload area (600px)
- Desktop (>1024px): Centered upload area (800px max)

**Animations:**
- Upload area: Pulse animation on drag-over
- Processing: Spinner with fade-in
- Results: Fade-in with slight slide-up
- Photo preview: Scale-in animation

### Functional Requirements

**Upload Flow:**
1. User selects photo via camera or file picker
2. Validate file (type, size) on client-side
3. Show preview with "Change Photo" and "Find My Photos" options
4. On "Find My Photos" click:
   - Show processing state
   - Upload to backend API: `POST /api/recognition/match`
   - Request body: `{ image: base64, galleryCode: string }`
5. Wait for response (30-60 seconds max)
6. Display results or no-results state

**API Integration (Mock for Now):**
```typescript
interface MatchResponse {
  success: boolean;
  matchCount: number;
  photos: Array<{
    id: string;
    thumbnailUrl: string;
    timestamp: string;
  }>;
}
```

**Error Handling:**
- Network error: "Connection lost. Please try again."
- File too large: "Photo must be under 10MB. Try a smaller file."
- Invalid format: "Please upload a JPG or PNG photo."
- Processing timeout: "Taking longer than usual. Please try again."
- Server error: "Something went wrong. Please try again later."

**Camera Access (Mobile):**
- Use `<input type="file" accept="image/*" capture="user" />` for camera
- Handle camera permission denial gracefully
- Fallback to file picker if camera unavailable

### Accessibility

- Keyboard navigation for all interactive elements
- Screen reader announcements for state changes ("Processing photo", "47 photos found")
- Alt text for result photo thumbnails
- Focus management (focus on results after loading)
- ARIA live regions for dynamic content updates

### Component Structure

```typescript
<SelfieUploadPage>
  <Header>
    <BackButton />
    <Title />
  </Header>

  <UploadSection>
    {!photoSelected && <DropzoneArea />}
    {photoSelected && !processing && <PhotoPreview />}
    {processing && <ProcessingState />}
    {results && <ResultsDisplay />}
    {noResults && <NoResultsState />}
  </UploadSection>

  <PrivacyNotice />
</SelfieUploadPage>
```

### Example Text Content

**Upload Instructions:**
- "Upload a clear photo of your face"
- "For best results: Good lighting, look at camera, no sunglasses"

**Processing Messages (Rotate Every 5 Seconds):**
- "Analyzing your photo..."
- "Searching through event photos..."
- "Matching faces with AI..."
- "Almost done..."

**Success Message:**
- "Great! We found {count} photos of you!"
- "Your photos are ready to view"

**No Results Troubleshooting:**
- "Tips for better results:"
- "✓ Use a recent photo with good lighting"
- "✓ Make sure your face is clearly visible"
- "✓ Try a photo where you're looking at the camera"

### Privacy & Consent

Before first upload, show a consent dialog:
- Title: "Photo Matching Consent"
- Message: "We'll use facial recognition to find your photos. Your selfie is only used for matching and is deleted after 24 hours. You can opt out anytime."
- Checkbox: "I consent to facial recognition for photo matching"
- Buttons: "Continue" (disabled until checkbox checked), "Cancel"

Store consent in localStorage: `facial_recognition_consent: true`

### Next Steps After This Page

After successful match:
- Display results with photo count
- "View All Photos" button navigates to `/gallery/{code}/photos?userId={matchedUserId}`
- That gallery view will be created in next prompt (Lovable Prompt 03)

---

**Priority:** High (MVP Sprint 4)
**Related User Stories:** US-001, US-030
**Dependencies:** Backend API endpoint for facial recognition (can mock for now)
**Deliverables:** Fully functional selfie upload component with file validation, preview, mock API integration, consent dialog
