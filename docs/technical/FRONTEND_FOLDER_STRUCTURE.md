# COOKie Frontend Folder Structure & Conventions

> **Version**: 1.0
> **Last Updated**: 2025-10-15
> **Framework**: Next.js 14 (App Router)

---

## Complete Folder Structure

```
cookie-frontend/
├── src/
│   ├── app/                          # Next.js 14 App Router
│   │   ├── (auth)/                   # Auth route group (no layout)
│   │   │   ├── login/
│   │   │   │   └── page.tsx          # /login
│   │   │   ├── register/
│   │   │   │   └── page.tsx          # /register
│   │   │   └── layout.tsx            # Auth-specific layout (centered)
│   │   │
│   │   ├── (main)/                   # Main app routes (with header/footer)
│   │   │   ├── recipes/
│   │   │   │   ├── page.tsx          # /recipes (search/browse)
│   │   │   │   └── [slug]/
│   │   │   │       └── page.tsx      # /recipes/pasta-carbonara
│   │   │   ├── profile/
│   │   │   │   ├── page.tsx          # /profile
│   │   │   │   ├── favorites/
│   │   │   │   │   └── page.tsx      # /profile/favorites
│   │   │   │   └── settings/
│   │   │   │       └── page.tsx      # /profile/settings
│   │   │   └── layout.tsx            # Main layout (Header + Footer)
│   │   │
│   │   ├── admin/                    # Admin panel (protected)
│   │   │   ├── recipes/
│   │   │   │   ├── page.tsx          # /admin/recipes (list)
│   │   │   │   ├── new/
│   │   │   │   │   └── page.tsx      # /admin/recipes/new
│   │   │   │   └── [id]/
│   │   │   │       └── edit/
│   │   │   │           └── page.tsx  # /admin/recipes/123/edit
│   │   │   ├── dashboard/
│   │   │   │   └── page.tsx          # /admin/dashboard
│   │   │   └── layout.tsx            # Admin layout (sidebar)
│   │   │
│   │   ├── api/                      # API routes (NextAuth, webhooks)
│   │   │   └── auth/
│   │   │       └── [...nextauth]/
│   │   │           └── route.ts      # NextAuth handlers
│   │   │
│   │   ├── layout.tsx                # Root layout (QueryProvider, auth)
│   │   ├── page.tsx                  # Home page (/)
│   │   ├── loading.tsx               # Loading UI
│   │   ├── error.tsx                 # Error UI
│   │   └── not-found.tsx             # 404 page
│   │
│   ├── components/
│   │   ├── ui/                       # Base UI components (custom-built)
│   │   │   ├── Button.tsx
│   │   │   ├── Input.tsx
│   │   │   ├── Textarea.tsx
│   │   │   ├── Card.tsx
│   │   │   ├── Badge.tsx
│   │   │   ├── Avatar.tsx
│   │   │   ├── Modal.tsx             # Using Headless UI
│   │   │   ├── Dropdown.tsx          # Using Headless UI
│   │   │   ├── Toast.tsx
│   │   │   ├── Spinner.tsx
│   │   │   └── Select.tsx            # Using Headless UI
│   │   │
│   │   ├── recipes/                  # Recipe-specific components
│   │   │   ├── RecipeCard.tsx
│   │   │   ├── RecipeGrid.tsx
│   │   │   ├── RecipeList.tsx
│   │   │   ├── RecipeFilters.tsx
│   │   │   ├── RecipeDetail.tsx
│   │   │   ├── NutritionInfo.tsx
│   │   │   ├── IngredientsList.tsx
│   │   │   ├── CookingSteps.tsx
│   │   │   ├── RatingStars.tsx
│   │   │   └── FavoriteButton.tsx
│   │   │
│   │   ├── layout/                   # Layout components
│   │   │   ├── Header.tsx
│   │   │   ├── Footer.tsx
│   │   │   ├── Sidebar.tsx
│   │   │   ├── MobileMenu.tsx
│   │   │   └── Breadcrumbs.tsx
│   │   │
│   │   ├── forms/                    # Form components
│   │   │   ├── LoginForm.tsx
│   │   │   ├── RegisterForm.tsx
│   │   │   ├── RecipeFilterForm.tsx
│   │   │   ├── ProfileEditForm.tsx
│   │   │   └── RecipeForm.tsx        # Admin recipe CRUD
│   │   │
│   │   └── common/                   # Shared components
│   │       ├── SearchBar.tsx
│   │       ├── Pagination.tsx
│   │       ├── ErrorMessage.tsx
│   │       ├── EmptyState.tsx
│   │       └── LoadingState.tsx
│   │
│   ├── hooks/
│   │   ├── api/                      # TanStack Query hooks
│   │   │   ├── useRecipes.ts         # GET /api/v1/recipes
│   │   │   ├── useRecipe.ts          # GET /api/v1/recipes/:slug
│   │   │   ├── useFavorites.ts       # GET /api/v1/users/me/favorites
│   │   │   ├── useFavorite.ts        # POST/DELETE favorite
│   │   │   ├── useRating.ts          # POST/PATCH rating
│   │   │   ├── useUser.ts            # GET /api/v1/users/me
│   │   │   └── useAuth.ts            # Login/logout mutations
│   │   │
│   │   ├── useDebounce.ts            # Debounce utility
│   │   ├── useLocalStorage.ts        # LocalStorage hook
│   │   ├── useMediaQuery.ts          # Responsive breakpoints
│   │   ├── useIntersectionObserver.ts # Infinite scroll
│   │   └── useClickOutside.ts        # Click outside detection
│   │
│   ├── lib/
│   │   ├── api/                      # API client & services
│   │   │   ├── axiosClient.ts        # Axios instance + interceptors
│   │   │   ├── recipes.ts            # Recipe API methods
│   │   │   ├── users.ts              # User API methods
│   │   │   ├── auth.ts               # Auth API methods
│   │   │   └── favorites.ts          # Favorites API methods
│   │   │
│   │   ├── utils.ts                  # Utility functions (cn, formatDate, etc.)
│   │   ├── queryClient.ts            # TanStack Query config
│   │   ├── constants.ts              # App constants
│   │   └── env.ts                    # Environment variable validation
│   │
│   ├── stores/                       # Zustand stores
│   │   ├── useUserPreferencesStore.ts # Theme, language preferences
│   │   ├── useAuthStore.ts           # Auth state (if not using NextAuth context)
│   │   └── useUIStore.ts             # UI state (sidebar, modals)
│   │
│   ├── schemas/                      # Zod validation schemas
│   │   ├── recipeSchema.ts
│   │   ├── userSchema.ts
│   │   ├── authSchema.ts
│   │   └── filterSchema.ts
│   │
│   ├── types/                        # TypeScript types & interfaces
│   │   ├── recipe.ts
│   │   ├── user.ts
│   │   ├── api.ts                    # API request/response types
│   │   ├── auth.ts
│   │   └── index.ts                  # Re-export all types
│   │
│   ├── styles/
│   │   └── globals.css               # Global styles, Tailwind imports
│   │
│   └── tests/                        # Test utilities
│       ├── setup.ts                  # Vitest setup
│       ├── utils.tsx                 # Test render helpers
│       └── mocks/                    # Mock data
│           ├── recipes.ts
│           └── users.ts
│
├── public/                           # Static assets
│   ├── images/
│   │   ├── logo.svg
│   │   ├── hero-bg.jpg
│   │   └── placeholder-recipe.png
│   ├── fonts/                        # Local fonts (if any)
│   └── favicon.ico
│
├── .env.local                        # Local environment variables
├── .env.example                      # Environment variable template
├── .eslintrc.json                    # ESLint configuration
├── .prettierrc                       # Prettier configuration
├── .gitignore
├── next.config.js                    # Next.js configuration
├── tailwind.config.js                # Tailwind configuration
├── tsconfig.json                     # TypeScript configuration
├── vitest.config.ts                  # Vitest configuration
├── docker-compose.yml                # Docker Compose (dev)
├── Dockerfile.dev                    # Dev Dockerfile
├── package.json
└── README.md
```

