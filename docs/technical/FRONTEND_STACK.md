# COOKie Frontend Technology Stack

> **Version**: 1.0
> **Last Updated**: 2025-10-15
> **Status**: Approved for MVP Development
> **Target**: Next.js 14 + ASP.NET Core 8 Backend

---

## Overview

This document defines the complete frontend technology stack for the COOKie MVP. All decisions prioritize **solo developer velocity**, **modern best practices**, and **maintainability** for future team scaling.

---

## Core Stack

### Framework & Runtime

| Technology | Version | Purpose | Justification |
|------------|---------|---------|---------------|
| **Next.js** | 14.x (App Router) | React framework with SSR/SSG | SEO-critical for recipe pages, built-in optimization |
| **React** | 18.x | UI library | Industry standard, massive ecosystem |
| **TypeScript** | 5.x (strict mode) | Type safety | Catch bugs at compile-time, better DX |
| **Node.js** | 20.x LTS | Runtime | Stable LTS, required for Next.js |

**Key Configuration**:
```json
{
  "compilerOptions": {
    "strict": true,
    "target": "ES2022",
    "module": "ESNext",
    "moduleResolution": "bundler",
    "jsx": "preserve",
    "incremental": true,
    "paths": {
      "@/*": ["./src/*"]
    }
  }
}
```

---

## State Management

### Global State: Zustand

**Version**: 4.x
**Use Cases**:
- User preferences (theme, language)
- App-wide UI state (sidebar open/close)
- Shopping cart (future feature)

**Why Zustand?**
- ✅ Minimal boilerplate (~50 lines vs 200+ for Redux)
- ✅ 1KB bundle size
- ✅ Perfect for solo dev, easy to scale
- ✅ DevTools support
- ✅ Works seamlessly with Next.js 14

**Example Store**:
```typescript
// src/stores/useUserPreferencesStore.ts
import { create } from 'zustand'
import { persist } from 'zustand/middleware'

interface UserPreferencesState {
  theme: 'light' | 'dark'
  setTheme: (theme: 'light' | 'dark') => void
}

export const useUserPreferencesStore = create<UserPreferencesState>()(
  persist(
    (set) => ({
      theme: 'light',
      setTheme: (theme) => set({ theme }),
    }),
    { name: 'user-preferences' }
  )
)
```

**Migration Path**: If team grows or complexity increases → Redux Toolkit (well-documented migration).

---

### Server State: TanStack Query (React Query)

**Version**: 5.x
**Use Cases**:
- Fetching recipes from API
- User profile data
- Favorites/ratings
- Search results

**Why TanStack Query?**
- ✅ **Automatic caching** - no manual cache management
- ✅ **Background refetching** - data always fresh
- ✅ **Loading/error states** - built-in
- ✅ **Optimistic updates** - instant UI feedback
- ✅ **Pagination/infinite scroll** - first-class support
- ✅ **Request deduplication** - prevents duplicate API calls
- ✅ Industry standard (used by Netflix, Google)

**Configuration**:
```typescript
// src/lib/queryClient.ts
import { QueryClient } from '@tanstack/react-query'

export const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      staleTime: 1000 * 60 * 5, // 5 minutes
      gcTime: 1000 * 60 * 30, // 30 minutes (was cacheTime in v4)
      retry: 1,
      refetchOnWindowFocus: false,
    },
  },
})
```

**Example Hook**:
```typescript
// src/hooks/api/useRecipes.ts
import { useQuery } from '@tanstack/react-query'
import { recipesApi } from '@/lib/api/recipes'

export function useRecipes(filters?: RecipeFilters) {
  return useQuery({
    queryKey: ['recipes', filters],
    queryFn: () => recipesApi.getRecipes(filters),
    staleTime: 1000 * 60 * 10, // 10 min for recipes
  })
}
```

---

### Context API (React Context)

**Use Cases** (limited):
- Authentication state (JWT token, user object)
- Theme provider (if not using Zustand)
- Localization (i18n)

**Why Limited Use?**
- ❌ Re-renders entire subtree (performance issue)
- ✅ Good for rarely-changing data (auth, theme)

---

## Data Fetching & HTTP

