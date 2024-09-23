# Rules for Next.js 14 Development

## General Guidelines

1. Use Next.js 14 with TypeScript and Tailwind CSS for optimal developer experience and type safety.
2. Use `bun` for all package installations and management.
3. Implement the App Router, which is the recommended routing system for Next.js 14.
4. Utilize Server Components by default, using Client Components only when necessary for interactivity or client-side state.
5. Leverage Server Actions for handling data mutations and form submissions.
6. Implement proper caching strategies using Next.js built-in caching mechanisms.
7. Ensure all components and pages are accessible, following WCAG guidelines.
8. Use environment variables for configuration following Next.js conventions.
9. Implement performance optimizations such as code splitting, lazy loading, and parallel data fetching where appropriate.
10. Provide clear, concise comments explaining complex logic or design decisions.

## Code Structure and Syntax

1. Use the `app` directory for all components and pages.
2. Implement the following file conventions in the `app` directory:
    - `layout.tsx`: For shared UI across multiple pages
    - `page.tsx`: For unique page content
    - `loading.tsx`: For loading UI
    - `error.tsx`: For error handling UI
    - `not-found.tsx`: For 404 pages
3. Use Server Components by default. Add the `'use client'` directive only when creating Client Components.
4. Define components using arrow function syntax with TypeScript:
    
    ```tsx
    import { FC } from 'react';
    
    interface ComponentProps {
      // Props definition
    }
    
    const Component: FC<ComponentProps> = ({ prop1, prop2 }) => {
      // Component logic
    };
    
    export default Component;
    
    ```
    
5. For page components, use default exports:
    
    ```tsx
    export default function Page() {
      // Page component logic
    }
    
    ```
    
6. If explicit typing is needed, prefer `React.FC` or `React.ReactNode`:
    
    ```tsx
    import React from 'react';
    
    const ComponentName: React.FC = () => {
      // Component logic
    };
    
    // OR
    
    const ComponentName = (): React.ReactNode => {
      // Component logic
    };
    
    ```
    

## Routing and Navigation

1. Implement nested routing using folder structure in the `app` directory.
2. Use the `<Link>` component from `next/link` for client-side navigation:
    
    ```tsx
    import Link from 'next/link';
    
    <Link href="/about">About</Link>
    
    ```
    
3. Implement dynamic routes using folder names with square brackets (e.g., `[id]`).
4. Use `generateStaticParams` for generating static paths in dynamic routes.

## Data Fetching and API Routes

1. Use Server Components and the `fetch` API for data fetching, leveraging Next.js automatic request deduplication:
    
    ```tsx
    async function getData() {
      const res = await fetch('<https://api.example.com/data>', { next: { revalidate: 3600 } });
      if (!res.ok) throw new Error('Failed to fetch data');
      return res.json();
    }
    
    export default async function Page() {
      const data = await getData();
      // Render component using data
    }
    
    ```
    
2. Implement Server Actions for data mutations:
    
    ```tsx
    'use server';
    
    import { revalidatePath } from 'next/cache';
    
    export async function updateData(formData: FormData) {
      // Update data in your database
      revalidatePath('/data');
    }
    
    ```
    
3. Use route handlers (route.ts) for API routes in the App Router.
4. Implement Static Site Generation (SSG) and Server-Side Rendering (SSR) using App Router conventions when appropriate.

## State Management and Interactivity

1. Use Server Actions for form submissions and data mutations:
    
    ```tsx
    import { updateData } from './actions';
    
    export default function Form() {
      return (
        <form action={updateData}>
          <input type="text" name="data" />
          <button type="submit">Update</button>
        </form>
      );
    }
    
    ```
    
2. Implement React hooks for client-side state management when necessary.
3. Use the `useState` and `useEffect` hooks in Client Components for local state and side effects.

## Styling

1. Use Tailwind CSS classes exclusively for styling. Avoid inline styles:
    
    ```tsx
    <div className="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
      {/* Component content */}
    </div>
    
    ```
    
2. Create custom Tailwind classes in the `tailwind.config.js` file for reusable styles.
3. Use CSS Modules for component-specific styles when needed.

## Performance Optimization

1. Implement automatic static optimization for eligible pages.
2. Use dynamic imports for code splitting:
    
    ```tsx
    import dynamic from 'next/dynamic';
    
    const DynamicComponent = dynamic(() => import('../components/DynamicComponent'));
    
    ```
    
3. Utilize the Image component from `next/image` for automatic image optimization:
    
    ```tsx
    import Image from 'next/image';
    
    <Image src="/image.jpg" alt="Description" width={500} height={300} />
    
    ```
    
4. Implement proper caching strategies using the Data Cache and Full Route Cache.
5. Use Next.js 14's built-in caching and revalidation features for optimal performance:
    
    ```tsx
    import { unstable_cache } from 'next/cache';
    
    const getCachedUser = unstable_cache(
      async (id: string) => getUser(id),
      ['user-cache'],
      { revalidate: 3600 } // Revalidate every hour
    );
    
    ```
    
6. Use on-demand revalidation when appropriate:
    
    ```tsx
    import { revalidatePath, revalidateTag } from 'next/cache';
    
    export async function updateData() {
      // Update data in your database
      revalidatePath('/data'); // Revalidate a specific path
      revalidateTag('data-tag'); // Revalidate all entries with this tag
    }
    
    ```
    
7. Implement parallel data fetching for improved performance:
    
    ```tsx
    async function ParallelDataFetch() {
      const dataPromise = fetch('<https://api.example.com/data>');
      const userPromise = fetch('<https://api.example.com/user>');
    
      const [data, user] = await Promise.all([
        dataPromise.then(res => res.json()),
        userPromise.then(res => res.json())
      ]);
    
      return { data, user };
    }
    
    ```
    

## Error Handling and Loading States

1. Create error.tsx files for error boundaries:
    
    ```tsx
    'use client';
    
    export default function Error({
      error,
      reset,
    }: {
      error: Error & { digest?: string };
      reset: () => void;
    }) {
      return (
        <div>
          <h2>Something went wrong!</h2>
          <button onClick={() => reset()}>Try again</button>
        </div>
      );
    }
    
    ```
    
2. Implement loading.tsx files for managing loading states.
3. Use React Suspense for more granular loading states:
    
    ```tsx
    import { Suspense } from 'react';
    
    export default function Page() {
      return (
        <Suspense fallback={<Loading />}>
          <SomeComponent />
        </Suspense>
      );
    }
    
    ```
    

## SEO and Metadata

1. Use the Metadata API for SEO optimization:
    
    ```tsx
    import type { Metadata } from 'next';
    
    export const metadata: Metadata = {
      title: 'Page Title',
      description: 'Page description',
    };
    
    ```
    
2. Implement dynamic metadata using generateMetadata for pages with dynamic content.

## Composer Mode-Specific Guidelines

1. When using Composer mode, provide clear, natural language descriptions of desired changes or additions.
2. For multi-file operations, specify the files involved and their relationships.
3. When requesting code generation, provide context about the desired functionality and how it fits into the existing project structure.
4. For refactoring tasks, describe the current code structure and the desired outcome.
5. When addressing errors, provide details about the error message and the surrounding code context.

Remember to adapt these rules based on specific project requirements and personal preferences. Always prioritize clean, efficient, and maintainable code that adheres to Next.js 14 best practices.
