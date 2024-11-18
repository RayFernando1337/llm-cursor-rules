## Authentication (Clerk)

- Clerk is used for authentication.
- The `ClerkProvider` wraps the application in `app/providers.tsx`.
- Middleware in `middleware.ts` handles authentication routes.
- `useSession` hook in `lib/utils.ts` provides authentication state.

## Database (Convex)

- Convex is used as the database and backend.
- Convex schema is defined in `convex/schema.ts`.
- Convex functions (queries, mutations, actions) are in separate files in the `convex` directory.
- The `ConvexProviderWithClerk` wraps the application in `app/providers.tsx`.
- Custom hooks like `authQuery`, `authMutation`, and `authAction` in `convex/util.ts` handle authenticated Convex operations.

## Payment Integration (Stripe)

- Stripe is used for payment processing.
- Stripe integration is primarily handled in `convex/stripe.ts`.
- The `pay` action initiates the payment process.
- Webhook handling for Stripe events is in `convex/http.ts`.

## File Structure

- Next.js 14 app directory structure is used.
- Pages are in `app` directory.
- Components are in `components` directory.
- Convex functions and schema are in the `convex` directory.

## Key Patterns

1. Server Components: Most pages are server components (no "use client" directive).
2. Client Components: Components that need interactivity use the "use client" directive.
3. Convex Queries and Mutations: Used throughout the application for data fetching and manipulation.
4. Authentication Checks: Many components and pages check authentication status before rendering or performing actions.
5. Environment Variables: Sensitive information and API keys are stored in environment variables.

## Important Files

- `convex/schema.ts`: Defines the database schema.
- `convex/users.ts`: Handles user-related operations.
- `convex/stripe.ts`: Manages Stripe integration.
- `app/providers.tsx`: Sets up global providers (Convex, Clerk, Theme).
- `middleware.ts`: Handles authentication middleware.
- `lib/utils.ts`: Contains utility functions and hooks.

## Styling

- Tailwind CSS is used for styling.
- Global styles are in `app/globals.css`.
- Tailwind config is in `tailwind.config.ts`.

## Deployment

- The application is configured for deployment on Vercel.
- Environment variables need to be set for Convex, Clerk, and Stripe in the deployment environment.

When working with this codebase, focus on these key areas and patterns to maintain consistency and leverage the existing infrastructure.