### HTTP Client: Axios

**Version**: 1.x
**Why Axios?**
- ✅ Request/response interceptors (auth tokens)
- ✅ Better error handling than fetch
- ✅ Automatic JSON transformation
- ✅ Browser + Node.js support
- ✅ Well-integrated with TanStack Query

**Configuration**:
```typescript
// src/lib/api/axiosClient.ts
import axios from 'axios'

export const axiosClient = axios.create({
  baseURL: process.env.NEXT_PUBLIC_API_BASE_URL,
  timeout: 10000,
  headers: {
    'Content-Type': 'application/json',
  },
})

// Request interceptor: add JWT token
axiosClient.interceptors.request.use((config) => {
  const token = localStorage.getItem('access_token')
  if (token) {
    config.headers.Authorization = `Bearer ${token}`
  }
  return config
})

// Response interceptor: handle 401, refresh token
axiosClient.interceptors.response.use(
  (response) => response,
  async (error) => {
    if (error.response?.status === 401) {
      // Refresh token logic here
    }
    return Promise.reject(error)
  }
)
```

---

## UI & Styling

### CSS Framework: TailwindCSS

**Version**: 3.x
**Configuration**:
- Custom color palette (brand colors)
- Custom breakpoints for recipe cards
- Dark mode support

**Why TailwindCSS?**
- ✅ Utility-first → rapid prototyping
- ✅ No CSS file management
- ✅ Tree-shaking → small bundle
- ✅ Responsive design built-in
- ✅ Dark mode support

**Config Highlights**:
```javascript
// tailwind.config.js
module.exports = {
  darkMode: 'class',
  theme: {
    extend: {
      colors: {
        primary: {
          50: '#fff7ed',
          500: '#f97316', // Orange for food
          900: '#7c2d12',
        },
        secondary: {
          500: '#10b981', // Green for healthy
        },
      },
      fontFamily: {
        sans: ['Inter', 'system-ui', 'sans-serif'],
      },
    },
  },
}
```

---

### Component Library: Custom Components

**Approach**: Build all components from scratch using TailwindCSS
**Primitives**: Headless UI (for accessibility) + Radix UI (optional, for complex interactions)

**Why Custom Components?**
- ✅ **Full control** - complete ownership, no external dependencies
- ✅ **Learning opportunity** - understand component internals
- ✅ **Lightweight** - only what you need, no unused code
- ✅ **Unique design** - not "another shadcn/ui site"
- ✅ **Flexibility** - adapt to exact MVP needs

**Optional Accessibility Helpers**:
```bash
# Install only for complex interactive components (dropdowns, modals, etc.)
npm install @headlessui/react        # Unstyled, accessible UI components
npm install @radix-ui/react-dialog   # If you need modals/dialogs
npm install @radix-ui/react-dropdown-menu  # For dropdowns
```

**Why Headless UI/Radix UI for complex components?**
- ✅ Handle keyboard navigation, focus management, ARIA attributes
- ✅ Still write your own styles with Tailwind
- ✅ Save time on accessibility implementation
- ❌ Don't use for simple components (Button, Input, Card)

**Component Structure**:
```
src/
├── components/
│   ├── ui/              # Base UI components (custom-built)
│   │   ├── Button.tsx
│   │   ├── Input.tsx
│   │   ├── Card.tsx
│   │   ├── Badge.tsx
│   │   ├── Modal.tsx          # Using Headless UI internally
│   │   ├── Dropdown.tsx       # Using Headless UI internally
│   │   └── Toast.tsx
│   ├── recipes/         # Recipe-specific components
│   │   ├── RecipeCard.tsx
│   │   ├── RecipeGrid.tsx
│   │   └── RecipeFilters.tsx
│   └── layout/          # Layout components
│       ├── Header.tsx
│       ├── Footer.tsx
│       └── Sidebar.tsx
```

