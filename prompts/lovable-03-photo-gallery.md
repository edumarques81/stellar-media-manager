# Lovable Prompt 03: Photo Gallery & Lightbox

## Prompt for Lovable AI

Create a **Photo Gallery Display** page for Stellar Media Manager that shows matched photos with watermarked previews, lightbox viewing, and favoriting capabilities.

### Page Structure

**Header (Sticky):**
- Back button (top-left) → returns to previous page
- Gallery title: "{Event Name} - Your Photos"
- Participant name if known: "Photos of {Name}"
- Photo count badge: "47 photos"
- Shopping cart icon (top-right) with item count badge
- Search/filter icon (top-right)

**Filter Bar (Below Header):**
Horizontal scroll on mobile, full row on desktop:
- "All Photos" (default active)
- "Portraits"
- "Action Shots"
- "Team Photos"
- "Most Recent"
- "Favorited" (shows only favorited photos)

**Photo Grid:**
- Responsive masonry grid layout
- Desktop: 4 columns
- Tablet: 3 columns
- Mobile: 2 columns
- Each photo card:
  - Watermarked image (center overlay: photographer logo/text, 40% opacity)
  - Hover effect: slight zoom (1.05) and shadow
  - Heart icon (top-right corner) for favoriting (filled if favorited, outline if not)
  - Photo number badge (bottom-left): "#23"
  - Date/time stamp (bottom-right): "Oct 20, 2:30pm"
  - Click anywhere on card → opens lightbox

**Infinite Scroll:**
- Load 30 photos initially
- Load 30 more when user scrolls to 80% of page
- Show "Loading more photos..." with spinner

**Lightbox (Modal):**
Opens when photo clicked:
- Full-screen overlay (semi-transparent black background)
- Large centered image (watermarked)
- Navigation arrows (left/right) for prev/next photo
- Close button (top-right, X icon)
- Photo info bar (bottom):
  - Photo number: "23 of 47"
  - Date/time: "October 20, 2025 at 2:30 PM"
  - Event name: "City Soccer Tournament"
- Action buttons (bottom-right):
  - Heart icon (favorite/unfavorite)
  - "Add to Cart" button (purple, prominent)
  - Share icon (copy link)
- Keyboard navigation: Arrow keys (prev/next), Esc (close), Space (favorite)
- Swipe gestures on mobile (left/right)

**Bottom Action Bar (Sticky):**
- "View Favorites ({count})" button
- "View Cart ({count} items)" button (purple, prominent if cart has items)

**Empty State (No Photos):**
If no photos match filters:
- Empty state illustration
- Message: "No photos found with this filter"
- "Clear Filters" button

**No Photos Found (User):**
If no photos matched during selfie upload:
- Friendly illustration
- Message: "We couldn't find any photos of you"
- Suggestions:
  - "Try uploading a different selfie"
  - "Browse all event photos instead"
- Buttons: "Try Another Selfie", "Browse All Photos"

### Design Requirements

**Technology:**
- React with TypeScript
- Tailwind CSS
- Shadcn UI components (Dialog for lightbox, Card)
- React Infinite Scroll Component or Intersection Observer
- Lucide React for icons
- Framer Motion for animations (optional)

