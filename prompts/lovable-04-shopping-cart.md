# Lovable Prompt 04: Shopping Cart & Checkout

## Prompt for Lovable AI

Create a **Shopping Cart and Checkout** page for Stellar Media Manager where customers can review selected photos, choose digital downloads or prints, and complete purchase.

### Page Structure

**Header:**
- Back to Gallery link (top-left)
- Page title: "Your Cart"
- Item count: "({count} items)"

**Cart Items Section:**
List of cart items, each showing:
- Photo thumbnail (100px square, watermarked)
- Photo details:
  - Event name
  - Photo number: "#23"
  - Date taken: "Oct 20, 2025"
- Product selection dropdown:
  - "Digital Download - $4.99" (default)
  - "4x6 Print - $6.99"
  - "5x7 Print - $9.99"
  - "8x10 Print - $14.99"
  - "11x14 Print - $24.99"
  - "16x20 Print - $39.99"
- Print options (if print selected):
  - Finish: Glossy / Matte / Metallic
  - Quantity selector (1-10)
- Item price (updates based on selection)
- Remove button (trash icon)

**Empty Cart State:**
- Empty cart illustration
- Message: "Your cart is empty"
- "Continue Shopping" button → back to gallery

**Order Summary (Sidebar on Desktop, Below Cart on Mobile):**
- Subtotal: ${subtotal}
- Shipping (if prints ordered): ${shipping} or "FREE for orders over $50"
- Tax (calculated): ${tax}
- Total: ${total}
- "Proceed to Checkout" button (large, purple, prominent)
- Trust badges: Secure checkout, money-back guarantee icons

**Promotional Section (Above Summary):**
- "Special Offer!" badge
- Message: "Buy 5+ digital downloads, get 20% off"
- Or: "Free shipping on print orders over $50"

### Checkout Modal (Appears on "Proceed to Checkout")

**Step 1: Customer Info**
Form fields:
- Email address (required) - "For order confirmation and download links"
- Name (required for prints only)
- Phone (optional) - "For delivery updates"

**Step 2: Shipping Address (If Prints in Cart)**
Form fields:
- Street address
- City
- State / Territory (Australian states dropdown)
- Postcode
- Country (default: Australia)
- "Same as billing" checkbox (checked by default)

**Step 3: Payment**
- Stripe payment element (card input)
- Or PayPal button
- Billing address (if different from shipping)
- Order summary (collapsed, expandable)
- Total: ${total}
- "Place Order" button (disabled until valid payment entered)

**Processing State:**
- Overlay with spinner
- Message: "Processing your order..."
- "Please don't close this window"

**Success State:**
- Replace checkout modal with success screen
- Checkmark icon (large, green)
- "Order Complete!" headline
- Order number: "#ORD-12345"
- For digital downloads:
  - "Your photos are ready!"
  - "Check your email for download links"
  - "Download Now" button (immediate download of all photos)
- For prints:
  - "Your prints are being prepared!"
  - "Estimated delivery: {date}"
  - "Track your order" link
- "Close" button → returns to gallery or home

**Error State:**
- Error icon (red)
- Message: "Payment failed. Please try again."
- Error details (e.g., "Card declined")
- "Try Again" button

### Design Requirements

**Technology:**
- React with TypeScript
- Tailwind CSS
- Shadcn UI (Dialog for checkout modal, Select for dropdowns)
- Stripe Elements for payment
- Lucide React for icons