**Example Custom Button**:
```typescript
// src/components/ui/Button.tsx
import { cn } from '@/lib/utils'
import { ButtonHTMLAttributes, forwardRef } from 'react'

interface ButtonProps extends ButtonHTMLAttributes<HTMLButtonElement> {
  variant?: 'primary' | 'secondary' | 'outline' | 'ghost'
  size?: 'sm' | 'md' | 'lg'
}

export const Button = forwardRef<HTMLButtonElement, ButtonProps>(
  ({ className, variant = 'primary', size = 'md', ...props }, ref) => {
    return (
      <button
        ref={ref}
        className={cn(
          'rounded-lg font-medium transition-colors focus:outline-none focus:ring-2',
          {
            'bg-primary-500 text-white hover:bg-primary-600': variant === 'primary',
            'bg-gray-200 text-gray-900 hover:bg-gray-300': variant === 'secondary',
            'border border-gray-300 hover:bg-gray-100': variant === 'outline',
            'hover:bg-gray-100': variant === 'ghost',
          },
          {
            'px-3 py-1.5 text-sm': size === 'sm',
            'px-4 py-2 text-base': size === 'md',
            'px-6 py-3 text-lg': size === 'lg',
          },
          className
        )}
        {...props}
      />
    )
  }
)

Button.displayName = 'Button'
```

**Example Modal (using Headless UI)**:
```typescript
// src/components/ui/Modal.tsx
import { Dialog, Transition } from '@headlessui/react'
import { Fragment, ReactNode } from 'react'
import { X } from 'lucide-react'

interface ModalProps {
  open: boolean
  onClose: () => void
  title?: string
  children: ReactNode
}

export function Modal({ open, onClose, title, children }: ModalProps) {
  return (
    <Transition appear show={open} as={Fragment}>
      <Dialog as="div" className="relative z-50" onClose={onClose}>
        <Transition.Child
          as={Fragment}
          enter="ease-out duration-300"
          enterFrom="opacity-0"
          enterTo="opacity-100"
          leave="ease-in duration-200"
          leaveFrom="opacity-100"
          leaveTo="opacity-0"
        >
          <div className="fixed inset-0 bg-black/50" />
        </Transition.Child>

        <div className="fixed inset-0 overflow-y-auto">
          <div className="flex min-h-full items-center justify-center p-4">
            <Transition.Child
              as={Fragment}
              enter="ease-out duration-300"
              enterFrom="opacity-0 scale-95"
              enterTo="opacity-100 scale-100"
              leave="ease-in duration-200"
              leaveFrom="opacity-100 scale-100"
              leaveTo="opacity-0 scale-95"
            >
              <Dialog.Panel className="w-full max-w-md rounded-2xl bg-white p-6 shadow-xl">
                <div className="flex items-start justify-between">
                  {title && (
                    <Dialog.Title className="text-lg font-semibold">
                      {title}
                    </Dialog.Title>
                  )}
                  <button
                    onClick={onClose}
                    className="rounded-lg p-1 hover:bg-gray-100"
                  >
                    <X className="h-5 w-5" />
                  </button>
                </div>
                <div className="mt-4">{children}</div>
              </Dialog.Panel>
            </Transition.Child>
          </div>
        </div>
      </Dialog>
    </Transition>
  )
}
```

---

### Icons: Lucide React

**Version**: 0.x
**Why Lucide?**
- ✅ 1000+ icons, beautiful design
- ✅ Tree-shakeable (only import icons you use)
- ✅ Fork of Feather Icons (maintained actively)
- ✅ Perfect match for shadcn/ui

```typescript
import { Heart, Search, User, ChefHat } from 'lucide-react'

<Heart className="w-5 h-5 text-red-500" />
```

---

## Forms & Validation

### React Hook Form

**Version**: 7.x
**Why React Hook Form?**
- ✅ **Best performance** - uncontrolled inputs, minimal re-renders
- ✅ **Small bundle** - 9KB gzipped
- ✅ **Great DX** - simple API, TypeScript support
- ✅ **Built-in validation** - integrates with Zod perfectly

### Zod (Schema Validation)

**Version**: 3.x
**Why Zod?**
- ✅ **TypeScript-first** - infer types from schemas
- ✅ **Runtime validation** - catch bad API responses
- ✅ **Composable** - reuse schemas across frontend/backend
- ✅ **Error messages** - clear, customizable

