# Lovable AI Prompts
## Stellar Media Manager Frontend

This folder contains detailed prompts for generating frontend components using Lovable AI (lovable.dev).

## Prompt Organization

Prompts are numbered sequentially and designed to be executed in order for optimal results:

### Customer-Facing Pages (MVP Priority)
1. **[lovable-01-landing-page.md](lovable-01-landing-page.md)** - Entry point with gallery code input and discovery paths
2. **[lovable-02-selfie-upload.md](lovable-02-selfie-upload.md)** - AI-powered selfie matching interface
3. **[lovable-03-photo-gallery.md](lovable-03-photo-gallery.md)** - Photo grid with lightbox and favoriting
4. **[lovable-04-shopping-cart.md](lovable-04-shopping-cart.md)** - Cart management and Stripe checkout

### Admin/Photographer Pages (MVP Priority)
5. **[lovable-05-photographer-dashboard.md](lovable-05-photographer-dashboard.md)** - Main admin dashboard with event management
6. **lovable-06-photo-upload.md** - Bulk photo upload interface (TBD)
7. **lovable-07-ai-review-queue.md** - Manual review interface for AI matches (TBD)
8. **lovable-08-analytics.md** - Event analytics and reporting (TBD)

### Additional Pages (Post-MVP)
9. **lovable-09-settings.md** - Account settings and preferences (TBD)
10. **lovable-10-print-products.md** - Print catalog and customization (Phase 2)

## How to Use These Prompts

### With Lovable AI (lovable.dev)

1. **Start a New Project:**
   - Go to lovable.dev
   - Create new project: "Stellar Media Manager"
   - Choose React + TypeScript + Tailwind CSS

2. **Execute Prompts Sequentially:**
   - Copy the entire content of `lovable-01-landing-page.md`
   - Paste into Lovable AI chat
   - Review generated code and preview
   - Test functionality
   - Move to next prompt

3. **Iterate and Refine:**
   - If component needs adjustments, provide feedback to Lovable
   - Ask for specific changes (e.g., "Make the button larger", "Change color scheme")
   - Lovable will update the code in real-time

4. **Export Code:**
   - Once satisfied with all components, export the full codebase
   - Integrate with backend API endpoints (developed separately in Go)

### Prompt Execution Tips

**Dependencies Between Prompts:**
- Prompts 1-4 form the customer journey (complete this first)
- Prompts 5-8 form the admin dashboard (can be done in parallel if multiple developers)
- Each prompt references previous components (e.g., Prompt 03 uses routes from Prompt 01)

**Customization Guidance:**
- Colors, fonts, and branding are specified in each prompt
- Modify the design requirements section if you want different styling
- Consistent design system across all prompts ensures cohesive UI

**Mock Data:**
- All prompts include API integration sections with TypeScript interfaces
- Use mock data initially for rapid prototyping
- Replace with real API calls when backend is ready

## Technical Stack

**Frontend Framework:**
- React 18+
- TypeScript
- Vite (build tool)

**UI Libraries:**
- Tailwind CSS (utility-first styling)
- Shadcn UI (accessible component primitives)
- Lucide React (icon system)

**State Management:**
- React Context for global state (auth, cart)
- Local state with useState for component-specific data
- localStorage for cart persistence and favorites

**Additional Libraries:**
- React Router (navigation)
- Stripe React (payments)
- Framer Motion (animations, optional)
- React Dropzone (file uploads)
- Recharts (analytics charts)

## Design System

**Color Palette:**
- Primary: Purple gradient (#667eea to #764ba2)
- Accent: Orange (#f59e0b)
- Success: Green (#10b981)
- Error: Red (#ef4444)
- Info: Blue (#3b82f6)
- Background: Light gray (#f3f4f6)
- Text: Dark gray (#1f2937)

**Typography:**
- Font: Inter (Google Fonts)
- Headings: Bold (700)
- Body: Regular (400)
- Small text: 14px
- Body text: 16px
- Headings: 24px-48px

**Spacing:**
- Base unit: 4px (Tailwind default)
- Container max-width: 1280px
- Section padding: 64px vertical, 16px horizontal (mobile)

**Breakpoints (Tailwind defaults):**
- sm: 640px
- md: 768px
- lg: 1024px
- xl: 1280px
- 2xl: 1536px

## API Integration Checklist

When integrating frontend with backend APIs:

1. **Update API Base URL:**
   - Development: `http://localhost:8080/api`
   - Production: `https://api.stellarmedia.com`

2. **Replace Mock Data:**
   - Replace mock fetch functions with real API calls
   - Use axios or fetch for HTTP requests
   - Handle loading, error, and success states

3. **Authentication:**
   - Implement JWT token storage (localStorage or httpOnly cookies)
   - Add token to Authorization header for protected routes
   - Handle 401 unauthorized responses (redirect to login)

4. **Error Handling:**
   - Network errors: Show "Connection lost" message
   - 4xx errors: Show user-friendly error messages
   - 5xx errors: Show "Something went wrong" with retry option

5. **Environment Variables:**
   - Create `.env` file:
     ```
     VITE_API_BASE_URL=http://localhost:8080/api
     VITE_STRIPE_PUBLIC_KEY=pk_test_xxx
     ```

## Quality Assurance

**Testing Checklist for Each Component:**
- ✅ Desktop responsiveness (1920px, 1440px, 1280px)
- ✅ Tablet responsiveness (768px, 1024px)
- ✅ Mobile responsiveness (375px, 414px)
- ✅ Keyboard navigation works
- ✅ Screen reader accessibility (test with VoiceOver/NVDA)
- ✅ Form validation displays correctly
- ✅ Loading states appear
- ✅ Error states display user-friendly messages
- ✅ Animations perform smoothly (60fps)
- ✅ Images lazy load
- ✅ No console errors or warnings

**Browser Compatibility:**
- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)
- Mobile Safari (iOS 14+)
- Mobile Chrome (Android 10+)

## Deployment

**Build for Production:**
```bash
npm run build
# or
yarn build
```

**Deploy to:**
- Vercel (recommended for frontend)
- Netlify
- AWS S3 + CloudFront
- Self-hosted with Nginx

**Environment Setup:**
- Set production environment variables
- Configure CDN for static assets
- Enable gzip compression
- Set cache headers for images (1 year)

## Related Documentation

- [Product Requirements Document](../project-design/PRD.md)
- [User Stories](../user-stories/README.md)
- [User Journey Map](../project-design/user-journey.md)
- [API Documentation](TBD - Backend Go API docs)

## Support

For questions or issues with these prompts:
- Review the PRD for detailed requirements
- Check user stories for acceptance criteria
- Consult user journey map for flow context

---

**Created:** October 22, 2025
**Total Prompts:** 10 (5 completed, 5 TBD)
**Estimated Development Time:** 6-8 weeks (with Lovable AI assistance)
**Target:** MVP (Phase 1) completion
