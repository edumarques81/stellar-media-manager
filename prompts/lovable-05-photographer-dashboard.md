# Lovable Prompt 05: Photographer Dashboard (Admin)

## Prompt for Lovable AI

Create a **Photographer Admin Dashboard** for Stellar Media Manager where photographers can manage events, upload photos, review AI matches, and view analytics.

### Page Layout

**Sidebar Navigation (Left, Collapsible on Mobile):**
- Logo/Brand: "Stellar Media Manager"
- User profile section:
  - Avatar (circular, 50px)
  - Photographer name
  - Business name (smaller text)
- Navigation menu:
  - 📊 Dashboard (home icon)
  - 📅 Events (calendar icon)
  - 🖼️ Galleries (images icon)
  - 🤖 AI Review Queue (brain icon) - badge with count
  - 📈 Analytics (chart icon)
  - ⚙️ Settings (gear icon)
- Bottom:
  - Help / Support link
  - Logout button

**Main Content Area:**
Dashboard view (default when logged in)

### Dashboard View

**Header:**
- Page title: "Dashboard"
- Greeting: "Welcome back, {PhotographerName}!"
- Date: Current date
- Quick action button: "+ Create Event" (top-right, purple, prominent)

**Key Metrics Cards (Top Row):**
4 stat cards in a row (stacked on mobile):
1. **Total Events**
   - Large number: "24"
   - Subtext: "Active events"
   - Icon: Calendar

2. **Photos Uploaded**
   - Large number: "12,453"
   - Subtext: "Across all events"
   - Icon: Camera

3. **Total Revenue**
   - Large number: "$18,245"
   - Subtext: "Last 30 days"
   - Trend: "+12% from last month" (green)
   - Icon: Dollar sign

4. **Pending Reviews**
   - Large number: "127"
   - Subtext: "Photos need review"
   - Action link: "Review now →"
   - Icon: Alert circle (orange if > 0)

**Recent Events (Main Section):**
- Section title: "Recent Events"
- Filter buttons: All / Upcoming / Past / Draft
- Event cards (2 columns on desktop, 1 on mobile):

Each event card shows:
- Event cover image (top, 16:9 aspect ratio)
- Event name: "City Soccer Tournament U12"
- Event date: "October 20-22, 2025"
- Status badge: "Published" (green), "Draft" (gray), "Processing" (yellow)
- Stats row:
  - 📷 Photos: 1,247
  - 👁️ Views: 3,452
  - 🛒 Sales: 89 ($421.55)
- Action buttons:
  - "View Gallery" (secondary)
  - "Analytics" (secondary)
  - "Upload Photos" (primary, if event is upcoming/active)
  - "Review Queue" (if has pending reviews, orange badge)
- Overflow menu (3 dots):
  - Edit event
  - Duplicate event
  - Delete event
  - Download all photos

**Empty State (No Events):**
- Illustration: Camera with empty folders
- Message: "You haven't created any events yet"
- Subtext: "Get started by creating your first event and uploading photos"
- "Create Your First Event" button (large, centered, purple)

**Quick Actions Panel (Right Sidebar on Desktop, Bottom on Mobile):**
- Title: "Quick Actions"
- Button list:
  - "+ Create Event"
  - "📤 Upload Photos"
  - "🔍 Review AI Matches"
  - "📊 View Analytics"
  - "⚙️ Account Settings"

**Recent Activity Feed (Optional):**
- Title: "Recent Activity"
- Timeline of recent actions:
  - "Sarah Johnson purchased 3 photos from 'Spring Soccer'" (2 min ago)
  - "AI processing completed for 'Marathon 2025'" (15 min ago)
  - "New event 'Graduation Day' created" (1 hour ago)
- "View all activity" link

### Create Event Modal

Triggered by "+ Create Event" button:

**Modal Structure:**
- Title: "Create New Event"
- Multi-step form (progress indicator at top):

**Step 1: Basic Info**
- Event name (required): text input
- Event type: dropdown (Sports, School, Marathon, Wedding, Other)
- Event date: date picker (single or range)
- Location: text input
- Description: textarea

**Step 2: AI Settings**
- Enable facial recognition: toggle (default: on)
- Enable jersey recognition: toggle (default: off)
- Enable bib/OCR recognition: toggle (default: off)
- Fusion weights (advanced, collapsible):
  - Face: slider (0-100%)
  - Jersey: slider (0-100%)
  - OCR: slider (0-100%)
  - Total must equal 100% (validation)

**Step 3: Gallery Settings**
- Gallery visibility: radio buttons (Public / Private with access code)
- Watermark settings:
  - Upload logo or use text
  - Text watermark: input (default: photographer name)
  - Watermark opacity: slider (20-60%)
- Pricing:
  - Digital download price: input (default: $4.99)
  - Enable print sales: toggle
  - Print pricing: auto-filled from defaults (can override)

**Step 4: Participants (Optional)**
- Upload participant roster: CSV file upload
- Or: "Skip for now" (can add later)
- Request selfies from participants: checkbox

**Footer Buttons:**
- "Back" (goes to previous step, disabled on step 1)
- "Next" (goes to next step)
- "Create Event" (on final step, primary button)
- "Cancel" (secondary)

### Design Requirements