---

## Naming Conventions

### Files & Folders

| Type | Convention | Example |
|------|------------|---------|
| **React Components** | PascalCase | `RecipeCard.tsx` |
| **Hooks** | camelCase with `use` prefix | `useRecipes.ts` |
| **Utils** | camelCase | `formatDate.ts` |
| **Types** | PascalCase (interfaces/types) | `Recipe`, `User` |
| **Constants** | UPPER_SNAKE_CASE | `API_BASE_URL` |
| **Routes** | kebab-case | `app/(main)/my-profile/page.tsx` |
| **API Endpoints** | kebab-case | `/api/v1/recipes-search` |

### Component File Structure

**Pattern**: One component per file, named exports for utilities

```typescript
// ✅ Good: RecipeCard.tsx
import { Recipe } from '@/types'
import { Card } from '@/components/ui/Card'

interface RecipeCardProps {
  recipe: Recipe
  onFavorite?: (id: number) => void
}

export function RecipeCard({ recipe, onFavorite }: RecipeCardProps) {
  return <Card>...</Card>
}

// ✅ Good: Helper functions below main component
function formatCalories(calories: number): string {
  return `${calories} ккал`
}
```

---

## Route Groups (Next.js 14)

### Why Route Groups?

Route groups allow you to organize routes without affecting the URL structure.

