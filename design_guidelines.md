# Design Guidelines for Hwalik (حوليك)

## Design Approach
**Selected Approach:** Design System with Marketplace References
- **Base System:** Material Design for RTL-friendly components and clear visual hierarchy
- **References:** Airbnb (trust-building through visual design), TaskRabbit (service categories), Noon.com (Saudi e-commerce leader for local market patterns)
- **Rationale:** Service marketplaces require both trust-building aesthetics and functional clarity. Material Design provides excellent RTL support while marketplace patterns establish credibility.

## Core Design Elements

### A. Color Palette

**Light Mode:**
- Primary: 210 85% 45% (Deep blue - trust and professionalism)
- Primary Variant: 210 70% 35% (Darker blue for emphasis)
- Secondary: 165 65% 50% (Teal - service completion, success)
- Background: 0 0% 98% (Warm white)
- Surface: 0 0% 100% (Pure white for cards)
- Text Primary: 220 15% 20% (Dark gray-blue)
- Text Secondary: 220 10% 50% (Medium gray)

**Dark Mode:**
- Primary: 210 75% 55% (Lighter blue)
- Background: 220 15% 12% (Dark blue-gray)
- Surface: 220 12% 16% (Card surfaces)
- Text Primary: 0 0% 95% (Off-white)
- Border: 220 10% 25% (Subtle dividers)

### B. Typography
- **Primary Font:** 'Cairo' (excellent Arabic font via Google Fonts) - weights 400, 600, 700
- **Headings:** Cairo Bold (700) - sizes 32px (h1), 24px (h2), 20px (h3)
- **Body:** Cairo Regular (400) - 16px base, 18px for important content
- **Subtext:** Cairo Regular (400) - 14px for metadata, labels

### C. Layout System
**Spacing Units:** Tailwind spacing of 3, 4, 6, 8, 12, 16 for consistent rhythm
- Component padding: p-4 to p-6
- Section spacing: py-12 to py-16
- Card gaps: gap-6
- Max content width: max-w-6xl for main content areas

### D. Component Library

**Navigation (RTL)**
- Top navbar with logo on right, main navigation center-right, user menu left
- Sticky header with shadow on scroll
- Mobile: Hamburger menu on left (RTL pattern)

**Hero Section**
- Full-width hero with background image showing Saudi home/technician at work
- Overlay gradient (from primary color at 60% opacity to transparent)
- Right-aligned content (RTL): Large heading, subtitle, dual CTA buttons
- Search bar for service types prominently placed
- Height: 70vh on desktop, 60vh on mobile

**Service Category Cards**
- Grid layout: 4 columns desktop (grid-cols-4), 2 columns tablet (md:grid-cols-2), 1 column mobile
- Each card: Icon at top, service name, technician count
- Rounded corners (rounded-lg), subtle shadow, hover lift effect
- Icons: Material Icons via CDN

**Technician Profile Cards**
- Horizontal layout: Avatar (circular, 80px) on right, details on left (RTL)
- Star rating, service type badge, price range
- "طلب خدمة" (Request Service) button - secondary color
- Card spacing: p-6, subtle border

**Request Status Section**
- List view with status badges (معلقة/قيد المراجعة/مقبولة/مرفوضة)
- Color coding: Gray (pending), Blue (reviewing), Green (accepted), Red (rejected)
- Timestamp and technician info on each request card

**Forms (User Registration, Service Request)**
- Full-width inputs with RTL text alignment
- Floating labels (Material Design pattern)
- Radio buttons for user type selection (large, clear)
- Dropdowns for service categories
- Primary button for submit, outline button for cancel

**Footer**
- Three-column layout (desktop): Company info, Quick links, Contact
- Saudi-specific: Include Absher integration mention, Commercial registry
- Social media icons (aligned right for RTL)
- Copyright centered

### E. Images
**Hero Section:**
- Large hero image: Professional Saudi technician with tools or happy family in modern Saudi home
- Dimensions: 1920x800px, optimized
- Placement: Full-width background with overlay

**Service Categories:**
- Icon-based (Material Icons): plumbing, electrical, cleaning, AC, painting, carpentry
- Color: Primary color fills

**Technician Profiles:**
- Circular avatar placeholders (80x80px)
- Default avatar if no image provided

**Trust Indicators:**
- Small badge icons: Verified, Top-rated, Fast response (placed near technician names)

## RTL-Specific Patterns
- All text right-aligned by default
- Flex layouts use flex-row-reverse
- Grid starts from right
- Floating action buttons positioned bottom-left (reversed)
- Navigation animations slide from right
- Form validation messages appear on right side of inputs

## Key Page Structures

**Homepage:** Hero with search → Service categories (4-col grid) → How it works (3 steps, horizontal) → Featured technicians → Trust section → CTA → Footer

**Technicians Listing:** Filters sidebar (right side in RTL) → Grid of technician cards (3-col) → Pagination

**Service Request Page:** Centered form (max-w-2xl) → Service details, date/time picker, description textarea, submit

**Dashboard (Client):** Header with stats → Active requests table → Past services history

**Dashboard (Technician):** Pending requests (cards with accept/reject) → Upcoming services → Earnings summary