**Colors:**
- Same palette as other pages
- Success: Green (#10b981)
- Error: Red (#ef4444)
- Warning (shipping threshold): Orange (#f59e0b)

**Responsive Design:**
- Mobile (<768px): Single column, cart items stacked, summary below cart
- Desktop (>768px): Cart items on left (65%), summary sidebar on right (35%)

**Animations:**
- Remove item: Slide-out and fade
- Price updates: Flash/highlight on change
- Checkout modal: Slide-up from bottom (mobile), fade-in center (desktop)

### Functional Requirements

**Cart Management:**
- Load cart from localStorage: `cart: Array<{photoId: string, product: string, finish?: string, quantity: number}>`
- Update cart when product selection changes
- Recalculate totals on any change
- Remove item with confirmation: "Remove this photo from cart?"

**Price Calculation:**
```typescript
const prices = {
  digital: 4.99,
  '4x6': 6.99,
  '5x7': 9.99,
  '8x10': 14.99,
  '11x14': 24.99,
  '16x20': 39.99,
};

const finishPricing = {
  glossy: 0,
  matte: 0,
  metallic: 5.00, // +$5 for metallic
};

const calculateShipping = (items) => {
  const hasPrints = items.some(i => i.product !== 'digital');
  if (!hasPrints) return 0;
  const subtotal = calculateSubtotal(items);
  if (subtotal >= 50) return 0; // Free shipping over $50
  return 9.99; // Flat rate
};

const calculateTax = (subtotal, shipping) => {
  const taxRate = 0.10; // 10% GST (Australian)
  return (subtotal + shipping) * taxRate;
};
```

**Checkout Flow:**
1. User clicks "Proceed to Checkout"
2. Open checkout modal (fullscreen on mobile)
3. Collect email (always required)
4. If prints in cart, collect shipping address
5. Show Stripe payment element
6. On "Place Order":
   - Validate form
   - Submit payment to Stripe
   - Create order in backend: `POST /api/orders`
   - Wait for confirmation
   - Show success or error state

**API Integration (Mock for Now):**
```typescript
interface OrderRequest {
  email: string;
  name?: string;
  phone?: string;
  shippingAddress?: Address;
  items: OrderItem[];
  paymentIntentId: string; // from Stripe
}

interface OrderResponse {
  orderId: string;
  orderNumber: string;
  totalAmount: number;
  downloadLinks?: string[]; // for digital downloads
  estimatedDelivery?: string; // for prints
  trackingUrl?: string;
}
```

**Form Validation:**
- Email: valid email format
- Name: required if prints in cart
- Address: all fields required if prints in cart
- Postcode: Australian format (4 digits)
- Payment: Stripe validates card info

**Promotional Logic:**
- Detect if user has 5+ digital downloads in cart
- Apply 20% discount automatically
- Show savings: "You saved $X.XX!"
- Free shipping if subtotal ≥ $50 (prints only)

### Accessibility

- Keyboard navigation through cart items
- Focus management in checkout modal (trap focus)
- Screen reader announcements for price updates
- ARIA labels for remove buttons ("Remove photo #23 from cart")
- Error messages associated with form fields (ARIA-describedby)
- Clear button states (disabled, loading)

### Component Structure

```typescript
<ShoppingCartPage>
  <Header />

  {cart.length === 0 ? (
    <EmptyCartState />
  ) : (
    <>
      <CartItems>
        {cart.map(item => (
          <CartItem
            key={item.photoId}
            item={item}
            onUpdate={updateItem}
            onRemove={removeItem}
          />
        ))}
      </CartItems>

      <OrderSummary
        subtotal={subtotal}
        shipping={shipping}
        tax={tax}
        total={total}
        onCheckout={openCheckout}
      />
    </>
  )}

  {checkoutOpen && (
    <CheckoutModal
      cart={cart}
      total={total}
      onSubmit={handleCheckout}
      onClose={closeCheckout}
    />
  )}
</ShoppingCartPage>
```

### Example Text Content

**Cart Header:**
- "Your Cart ({count} items)"
- "Continue shopping" link

**Product Options:**
- "Choose your product"
- "Digital Download (instant) - $4.99"
- "8x10 Print (matte finish) - $14.99"

**Shipping Notice:**
- "Prints ship within 3-5 business days"
- "Free shipping on orders over $50!"

**Order Summary:**
- "Order Summary"
- "Subtotal: ${amount}"
- "Shipping: ${amount} (FREE over $50)"
- "Tax (10% GST): ${amount}"
- "Total: ${amount}"

**Checkout Form:**
- "Enter your email to receive your photos"
- "Where should we ship your prints?"
- "Enter your payment information"
- "Place Order - ${total}"

**Success:**
- "Order Complete! 🎉"
- "Order #ORD-{number}"
- "Check your email at {email} for download links"
- "Your prints will arrive by {date}"

**Error:**
- "Payment Failed"
- "Your card was declined. Please try a different payment method."

### Trust & Security

**Trust Badges (In Order Summary):**
- "Secure Checkout" with lock icon
- "100% Satisfaction Guarantee"
- Payment logos: Visa, Mastercard, PayPal, Amex

**Privacy Note:**
- "We never share your information"
- Link to privacy policy

### Next Steps After This Page

After successful order:
- User receives confirmation email with download links
- For digital downloads: can immediately download from success screen
- For prints: receive tracking email when shipped
- Next prompt: Admin Dashboard for photographers (Lovable Prompt 05)

---

**Priority:** High (MVP Sprint 5)
**Related User Stories:** US-040, US-041, US-042
**Dependencies:** Stripe integration, backend order API (can mock for now)
**Deliverables:** Shopping cart with item management, checkout modal with Stripe integration, order confirmation, responsive design