**Colors:**
- Same palette as previous pages
- Favorite heart: Red (#ef4444) when filled
- Cart badge: Orange (#f59e0b)

**Image Handling:**
- Lazy load images (only load when in viewport)
- Use low-res placeholders while loading (blur-up effect)
- Watermark: Semi-transparent overlay (photographer logo or text)
- Maintain aspect ratio (use object-fit: cover)
- Thumbnail size: 400px width (auto height)
- Lightbox size: 1200px max width (auto height)

**Responsive Design:**
- Mobile: 2-column grid, simplified lightbox controls
- Tablet: 3-column grid, full lightbox features
- Desktop: 4-column grid, all features

**Animations:**
- Grid photos: Fade-in as they load
- Lightbox: Fade-in overlay, scale-in image
- Favorite heart: Scale pulse when clicked
- Cart badge: Bounce when item added

### Functional Requirements

**Photo Loading:**
- Initial load: Fetch 30 photos via API `GET /api/galleries/{code}/photos?userId={userId}&limit=30&offset=0`
- Infinite scroll: Fetch next batch when user scrolls near bottom
- Cache loaded photos to avoid re-fetching

**Favoriting:**
- Click heart icon → toggle favorite status
- Store favorites in localStorage: `favorites_{userId}: string[]` (photo IDs)
- Visual feedback: heart fills with red, slight scale animation
- Update favorites count in filter bar
- Persist across sessions

**Add to Cart:**
- Click "Add to Cart" in lightbox or on photo card
- Add photo ID to cart: stored in state and localStorage
- Update cart count badge (animate on change)
- Show toast notification: "Added to cart!" (2 seconds, bottom-right)
- Prevent duplicate adds (show "Already in cart" message)

**Filtering:**
- Click filter button → re-fetch photos with filter parameter
- API: `GET /api/galleries/{code}/photos?userId={userId}&filter={filterType}`
- Update grid with new results
- Maintain favorites filter client-side (filter from loaded photos)

**Lightbox Navigation:**
- Click photo → open lightbox with that photo
- Arrow keys / swipe → navigate to prev/next photo
- Esc key / click outside / X button → close lightbox
- Maintain scroll position when closing lightbox
- Preload prev/next images for smooth navigation

**Share Photo (Lightbox):**
- Click share icon → copy photo preview link to clipboard
- Link format: `https://stellarmedia.com/photo/{photoId}?preview=true`
- Show toast: "Link copied to clipboard!"

### Accessibility

- Proper focus management in lightbox (trap focus)
- Keyboard navigation (Tab, Arrow keys, Esc, Space, Enter)
- Screen reader announcements:
  - "Photo 23 of 47, City Soccer Tournament"
  - "Favorited" or "Unfavorited"
  - "Added to cart"
- Alt text for photos: "{EventName} photo {number}"
- ARIA labels for icon-only buttons
- Skip link to main content

### Component Structure

```typescript
<PhotoGalleryPage>
  <Header>
    <BackButton />
    <GalleryTitle />
    <CartIcon />
  </Header>

  <FilterBar>
    <FilterButton active={filter === 'all'}>All Photos</FilterButton>
    <FilterButton active={filter === 'portraits'}>Portraits</FilterButton>
    {/* ... */}
  </FilterBar>

  <PhotoGrid>
    {photos.map(photo => (
      <PhotoCard
        key={photo.id}
        photo={photo}
        onFavorite={handleFavorite}
        onClick={openLightbox}
      />
    ))}
  </PhotoGrid>

  <InfiniteScroll onLoadMore={loadMorePhotos} />

  {lightboxOpen && (
    <Lightbox
      photo={selectedPhoto}
      onClose={closeLightbox}
      onNext={nextPhoto}
      onPrev={prevPhoto}
      onFavorite={handleFavorite}
      onAddToCart={addToCart}
    />
  )}

  <BottomActionBar>
    <ViewFavoritesButton />
    <ViewCartButton />
  </BottomActionBar>
</PhotoGalleryPage>
```

### API Integration (Mock for Now)

```typescript
interface Photo {
  id: string;
  thumbnailUrl: string;
  fullSizeUrl: string;
  watermarkedUrl: string;
  timestamp: string;
  eventName: string;
  photoNumber: number;
  tags: string[]; // e.g., ["portrait", "action", "team"]
}

interface GalleryResponse {
  photos: Photo[];
  totalCount: number;
  hasMore: boolean;
}

// Mock API call
const fetchPhotos = async (
  galleryCode: string,
  userId: string,
  limit: number,
  offset: number,
  filter?: string
): Promise<GalleryResponse> => {
  // Return mock data
};
```

### Example Text Content

**Filter Labels:**
- All Photos
- Portraits
- Action Shots
- Team Photos
- Most Recent
- Favorited

**Lightbox Info:**
- "Photo {number} of {total}"
- "{EventName} - {Date} at {Time}"
- "Add to Cart - $4.99"

**Empty States:**
- "No favorited photos yet. Click the heart icon on photos you love!"
- "No photos match this filter. Try selecting a different filter."

**Toast Messages:**
- "Added to cart!" (success, green)
- "Already in cart" (info, blue)
- "Favorited!" (success, red heart icon)
- "Removed from favorites" (info)
- "Link copied to clipboard!" (success)

### Watermark Specification

**Watermark Overlay:**
- Position: Center of image
- Text: Photographer name or business logo
- Opacity: 40%
- Color: White with slight drop shadow (for visibility on dark backgrounds)
- Font size: 5% of image width (scalable)
- Rotation: 15° diagonal (optional)

Alternatively:
- Repeated pattern watermark (tiled across image)
- Logo in corner (bottom-right, 20% opacity)

### Next Steps After This Page

After user adds photos to cart:
- "View Cart" button navigates to `/cart` (Lovable Prompt 04: Shopping Cart)
- That cart page will show selected photos, pricing, and checkout

---

**Priority:** High (MVP Sprint 4)
**Related User Stories:** US-031, US-032, US-040
**Dependencies:** Backend API for fetching photos (can mock for now), watermark generation
**Deliverables:** Photo grid with infinite scroll, lightbox with navigation, favoriting, cart integration, responsive design
