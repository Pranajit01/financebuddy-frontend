# Financebuddy — Architecture Documentation

## 📐 System Architecture

### High-Level Overview

```
┌─────────────────────────────────────────────────────────┐
│                    Landing Page (Phase 1)                │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐        │
│  │   Navbar   │  │    Hero    │  │  Features  │        │
│  └────────────┘  └────────────┘  └────────────┘        │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐        │
│  │ How It     │  │Testimonials│  │    CTA     │        │
│  │ Works      │  │            │  │            │        │
│  └────────────┘  └────────────┘  └────────────┘        │
│  ┌────────────┐                                         │
│  │   Footer   │  Background: Financial Ecosystem        │
│  └────────────┘                                         │
└─────────────────────────────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────┐
│              Future: Full App (Phase 2)                  │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐        │
│  │ Dashboard  │  │Transactions│  │  Budgets   │        │
│  └────────────┘  └────────────┘  └────────────┘        │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐        │
│  │ Analytics  │  │  Settings  │  │    Auth    │        │
│  └────────────┘  └────────────┘  └────────────┘        │
│                                                          │
│  Backend: Supabase (Auth + PostgreSQL + Realtime)       │
└─────────────────────────────────────────────────────────┘
```

---

## 🏗️ Component Architecture

### Component Hierarchy

```
App
├── FinancialEcosystem (Animated Background)
├── Navbar
│   ├── Logo
│   ├── Navigation Links
│   ├── CTA Button
│   └── Mobile Menu
├── Hero
│   ├── Badge
│   ├── Headline
│   ├── Subheadline
│   ├── CTA Buttons
│   ├── Social Proof
│   └── Dashboard Preview
├── Features
│   └── FeatureCard (x6)
│       ├── Icon
│       ├── Title
│       └── Description
├── HowItWorks
│   └── Step (x4)
│       ├── Number
│       ├── Title
│       └── Description
├── Testimonials
│   └── TestimonialCard (x3)
│       ├── Quote
│       ├── Rating
│       └── Author
├── CTA
│   ├── Headline
│   ├── Description
│   ├── Perks
│   └── CTA Buttons
└── Footer
    ├── Logo & Tagline
    ├── Link Sections
    ├── Social Links
    └── Copyright
```

---

## 🎨 Design System

### Color System

```typescript
// Primary Palette
brand: {
  50:  '#eff6ff',  // Lightest
  100: '#dbeafe',
  200: '#bfdbfe',
  300: '#93c5fd',
  400: '#60a5fa',
  500: '#3b82f6',  // Primary
  600: '#2563eb',  // Primary hover
  700: '#1d4ed8',
  800: '#1e40af',
  900: '#1e3a8a',  // Darkest
}

// Semantic Colors
success: green-500  (#22c55e)
warning: amber-500  (#f59e0b)
error:   red-500    (#ef4444)
info:    blue-500   (#3b82f6)
```

### Typography Scale

```
Display:  60px / 72px / -2% / 800
H1:       36px / 44px / -1% / 700
H2:       30px / 38px / -1% / 700
H3:       24px / 32px / -0.5% / 600
Body:     16px / 24px / 0% / 400
Small:    14px / 20px / 0% / 400
```

### Spacing Scale

```
Base: 4px

0:  0px
1:  4px
2:  8px
3:  12px
4:  16px   (default)
6:  24px   (card padding)
8:  32px
12: 48px   (section gaps)
16: 64px
20: 80px
24: 96px   (hero spacing)
```

---

## 🎬 Animation System

### "Living Financial Ecosystem" Background

#### Layer 1: Background Grid
```typescript
Purpose: Foundation, stability
Animation: Slow vertical scroll (60s)
Opacity: 3% (light), 5% (dark)
Performance: Static on mobile
```

#### Layer 2: Flow Network (SVG Paths)
```typescript
Elements: 5 curved paths
Types:
  - Income flows (green → blue)
  - Expense flows (blue → red)
  - Savings flows (blue → violet)

Animation:
  - Stroke-dasharray: 20 80
  - Stroke-dashoffset: 0 → -100
  - Duration: 8-15 seconds
  - Easing: linear
  - Loop: infinite
```

#### Layer 3: Nodes
```typescript
Elements: 6 glowing circles
Types:
  - Income nodes (green, 24px)
  - Expense nodes (red, 16-18px)
  - Savings nodes (blue, 20px)
  - Goal nodes (violet, 22px)

Animation:
  - Scale: 1 → 1.3 → 1
  - Opacity: 0.4 → 0.7 → 0.4
  - Duration: 3-5 seconds
  - Easing: easeInOut
```