**Example Form**:
```typescript
// src/schemas/recipeSchema.ts
import { z } from 'zod'

export const recipeFilterSchema = z.object({
  cuisine: z.string().optional(),
  maxTime: z.number().min(0).max(180).optional(),
  difficulty: z.enum(['easy', 'medium', 'hard']).optional(),
  dietary: z.array(z.string()).optional(),
})

export type RecipeFilters = z.infer<typeof recipeFilterSchema>

// src/components/RecipeFilterForm.tsx
import { useForm } from 'react-hook-form'
import { zodResolver } from '@hookform/resolvers/zod'
import { recipeFilterSchema, RecipeFilters } from '@/schemas/recipeSchema'

export function RecipeFilterForm() {
  const { register, handleSubmit, formState: { errors } } = useForm<RecipeFilters>({
    resolver: zodResolver(recipeFilterSchema),
  })

  const onSubmit = (data: RecipeFilters) => {
    // Handle filter submission
  }

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register('cuisine')} />
      {errors.cuisine && <p>{errors.cuisine.message}</p>}
    </form>
  )
}
```

---

## Authentication

### NextAuth.js (Auth.js v5)

**Version**: 5.x (beta, stable for production)
**Why NextAuth.js?**
- ✅ **Built-in OAuth** - Yandex, VK providers easy to add
- ✅ **Session management** - handles JWT refresh automatically
- ✅ **Next.js 14 compatible** - works with App Router
- ✅ **Custom backend** - can integrate with ASP.NET Core API
- ✅ **Saves 2-3 days** of auth implementation time

**Configuration**:
```typescript
// src/app/api/auth/[...nextauth]/route.ts
import NextAuth from 'next-auth'
import CredentialsProvider from 'next-auth/providers/credentials'
import YandexProvider from 'next-auth/providers/yandex'

export const authOptions = {
  providers: [
    CredentialsProvider({
      name: 'Credentials',
      credentials: {
        email: { label: 'Email', type: 'email' },
        password: { label: 'Password', type: 'password' },
      },
      async authorize(credentials) {
        // Call ASP.NET Core API
        const res = await fetch(`${process.env.API_BASE_URL}/api/v1/auth/login`, {
          method: 'POST',
          body: JSON.stringify(credentials),
          headers: { 'Content-Type': 'application/json' },
        })
        const user = await res.json()
        if (res.ok && user) {
          return user
        }
        return null
      },
    }),
    YandexProvider({
      clientId: process.env.YANDEX_CLIENT_ID,
      clientSecret: process.env.YANDEX_CLIENT_SECRET,
    }),
  ],
  callbacks: {
    async jwt({ token, user }) {
      if (user) {
        token.accessToken = user.accessToken
        token.refreshToken = user.refreshToken
      }
      return token
    },
    async session({ session, token }) {
      session.accessToken = token.accessToken
      return session
    },
  },
}

const handler = NextAuth(authOptions)
export { handler as GET, handler as POST }
```

---

## Image Optimization

### Next.js Image Component

**Built-in**: `next/image`
**Configuration**:
```javascript
// next.config.js
module.exports = {
  images: {
    domains: ['storage.yandexcloud.net'], // Yandex Object Storage
    formats: ['image/avif', 'image/webp'],
    deviceSizes: [640, 750, 828, 1080, 1200],
    imageSizes: [16, 32, 48, 64, 96, 128, 256, 384],
  },
}
```

**Usage**:
```typescript
import Image from 'next/image'

<Image
  src="https://storage.yandexcloud.net/cookie-recipes/pasta-carbonara.jpg"
  alt="Pasta Carbonara"
  width={400}
  height={300}
  className="rounded-lg"
  priority // for above-the-fold images
/>
```

**CDN Strategy**:
- **MVP**: Direct Yandex Object Storage URLs
- **Phase 2**: Add CloudFlare CDN (~$5-10/month)

---

## Utilities

### Date Manipulation: date-fns

**Version**: 3.x
**Why date-fns over moment.js?**
- ✅ Modular (tree-shakeable)
- ✅ Immutable (functional)
- ✅ TypeScript support
- ✅ 13KB vs 67KB (moment.js)