```
(auth)/              # Auth pages (no header/footer)
  login/
  register/

(main)/              # Main app (with header/footer)
  recipes/
  profile/

admin/               # Admin panel (different layout)
  dashboard/
  recipes/
```

**Result**:
- `/login` (not `/auth/login`)
- `/recipes` (not `/main/recipes`)
- `/admin/dashboard` (keeps `/admin` prefix)

---

## Component Organization

### UI Components (Generic)

**Location**: `src/components/ui/`
**Purpose**: Reusable, project-agnostic components
**Example**: Button, Input, Modal, Card

**Characteristics**:
- ✅ No business logic
- ✅ Accept props for customization
- ✅ Fully typed with TypeScript
- ✅ Support `className` prop for overrides

```typescript
// src/components/ui/Button.tsx
export interface ButtonProps extends ButtonHTMLAttributes<HTMLButtonElement> {
  variant?: 'primary' | 'secondary' | 'outline'
  size?: 'sm' | 'md' | 'lg'
  isLoading?: boolean
}

export const Button = forwardRef<HTMLButtonElement, ButtonProps>(...)
```

---

### Feature Components (Domain-Specific)

**Location**: `src/components/recipes/`, `src/components/profile/`
**Purpose**: Business logic, feature-specific components
**Example**: RecipeCard, RecipeFilters, ProfileAvatar

**Characteristics**:
- ✅ Use UI components internally
- ✅ Connect to API hooks
- ✅ Handle business logic

```typescript
// src/components/recipes/RecipeCard.tsx
import { Recipe } from '@/types'
import { Card } from '@/components/ui/Card'
import { Button } from '@/components/ui/Button'
import { useFavorite } from '@/hooks/api/useFavorite'

export function RecipeCard({ recipe }: { recipe: Recipe }) {
  const { mutate: toggleFavorite } = useFavorite()

  return (
    <Card>
      <h3>{recipe.title}</h3>
      <Button onClick={() => toggleFavorite(recipe.id)}>
        Favorite
      </Button>
    </Card>
  )
}
```

---

## API Hooks Pattern

### Structure

```typescript
// src/hooks/api/useRecipes.ts
import { useQuery } from '@tanstack/react-query'
import { recipesApi } from '@/lib/api/recipes'
import { RecipeFilters } from '@/types'

export function useRecipes(filters?: RecipeFilters) {
  return useQuery({
    queryKey: ['recipes', filters],
    queryFn: () => recipesApi.getRecipes(filters),
    staleTime: 1000 * 60 * 5, // 5 minutes
  })
}

// Usage in component
function RecipesPage() {
  const { data, isLoading, error } = useRecipes({ cuisine: 'italian' })

  if (isLoading) return <LoadingState />
  if (error) return <ErrorMessage error={error} />

  return <RecipeGrid recipes={data.recipes} />
}
```

### Mutation Hooks

```typescript
// src/hooks/api/useFavorite.ts
import { useMutation, useQueryClient } from '@tanstack/react-query'
import { favoritesApi } from '@/lib/api/favorites'

export function useFavorite() {
  const queryClient = useQueryClient()

  return useMutation({
    mutationFn: (recipeId: number) => favoritesApi.toggle(recipeId),
    onSuccess: () => {
      // Invalidate favorites list
      queryClient.invalidateQueries({ queryKey: ['favorites'] })
    },
  })
}
```