#### Layer 4: Particles
```typescript
Elements: 15 floating dots
Animation:
  - Y: 0 → -30 → 0
  - X: random drift
  - Opacity: 0.2 → 0.5 → 0.2
  - Duration: 4-8 seconds
```

#### Layer 5: Gradient Orbs
```typescript
Elements: 2 large blurred circles
Animation:
  - Position: circular motion
  - Scale: 1 → 1.2 → 1
  - Duration: 20-25 seconds
  - Easing: easeInOut
```

### Component Animations

```typescript
// Scroll-triggered reveals
initial: { opacity: 0, y: 32 }
animate: { opacity: 1, y: 0 }
duration: 500ms
easing: ease-out
trigger: 30% visible

// Hover effects
Cards: translateY(-4px) + shadow-lg
Buttons: translateY(-1px) + shadow-md
Icons: scale(1.1) + rotate(5deg)

// Stagger animations
delay: index * 80ms
```

---

## 📱 Responsive Strategy

### Breakpoints

```typescript
sm:  640px   // Large phones
md:  768px   // Tablets
lg:  1024px  // Laptops
xl:  1280px  // Desktops
2xl: 1536px  // Large screens
```

### Layout Adaptations

```
Mobile (< 768px):
├── Single column
├── Stacked elements
├── Hamburger menu
├── Full-width buttons
├── Simplified animations
└── Hidden background complexity

Tablet (768px - 1023px):
├── 2-column grids
├── Horizontal navigation
├── Side-by-side CTAs
├── Moderate animations
└── Simplified background

Desktop (1024px+):
├── 3-column grids
├── Full navigation
├── Parallax effects
├── Full animations
└── Complete background system
```

---

## ⚡ Performance Strategy

### Bundle Optimization

```
Target Sizes:
├── Initial bundle: < 200KB
├── Vendor bundle: < 150KB
├── Component chunks: < 50KB each
└── Total (gzipped): < 400KB

Techniques:
├── Code splitting by route
├── Tree-shaking unused code
├── Dynamic imports for heavy components
├── Lazy loading images
└── Preloading critical assets
```

### Animation Performance

```
GPU-Accelerated Properties:
✅ transform
✅ opacity
✅ filter (blur)

Avoid:
❌ width/height
❌ top/left/right/bottom
❌ margin/padding
❌ background-position

Optimization:
├── will-change: transform
├── transform: translateZ(0)
├── Throttle scroll events (60fps)
└── Pause off-screen animations
```

### Loading Strategy

```
Critical Path:
1. HTML (inline critical CSS)
2. Fonts (preload Inter)
3. JavaScript (defer non-critical)
4. Images (lazy load below fold)
5. Animations (progressive enhancement)

Metrics:
├── FCP: < 2s
├── LCP: < 2.5s
├── TTI: < 3s
├── CLS: < 0.1
└── FID: < 100ms
```

---

## 🔮 Future Architecture (Phase 2)

### State Management

```typescript
// Global UI State (Zustand)
interface UIStore {
  theme: 'light' | 'dark'
  sidebarOpen: boolean
  activeModal: string | null
}

// Server State (React Query)
useQuery(['transactions', userId])
useQuery(['budgets', userId])
useQuery(['analytics', userId, dateRange])

// Form State (React Hook Form)
const { register, handleSubmit } = useForm()
```

### Routing Structure

```
/ (public)
├── /login
├── /signup
└── /reset-password

/app (protected)
├── /app/dashboard
├── /app/transactions
│   └── /app/transactions/:id
├── /app/budgets
│   └── /app/budgets/:id
├── /app/analytics
└── /app/settings
    ├── /app/settings/profile
    └── /app/settings/security
```

### Database Schema

```sql
-- Users (managed by Supabase Auth)
users (
  id uuid PRIMARY KEY,
  email text UNIQUE,
  created_at timestamp
)

-- Profiles (1:1 with users)
profiles (
  id uuid PRIMARY KEY REFERENCES users(id),
  name text,
  avatar_url text,
  currency text DEFAULT 'USD',
  created_at timestamp
)

-- Transactions
transactions (
  id uuid PRIMARY KEY,
  user_id uuid REFERENCES users(id),
  amount numeric,
  type enum('income', 'expense'),
  category text,
  description text,
  date date,
  created_at timestamp
)

-- Budgets
budgets (
  id uuid PRIMARY KEY,
  user_id uuid REFERENCES users(id),
  category text,
  amount numeric,
  period enum('monthly', 'weekly'),
  start_date date,
  end_date date
)

-- Row Level Security (RLS)
ALTER TABLE transactions ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Users can view own transactions"
  ON transactions FOR SELECT
  USING (auth.uid() = user_id);
```