```typescript
import { formatDistanceToNow, format } from 'date-fns'
import { ru } from 'date-fns/locale'

// "2 часа назад"
formatDistanceToNow(new Date(recipe.createdAt), { addSuffix: true, locale: ru })

// "15 октября 2025"
format(new Date(), 'dd MMMM yyyy', { locale: ru })
```

---

### Class Name Utilities

**clsx + tailwind-merge**

```typescript
import { clsx, type ClassValue } from 'clsx'
import { twMerge } from 'tailwind-merge'

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs))
}

// Usage
<button className={cn('px-4 py-2', isActive && 'bg-blue-500', className)} />
```

---

## Testing

### Unit Testing: Vitest

**Version**: 1.x
**Why Vitest over Jest?**
- ✅ **10x faster** - native ESM support
- ✅ **Vite-powered** - same config as Next.js (if migrating)
- ✅ **Jest-compatible API** - easy migration
- ✅ **TypeScript first-class** - no extra setup

**Configuration**:
```typescript
// vitest.config.ts
import { defineConfig } from 'vitest/config'
import react from '@vitejs/plugin-react'
import path from 'path'

export default defineConfig({
  plugins: [react()],
  test: {
    environment: 'jsdom',
    globals: true,
    setupFiles: ['./src/tests/setup.ts'],
  },
  resolve: {
    alias: {
      '@': path.resolve(__dirname, './src'),
    },
  },
})
```

---

### Component Testing: React Testing Library

**Version**: 14.x
**Philosophy**: Test user behavior, not implementation details

**Example Test**:
```typescript
// src/components/RecipeCard.test.tsx
import { render, screen } from '@testing-library/react'
import { RecipeCard } from './RecipeCard'

describe('RecipeCard', () => {
  it('renders recipe title and rating', () => {
    const recipe = {
      id: 1,
      title: 'Pasta Carbonara',
      rating: 4.5,
      imageUrl: '/pasta.jpg',
    }

    render(<RecipeCard recipe={recipe} />)

    expect(screen.getByText('Pasta Carbonara')).toBeInTheDocument()
    expect(screen.getByText('4.5')).toBeInTheDocument()
  })
})
```

---

### E2E Testing (Phase 2)

**Tool**: Playwright
**Reason**: Skip for MVP, add when user flows are stable.

---

## Development Tools

### Linting & Formatting

| Tool | Version | Purpose |
|------|---------|---------|
| **ESLint** | 8.x | Code linting |
| **Prettier** | 3.x | Code formatting |
| **eslint-config-next** | Built-in | Next.js best practices |
| **@typescript-eslint** | 6.x | TypeScript linting |

**ESLint Config**:
```json
{
  "extends": [
    "next/core-web-vitals",
    "plugin:@typescript-eslint/recommended",
    "prettier"
  ],
  "rules": {
    "no-console": "warn",
    "prefer-const": "error"
  }
}
```

**Prettier Config**:
```json
{
  "semi": false,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5",
  "printWidth": 100
}
```

---

### Git Hooks: Husky + lint-staged

**Purpose**: Run linting/tests before commits

```json
// package.json
{
  "scripts": {
    "prepare": "husky install"
  },
  "lint-staged": {
    "*.{ts,tsx}": ["eslint --fix", "prettier --write"],
    "*.{json,md}": ["prettier --write"]
  }
}
```

---

## Environment Variables

### Structure

```bash
# .env.local (local development)
NEXT_PUBLIC_API_BASE_URL=http://localhost:5000
NEXT_PUBLIC_OBJECT_STORAGE_URL=https://storage.yandexcloud.net/cookie-dev

NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=your-secret-key-here

YANDEX_CLIENT_ID=your-yandex-oauth-id
YANDEX_CLIENT_SECRET=your-yandex-oauth-secret

# .env.production (production)
NEXT_PUBLIC_API_BASE_URL=https://api.cookie.com
NEXT_PUBLIC_OBJECT_STORAGE_URL=https://storage.yandexcloud.net/cookie-prod

NEXTAUTH_URL=https://cookie.com
NEXTAUTH_SECRET=production-secret-key

YANDEX_CLIENT_ID=production-oauth-id
YANDEX_CLIENT_SECRET=production-oauth-secret
```