---

## Type Organization

### API Types

```typescript
// src/types/api.ts
export interface ApiResponse<T> {
  data: T
  message?: string
  success: boolean
}

export interface PaginatedResponse<T> {
  data: T[]
  pagination: {
    page: number
    perPage: number
    total: number
    totalPages: number
  }
}

export type ApiError = {
  message: string
  code: string
  details?: Record<string, string[]>
}
```

### Domain Types

```typescript
// src/types/recipe.ts
export interface Recipe {
  id: number
  slug: string
  title: string
  description: string
  cuisine: string
  difficulty: 'easy' | 'medium' | 'hard'
  prepTime: number
  cookTime: number
  totalTime: number
  servings: number
  instructions: CookingStep[]
  nutrition: NutritionInfo
  dietaryTags: string[]
  allergens: string[]
  imageUrls: string[]
  rating: {
    average: number
    count: number
  }
  viewCount: number
  favoriteCount: number
  createdAt: string
  updatedAt: string
}

export interface CookingStep {
  stepNumber: number
  instruction: string
  imageUrl?: string
}

export interface NutritionInfo {
  calories: number
  protein: number
  carbs: number
  fat: number
  fiber?: number
}
```

---

## Environment Variables

### .env.local

```bash
# API
NEXT_PUBLIC_API_BASE_URL=http://localhost:5000
NEXT_PUBLIC_API_TIMEOUT=10000

# Auth
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=your-secret-here

# OAuth
YANDEX_CLIENT_ID=your-yandex-id
YANDEX_CLIENT_SECRET=your-yandex-secret
VK_CLIENT_ID=your-vk-id
VK_CLIENT_SECRET=your-vk-secret

# Storage
NEXT_PUBLIC_OBJECT_STORAGE_URL=https://storage.yandexcloud.net/cookie-dev

# Analytics (Phase 2)
NEXT_PUBLIC_GA_TRACKING_ID=G-XXXXXXXXXX

# Feature Flags
NEXT_PUBLIC_ENABLE_RATINGS=true
NEXT_PUBLIC_ENABLE_COMMENTS=false
```

### Validation

```typescript
// src/lib/env.ts
import { z } from 'zod'

const envSchema = z.object({
  NEXT_PUBLIC_API_BASE_URL: z.string().url(),
  NEXT_PUBLIC_API_TIMEOUT: z.coerce.number().default(10000),
  NEXTAUTH_URL: z.string().url(),
  NEXTAUTH_SECRET: z.string().min(32),
  YANDEX_CLIENT_ID: z.string(),
  YANDEX_CLIENT_SECRET: z.string(),
})

export const env = envSchema.parse({
  NEXT_PUBLIC_API_BASE_URL: process.env.NEXT_PUBLIC_API_BASE_URL,
  NEXT_PUBLIC_API_TIMEOUT: process.env.NEXT_PUBLIC_API_TIMEOUT,
  NEXTAUTH_URL: process.env.NEXTAUTH_URL,
  NEXTAUTH_SECRET: process.env.NEXTAUTH_SECRET,
  YANDEX_CLIENT_ID: process.env.YANDEX_CLIENT_ID,
  YANDEX_CLIENT_SECRET: process.env.YANDEX_CLIENT_SECRET,
})
```

---

## Testing Structure

### Component Tests

```
src/
└── components/
    └── recipes/
        ├── RecipeCard.tsx
        └── RecipeCard.test.tsx    # Co-located test file
```

```typescript
// src/components/recipes/RecipeCard.test.tsx
import { render, screen } from '@testing-library/react'
import { RecipeCard } from './RecipeCard'
import { mockRecipe } from '@/tests/mocks/recipes'

describe('RecipeCard', () => {
  it('renders recipe title', () => {
    render(<RecipeCard recipe={mockRecipe} />)
    expect(screen.getByText(mockRecipe.title)).toBeInTheDocument()
  })

  it('displays rating correctly', () => {
    render(<RecipeCard recipe={mockRecipe} />)
    expect(screen.getByText('4.5')).toBeInTheDocument()
  })
})
```

### Hook Tests