### API Layer

```typescript
// Service Layer
export const transactionService = {
  getAll: (filters) => supabase.from('transactions').select('*'),
  getById: (id) => supabase.from('transactions').select('*').eq('id', id),
  create: (data) => supabase.from('transactions').insert(data),
  update: (id, data) => supabase.from('transactions').update(data).eq('id', id),
  delete: (id) => supabase.from('transactions').delete().eq('id', id),
}

// React Query Hooks
const useTransactions = () => {
  return useQuery({
    queryKey: ['transactions'],
    queryFn: () => transactionService.getAll(),
  })
}

const useCreateTransaction = () => {
  return useMutation({
    mutationFn: transactionService.create,
    onSuccess: () => {
      queryClient.invalidateQueries(['transactions'])
    },
  })
}
```

---

## 🔒 Security Considerations

### Frontend Security

```typescript
// Environment Variables
VITE_SUPABASE_URL=xxx        // Safe to expose
VITE_SUPABASE_ANON_KEY=xxx   // Safe to expose (RLS protects data)

// Never expose:
SUPABASE_SERVICE_KEY         // Bypasses RLS!

// Input Validation
- Client-side: immediate feedback
- Server-side: Supabase RLS + constraints
- Sanitize: prevent XSS
- Type safety: TypeScript

// Authentication
- Session: localStorage (Supabase default)
- Refresh: automatic (30 days)
- HTTPS: enforce in production
- CSRF: built into Supabase
```

### Database Security

```sql
-- Row Level Security (RLS)
-- Users can only access their own data

CREATE POLICY "Users can view own data"
  ON transactions FOR SELECT
  USING (auth.uid() = user_id);

CREATE POLICY "Users can insert own data"
  ON transactions FOR INSERT
  WITH CHECK (auth.uid() = user_id);

-- Prevents data leaks even if frontend is compromised
```

---

## 📊 Monitoring & Analytics

### Performance Monitoring

```typescript
// Web Vitals
import { getCLS, getFID, getFCP, getLCP, getTTFB } from 'web-vitals'

getCLS(console.log)  // Cumulative Layout Shift
getFID(console.log)  // First Input Delay
getFCP(console.log)  // First Contentful Paint
getLCP(console.log)  // Largest Contentful Paint
getTTFB(console.log) // Time to First Byte
```

### Error Tracking

```typescript
// Sentry (recommended)
import * as Sentry from '@sentry/react'

Sentry.init({
  dsn: 'your-sentry-dsn',
  environment: import.meta.env.MODE,
  tracesSampleRate: 1.0,
})
```

### User Analytics

```typescript
// Plausible (privacy-friendly)
<script defer data-domain="financebuddy.io" src="https://plausible.io/js/script.js"></script>

// Track events
window.plausible('Signup', { props: { method: 'email' } })
```

---

## 🚀 Deployment Strategy

### Build Process

```bash
# 1. Install dependencies
npm install

# 2. Run tests
npm run lint
npx tsc --noEmit

# 3. Build for production
npm run build

# 4. Preview build
npm run preview

# 5. Deploy
vercel deploy --prod
```

### Environment Setup

```
Development:
├── .env.local (local overrides)
├── Hot reload enabled
├── Source maps enabled
└── Debug mode on

Production:
├── .env.production
├── Minified bundles
├── Source maps disabled
├── Error tracking enabled
└── Analytics enabled
```

### CI/CD Pipeline

```yaml
# .github/workflows/deploy.yml
name: Deploy
on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
      - run: npm install
      - run: npm run lint
      - run: npm run build
      - uses: amondnet/vercel-action@v20
```

---

## 📚 Technology Decisions

### Why React?
- Component-based architecture
- Large ecosystem
- Excellent TypeScript support
- Industry standard

### Why Tailwind CSS?
- Utility-first (fast development)
- Small bundle size (tree-shaking)
- Consistent design system
- No CSS conflicts

### Why Framer Motion?
- Declarative animations
- React-friendly API
- Powerful gesture support
- Layout animations

### Why Vite?
- Fast HMR (< 100ms)
- Modern build tool
- Optimized production builds
- Native ESM support

### Why Supabase? (Phase 2)
- Auth + Database + Realtime in one
- PostgreSQL (powerful, scalable)
- Row Level Security (secure by default)
- Generous free tier

---

This architecture is designed to be **scalable**, **maintainable**, and **performant** for a production SaaS application.