### Validation

```typescript
// src/lib/env.ts
import { z } from 'zod'

const envSchema = z.object({
  NEXT_PUBLIC_API_BASE_URL: z.string().url(),
  NEXTAUTH_SECRET: z.string().min(32),
  YANDEX_CLIENT_ID: z.string(),
})

export const env = envSchema.parse(process.env)
```

---

## Docker Development

### docker-compose.yml (Frontend Only)

```yaml
version: '3.8'

services:
  frontend:
    build:
      context: .
      dockerfile: Dockerfile.dev
    ports:
      - "3000:3000"
    volumes:
      - .:/app
      - /app/node_modules
      - /app/.next
    environment:
      - NODE_ENV=development
      - NEXT_PUBLIC_API_BASE_URL=http://backend:5000
    depends_on:
      - backend

  backend:
    image: cookie-backend:latest
    ports:
      - "5000:5000"
    environment:
      - ASPNETCORE_ENVIRONMENT=Development
```

### Dockerfile.dev

```dockerfile
FROM node:20-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .

EXPOSE 3000

CMD ["npm", "run", "dev"]
```

---

## Project Structure

```
cookie-frontend/
├── src/
│   ├── app/                      # Next.js 14 App Router
│   │   ├── (auth)/              # Auth group (login, register)
│   │   ├── (main)/              # Main app (recipes, profile)
│   │   ├── api/                 # API routes (NextAuth)
│   │   ├── layout.tsx           # Root layout
│   │   └── page.tsx             # Home page
│   │
│   ├── components/
│   │   ├── ui/                  # shadcn/ui components
│   │   ├── recipes/             # Recipe-specific
│   │   ├── layout/              # Header, Footer, Sidebar
│   │   └── common/              # Shared components
│   │
│   ├── hooks/
│   │   ├── api/                 # TanStack Query hooks
│   │   │   ├── useRecipes.ts
│   │   │   ├── useRecipe.ts
│   │   │   └── useFavorites.ts
│   │   └── useDebounce.ts       # Utility hooks
│   │
│   ├── lib/
│   │   ├── api/                 # API client setup
│   │   │   ├── axiosClient.ts
│   │   │   └── recipes.ts
│   │   ├── utils.ts             # Utility functions (cn, etc.)
│   │   ├── queryClient.ts       # TanStack Query config
│   │   └── env.ts               # Environment validation
│   │
│   ├── stores/                  # Zustand stores
│   │   ├── useUserPreferencesStore.ts
│   │   └── useAuthStore.ts
│   │
│   ├── schemas/                 # Zod schemas
│   │   ├── recipeSchema.ts
│   │   └── userSchema.ts
│   │
│   ├── types/                   # TypeScript types
│   │   ├── recipe.ts
│   │   ├── user.ts
│   │   └── api.ts
│   │
│   └── tests/                   # Test setup
│       ├── setup.ts
│       └── utils.tsx
│
├── public/                      # Static assets
│   ├── images/
│   └── fonts/
│
├── .env.local                   # Local env variables
├── .env.example                 # Env template
├── next.config.js               # Next.js config
├── tailwind.config.js           # Tailwind config
├── tsconfig.json                # TypeScript config
├── vitest.config.ts             # Vitest config
├── docker-compose.yml           # Docker dev setup
├── Dockerfile.dev               # Dev Dockerfile
└── package.json
```

---

## Performance Optimizations

### 1. Code Splitting (Next.js Built-in)
- Dynamic imports for heavy components
- Route-based code splitting (automatic)

### 2. Image Optimization
- `next/image` with WebP/AVIF
- Lazy loading for below-the-fold images
- Placeholder blur-up effect

### 3. Font Optimization
```typescript
// src/app/layout.tsx
import { Inter } from 'next/font/google'

const inter = Inter({ subsets: ['latin', 'cyrillic'], display: 'swap' })

export default function RootLayout({ children }) {
  return (
    <html lang="ru" className={inter.className}>
      {children}
    </html>
  )
}
```

### 4. Bundle Analysis (Phase 2)
```bash
npm install -D @next/bundle-analyzer

# Analyze bundle
ANALYZE=true npm run build
```

---

