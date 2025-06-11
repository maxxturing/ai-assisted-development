# Architecture Specification: Travel Planning App

## Tech Stack

### Core Technologies
- **Language**: TypeScript
- **Frontend**: Solito (React Native + Next.js)
- **Styling**: Tamagui (Universal Design System)
- **Database**: Turso (LibSQL) with Drizzle ORM
- **Package Manager**: Yarn
- **State Management**: React Query (TanStack Query) + Custom Hooks

### Platform Structure
- **Mobile**: React Native with Expo
- **Web**: Next.js with React
- **Shared**: Universal components and business logic

## Project Structure

### Monorepo Package Organization
```
packages/
├── app/           # Shared navigation and business logic
├── ui/            # Universal components (Tamagui)
├── db/            # Database schema and queries (Drizzle)
└── config/        # Shared configuration

apps/
├── expo/          # Mobile app
└── next/          # Web app
```

### Package Dependencies
- `packages/app` - Core application logic, navigation, custom hooks
- `packages/ui` - Tamagui components, shared UI patterns
- `packages/db` - Drizzle schema, queries, database utilities
- `packages/config` - Shared TypeScript configs, constants

## Data Architecture

### Database Schema (Drizzle)
```typescript
// trips table
{
  id: string (primary key)
  name: string
  destination: string
  startDate: date
  endDate: date
  description: string (optional)
  createdAt: timestamp
}

// packingLists table
{
  id: string (primary key)
  tripId: string (foreign key to trips)
  name: string
  createdAt: timestamp
}

// packingItems table
{
  id: string (primary key)
  packingListId: string (foreign key to packingLists)
  name: string
  description: string (optional)
  isPacked: boolean
  category: string (optional)
}
```

### Data Relationships
- One Trip → Many PackingLists
- One PackingList → Many PackingItems
- Cascade deletes: Trip deletion removes all related packing lists and items

## State Management Architecture

### React Query Implementation
- **Queries**: Data fetching with caching and background sync
- **Mutations**: Optimistic updates for packing item toggles
- **Cache Management**: Intelligent invalidation and refetching

### Custom Hooks Pattern
```typescript
// Business logic encapsulation
useTrips() // Trip CRUD operations
usePackingLists(tripId) // Packing list management
usePackingItems(packingListId) // Item management with optimistic updates
```

### Component State Strategy
- Server state: React Query
- UI state: useState/useReducer
- Global state: React Context (minimal usage)

## Component Architecture

### Screen Components
- **Trip Screens**: TripList, TripDetails, CreateTrip, EditTrip
- **Packing Screens**: PackingListView, PackingItemManager
- **Shared Screens**: Navigation, Settings

### UI Components (Tamagui)
- Form components with validation
- List components with loading states
- Button components with consistent styling
- Toast notifications for feedback

### Navigation Structure
```
App
├── BottomTabs (Mobile) / Sidebar (Web)
│   ├── Trips Stack
│   │   ├── TripList
│   │   ├── TripDetails
│   │   └── PackingListView
│   └── Settings Stack
└── Modals
    ├── CreateTrip
    ├── EditTrip
    └── AddPackingItem
```

## Error Handling Strategy

### Error Boundaries
- Top-level boundary in each app
- Feature-level boundaries for isolated error handling
- Fallback UI components for graceful degradation

### Toast Notifications (Tamagui)
- Success feedback for completed actions
- Error messages with retry options
- Loading states with progress indicators

### Error Categorization
- Network errors: Retry with exponential backoff
- Validation errors: User-friendly form feedback
- Application errors: Logged and reported with fallback UI

## Performance Optimization

### Mobile-First Approach
- Optimized bundle sizes with code splitting
- Lazy loading for non-critical screens
- Image optimization and caching

### React Query Optimizations
- Background refetching for data freshness
- Optimistic updates for immediate feedback
- Intelligent cache invalidation

### Universal Performance
- Shared component optimization
- Platform-specific performance considerations
- Memory management for large lists

## Development Patterns

### Code Organization Principles
- Business logic in custom hooks
- UI components focused on presentation only
- Shared utilities in appropriate packages

### TypeScript Standards
- Strict mode enabled
- Comprehensive interface definitions
- No `any` types allowed
- Proper error type definitions

### Testing Strategy
- Focus on critical business logic
- Custom hook testing
- Component interaction testing
- Minimal but essential coverage

## Deployment Architecture

### Development
- Local Turso database (LibSQL)
- Hot reloading for rapid development
- Shared development environment
- Edge-distributed database for optimal performance

### Production Considerations
- Turso edge replicas for global performance
- Git-like database branching for feature development
- Platform-specific build optimizations
- Error monitoring and logging setup
- Universal database access pattern (web + mobile)