```typescript
// src/hooks/api/useRecipes.test.ts
import { renderHook, waitFor } from '@testing-library/react'
import { useRecipes } from './useRecipes'
import { QueryClient, QueryClientProvider } from '@tanstack/react-query'

const createWrapper = () => {
  const queryClient = new QueryClient()
  return ({ children }) => (
    <QueryClientProvider client={queryClient}>{children}</QueryClientProvider>
  )
}

describe('useRecipes', () => {
  it('fetches recipes successfully', async () => {
    const { result } = renderHook(() => useRecipes(), {
      wrapper: createWrapper(),
    })

    await waitFor(() => expect(result.current.isSuccess).toBe(true))
    expect(result.current.data).toBeDefined()
  })
})
```

---

## Import Aliases

**Configuration** (`tsconfig.json`):
```json
{
  "compilerOptions": {
    "paths": {
      "@/*": ["./src/*"],
      "@/components/*": ["./src/components/*"],
      "@/hooks/*": ["./src/hooks/*"],
      "@/lib/*": ["./src/lib/*"],
      "@/types/*": ["./src/types/*"]
    }
  }
}
```

**Usage**:
```typescript
// ✅ Good: Absolute imports
import { Button } from '@/components/ui/Button'
import { useRecipes } from '@/hooks/api/useRecipes'
import { Recipe } from '@/types/recipe'

// ❌ Avoid: Relative imports for deep paths
import { Button } from '../../../components/ui/Button'
```

---

## Code Style Guidelines

### Component Style

```typescript
// ✅ Good: Functional component with TypeScript
export function RecipeCard({ recipe, onFavorite }: RecipeCardProps) {
  const [isHovered, setIsHovered] = useState(false)

  return (
    <article
      onMouseEnter={() => setIsHovered(true)}
      onMouseLeave={() => setIsHovered(false)}
      className="rounded-lg border p-4"
    >
      {/* Content */}
    </article>
  )
}

// ❌ Avoid: Arrow function exports (harder to debug)
export const RecipeCard = ({ recipe }: RecipeCardProps) => {
  // ...
}
```

### Event Handlers

```typescript
// ✅ Good: Named handler functions
function RecipeCard({ recipe }: RecipeCardProps) {
  const handleFavoriteClick = () => {
    // Logic here
  }

  return <Button onClick={handleFavoriteClick}>Favorite</Button>
}

// ❌ Avoid: Inline arrow functions (causes re-renders)
<Button onClick={() => console.log('Favorite')}>Favorite</Button>
```

---

## Performance Best Practices

### 1. Lazy Load Heavy Components

```typescript
// src/app/(main)/recipes/[slug]/page.tsx
import { lazy, Suspense } from 'react'

const RecipeComments = lazy(() => import('@/components/recipes/RecipeComments'))

export default function RecipePage() {
  return (
    <>
      <RecipeDetail />
      <Suspense fallback={<div>Loading comments...</div>}>
        <RecipeComments />
      </Suspense>
    </>
  )
}
```

### 2. Optimize Images

```typescript
// Always use next/image
import Image from 'next/image'

<Image
  src={recipe.imageUrls[0]}
  alt={recipe.title}
  width={400}
  height={300}
  className="rounded-lg"
  loading="lazy" // Below-the-fold images
  priority={false} // Or true for above-the-fold
/>
```

### 3. Memoize Expensive Calculations

```typescript
import { useMemo } from 'react'

function RecipeGrid({ recipes }: { recipes: Recipe[] }) {
  const sortedRecipes = useMemo(() => {
    return recipes.sort((a, b) => b.rating.average - a.rating.average)
  }, [recipes])

  return <div>{/* Render sortedRecipes */}</div>
}
```

---

## Summary

**Key Principles**:
1. ✅ **Colocation** - Keep related files together
2. ✅ **Separation of concerns** - UI vs business logic
3. ✅ **Type safety** - Everything typed with TypeScript
4. ✅ **Reusability** - Generic UI components, feature-specific composed
5. ✅ **Performance** - Lazy loading, memoization, optimized images
6. ✅ **Testing** - Co-located test files

**Next Steps**:
1. Initialize project structure
2. Create base UI components
3. Set up API client
4. Implement authentication
5. Build recipe browsing features

---

**Document Status**: ✅ Ready for Implementation
**Last Review**: 2025-10-15
**Next Review**: After first sprint (Week 8)
