---
description: Tailwind CSS usage rules for styling (2025 best practices)
globs: **/*.{html,js,jsx,ts,tsx,vue,svelte,css,scss,sass,md,mdx,php,blade.php,ejs,hbs,twig,liquid,njk,pug,astro,xml,json,yml,yaml,svg}
---

## General Guidelines
- Use Tailwind utility classes for consistent styling, with custom CSS only for special cases  
- Organize classes logically (layout, spacing, color, typography)  
- Use responsive and state variants (e.g., sm:, md:, lg:, hover:, focus:, dark:) in markup  
- Embrace Tailwind v4 features like container queries and CSS variables  
- Keep `tailwind.config.ts` updated with design tokens and purge paths  
- Rely on Tailwind classes rather than inline styles or external CSS files for a unified design language

## Configuration (CSS Files)
- Use the `@theme` directive to define custom design tokens like fonts, breakpoints, and colors
- Prefer modern color formats such as `oklch` for better color gamut support, defining them in the `:root` scope
- Take advantage of automatic content detection, which eliminates the need for a `content` array in configuration
- Rely on Oxide engine to scan project files, excluding those in `.gitignore` and binary extensions
- Add specific sources with `@source` only when necessary
- Extend Tailwind with custom utilities using the `@utility` directive in CSS files

## Styling (CSS Files)
- Incorporate 3D transform utilities like `rotate-x-*`, `rotate-y-*`, and `scale-z-*` for advanced visual effects
- Implement container queries with `@container`, `@max-*`, and `@min-*` utilities for adaptive layouts
- Use arbitrary values and properties with square bracket notation (e.g., `[mask-type:luminance]` or `top-[117px]`)
- Apply modifiers like `hover` or `lg` with arbitrary values for flexible styling
- Use the `not-*` variant for `:not()` pseudo-classes and the `starting` variant for `@starting-style`
- Check browser support for advanced features like `@starting-style` using resources like caniuse

## Components (HTML)
- Apply Tailwind utility classes directly in HTML for styling components
- Use dynamic arbitrary values like `grid-cols-[1fr_500px_2fr]` for flexible layouts
- Implement data attribute variants like `data-current:opacity-100` for conditional styling
- Ensure accessibility by pairing Tailwind utilities with appropriate ARIA attributes
- Use `aria-hidden="true"` or `role="presentation"` when applying utilities like `hidden` or `sr-only`

## Components (TypeScript/JavaScript)
- Prefer TypeScript over JavaScript for component files to ensure type safety when applying Tailwind classes
- Use dynamic utility classes with template literals or arrays (e.g., `className={`p-${padding} bg-${color}`}`)
- Validate dynamic values with TypeScript types
- Integrate Tailwind with modern frameworks by applying utilities in component logic
- Favor functional components over class-based ones in frameworks like React

## Project-Wide Systems
- Leverage the Oxide engine's fast build times for performance optimization
- Avoid manual content configuration unless explicitly required
- Maintain consistency by using theme variables defined in CSS configuration files
- Reference theme variables in both utility classes and custom CSS (e.g., `text-[--color-primary]`)
- Update rules regularly to reflect Tailwind v4's evolving feature set
- Be aware of deprecated options from v3.x like `text-opacity`