## Migration Path & Scalability

### When to Consider Changes

| Scenario | Current Solution | Migrate To | Timeline |
|----------|------------------|------------|----------|
| Team grows to 3+ devs | Zustand | Redux Toolkit | Month 3-4 |
| Need real-time features | REST + polling | WebSockets/SSE | Phase 2 |
| SEO issues with CSR | Next.js SSR | Keep (already optimal) | N/A |
| Bundle size > 500KB | Manual optimization | Lazy loading + code splitting | Month 2-3 |
| Need offline support | None | PWA + service workers | Phase 3 |

---

## Dependencies Summary

### Production Dependencies

```json
{
  "dependencies": {
    "next": "^14.2.0",
    "react": "^18.3.0",
    "react-dom": "^18.3.0",
    "typescript": "^5.4.0",

    "@tanstack/react-query": "^5.28.0",
    "zustand": "^4.5.0",
    "axios": "^1.6.0",

    "next-auth": "^5.0.0-beta",
    "react-hook-form": "^7.51.0",
    "zod": "^3.22.0",
    "@hookform/resolvers": "^3.3.0",

    "tailwindcss": "^3.4.0",
    "clsx": "^2.1.0",
    "tailwind-merge": "^2.2.0",

    "lucide-react": "^0.360.0",
    "date-fns": "^3.6.0",

    "@headlessui/react": "^1.7.0"
  }
}
```

### Dev Dependencies

```json
{
  "devDependencies": {
    "@types/node": "^20.11.0",
    "@types/react": "^18.2.0",
    "@types/react-dom": "^18.2.0",

    "vitest": "^1.4.0",
    "@testing-library/react": "^14.2.0",
    "@testing-library/jest-dom": "^6.4.0",
    "@vitejs/plugin-react": "^4.2.0",

    "eslint": "^8.57.0",
    "eslint-config-next": "^14.2.0",
    "@typescript-eslint/eslint-plugin": "^7.2.0",
    "@typescript-eslint/parser": "^7.2.0",

    "prettier": "^3.2.0",
    "prettier-plugin-tailwindcss": "^0.5.0",

    "husky": "^9.0.0",
    "lint-staged": "^15.2.0"
  }
}
```

---

## Summary

**Tech Stack at a Glance**:

| Category | Technology | Version |
|----------|-----------|---------|
| **Framework** | Next.js | 14.x |
| **Language** | TypeScript | 5.x |
| **Global State** | Zustand | 4.x |
| **Server State** | TanStack Query | 5.x |
| **Forms** | React Hook Form + Zod | 7.x / 3.x |
| **Styling** | TailwindCSS (custom components) | 3.x |
| **UI Primitives** | Headless UI (optional) | 1.7.x |
| **Auth** | NextAuth.js | 5.x |
| **HTTP** | Axios | 1.x |
| **Icons** | Lucide React | 0.x |
| **Testing** | Vitest + RTL | 1.x / 14.x |
| **Date Utils** | date-fns | 3.x |
| **Dev Tools** | ESLint + Prettier + Husky | Latest |

---

## Next Steps

1. ✅ **Initialize Next.js 14 project**
   ```bash
   npx create-next-app@latest cookie-frontend \
     --typescript --tailwind --app --src-dir --import-alias "@/*"
   ```

2. ✅ **Install core dependencies**
   ```bash
   npm install @tanstack/react-query zustand axios next-auth
   npm install react-hook-form @hookform/resolvers zod
   npm install lucide-react date-fns clsx tailwind-merge
   npm install @headlessui/react
   ```

3. ✅ **Create base UI components** (custom-built)
   - Start with: Button, Input, Card, Badge
   - Add complex components with Headless UI: Modal, Dropdown, Toast

4. ✅ **Configure development tools**
   - ESLint + Prettier
   - Husky + lint-staged
   - Vitest + React Testing Library

5. ✅ **Create project structure** (follow structure above)

6. ✅ **Set up Docker Compose** for local development

7. ✅ **Configure environment variables** (.env.example)

---

**Document Status**: ✅ Ready for Development
**Last Review**: 2025-10-15
**Next Review**: After MVP Phase 1 (Week 10)