**Technology:**
- React with TypeScript
- Tailwind CSS
- Shadcn UI (Card, Dialog, Tabs, Select, DatePicker)
- Recharts for analytics charts
- Lucide React for icons

**Colors:**
- Same palette (purple primary)
- Status colors:
  - Published: Green (#10b981)
  - Draft: Gray (#6b7280)
  - Processing: Yellow (#f59e0b)
  - Error: Red (#ef4444)

**Responsive Design:**
- Mobile (<768px): Sidebar collapses to hamburger menu, single-column layout
- Tablet (768-1024px): Sidebar visible, 2-column event cards
- Desktop (>1024px): Sidebar + main content + right sidebar

**Animations:**
- Sidebar slide-in on mobile
- Event cards: Hover lift effect
- Metric cards: Count-up animation on load
- Loading states: Skeleton screens for cards

### Functional Requirements

**Dashboard Data Loading:**
- Fetch summary stats: `GET /api/photographer/stats`
- Fetch recent events: `GET /api/photographer/events?limit=10&sort=recent`
- Update stats every 30 seconds (live refresh)
- Real-time activity feed via WebSocket (optional)

**Event Creation:**
1. User clicks "+ Create Event"
2. Modal opens with step 1
3. User completes all steps (validate each step before allowing next)
4. On "Create Event": `POST /api/events` with full event config
5. Show loading state
6. On success: Close modal, show success toast, refresh event list
7. On error: Show error message in modal

**Event Actions:**
- View Gallery: Navigate to `/gallery/{eventCode}` (customer view)
- Analytics: Navigate to `/admin/events/{eventId}/analytics`
- Upload Photos: Navigate to `/admin/events/{eventId}/upload`
- Review Queue: Navigate to `/admin/events/{eventId}/review`
- Edit: Open edit modal (pre-filled with event data)
- Duplicate: Create copy with "(Copy)" appended to name
- Delete: Confirmation dialog → `DELETE /api/events/{eventId}`

**Filters:**
- All: Show all events
- Upcoming: Events with date in future
- Past: Events with date in past
- Draft: Events not yet published
- Client-side filtering (fast) or server-side (if many events)

### Accessibility

- Keyboard navigation for sidebar and event cards
- Focus indicators on all interactive elements
- Screen reader announcements for dynamic content (new events loaded, stats updated)
- ARIA labels for icon-only buttons
- Proper heading hierarchy (h1 for Dashboard, h2 for sections)
- Form validation with clear error messages

### Component Structure

```typescript
<DashboardLayout>
  <Sidebar>
    <UserProfile />
    <Navigation />
    <LogoutButton />
  </Sidebar>

  <MainContent>
    <Header>
      <Greeting />
      <CreateEventButton />
    </Header>

    <MetricsCards>
      <MetricCard title="Total Events" value={24} />
      <MetricCard title="Photos" value={12453} />
      <MetricCard title="Revenue" value="$18,245" trend="+12%" />
      <MetricCard title="Pending Reviews" value={127} />
    </MetricsCards>

    <RecentEvents>
      <FilterBar />
      <EventGrid>
        {events.map(event => (
          <EventCard key={event.id} event={event} />
        ))}
      </EventGrid>
    </RecentEvents>
  </MainContent>

  <QuickActionsPanel />

  {createModalOpen && (
    <CreateEventModal
      onClose={closeModal}
      onSubmit={handleCreateEvent}
    />
  )}
</DashboardLayout>
```

### API Integration (Mock for Now)

```typescript
interface PhotographerStats {
  totalEvents: number;
  totalPhotos: number;
  revenue30Days: number;
  revenueTrend: string; // e.g., "+12%"
  pendingReviews: number;
}

interface Event {
  id: string;
  name: string;
  type: string;
  date: string;
  coverImageUrl: string;
  status: 'draft' | 'published' | 'processing';
  photoCount: number;
  viewCount: number;
  salesCount: number;
  salesRevenue: number;
  pendingReviews: number;
}
```

### Example Text Content

**Greeting:**
- "Welcome back, Marcus!"
- "Good morning, Marcus!"
- "You have 3 events this weekend"

**Metric Cards:**
- "Total Events - 24 active events"
- "Photos Uploaded - 12,453 across all events"
- "Total Revenue - $18,245 in last 30 days (+12% from last month)"
- "Pending Reviews - 127 photos need your review"

**Event Card:**
- "City Soccer Tournament U12"
- "October 20-22, 2025"
- "Published • 1,247 photos • 3,452 views • 89 sales ($421.55)"

**Create Event Modal:**
- "Create New Event"
- "Let's set up your new event. This should only take a minute."
- "Basic Information"
- "AI Recognition Settings"
- "Gallery & Pricing Settings"
- "Participants (Optional)"

**Empty State:**
- "No events yet"
- "Create your first event to start uploading and selling photos"

### Next Steps After This Dashboard

User can navigate to:
- Event upload page (Lovable Prompt 06)
- AI review queue (Lovable Prompt 07)
- Analytics page (Lovable Prompt 08)
- Settings page (future)

---

**Priority:** High (MVP Sprint 6)
**Related User Stories:** US-010, US-050
**Dependencies:** Backend API for events and stats (can mock for now)
**Deliverables:** Full admin dashboard with sidebar navigation, metrics, event cards, create event modal, responsive design
