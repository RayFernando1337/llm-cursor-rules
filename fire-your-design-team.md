# shadcn/ui with Tailwind v4 Design System Guidelines

This document outlines design principles and implementation guidelines for applications using shadcn/ui with Tailwind v4. These guidelines ensure consistency, accessibility, and best practices throughout the UI development process.

## Core Design Principles

### 1. Typography System: 4 Sizes, 2 Weights
- **4 Font Sizes Only**:
  - Size 1: Large headings
  - Size 2: Subheadings/Important content
  - Size 3: Body text
  - Size 4: Small text/labels
- **2 Font Weights Only**:
  - Semibold: For headings and emphasis
  - Regular: For body text and general content
- **Consistent Hierarchy**: Maintain clear visual hierarchy with limited options

### 2. 8pt Grid System
- **All spacing values must be divisible by 8 or 4**
- **Examples**:
  - Instead of 25px padding → Use 24px (divisible by 8)
  - Instead of 11px margin → Use 12px (divisible by 4)
- **Consistent Rhythm**: Creates visual harmony throughout the interface

### 3. 60/30/10 Color Rule
- **60%**: Neutral color (white/light gray)
- **30%**: Complementary color (dark gray/black)
- **10%**: Main brand/accent color (e.g., red, blue)
- **Color Balance**: Prevents visual stress while maintaining hierarchy

### 4. Clean Visual Structure
- **Logical Grouping**: Related elements should be visually connected
- **Deliberate Spacing**: Spacing between elements should follow the grid system
- **Alignment**: Elements should be properly aligned within their containers
- **Simplicity Over Flashiness**: Focus on clarity and function first

## Foundation

### Tailwind v4 Integration
- **Use Tailwind CSS v4 for styling**: Leverage the latest Tailwind features including the new @theme directive, dynamic utility values, and OKLCH colors. [Tailwind CSS v4 Documentation](mdc:https://tailwindcss.com/docs)
- **Modern browsing features**: Tailwind v4 uses bleeding-edge browser features and is designed for modern browsers.
- **Simplified installation**: Fewer dependencies, zero configuration required in many cases.
- **shadcn/ui v4 demo**: Reference the demo site for component examples. [shadcn/ui v4 Demo](mdc:https://v4.shadcn.com/)

### New CSS Structure
- **Replace @layer base with @theme directive**:
  ```css
  /* Old approach in v3 */
  @layer base {
    :root {
      --background: 0 0% 100%;
      --foreground: 0 0% 3.9%;
    }
  }
  
  /* New approach in v4 */
  @theme {
    --color-background: hsl(var(--background));
    --color-foreground: hsl(var(--foreground));
  }
  ```
- **Tailwind imports**: Use `@import "tailwindcss"` instead of `@tailwind base`
- **Container queries**: Built-in support without plugins
- **OKLCH color format**: Updated from HSL for better color perception

## Typography System

### Font Sizes & Weights
- **Strictly limit to 4 distinct sizes**:
  - Size 1: Large headings (largest)
  - Size 2: Subheadings
  - Size 3: Body text
  - Size 4: Small text/labels (smallest)
- **Only use 2 font weights**:
  - Semibold: For headings and emphasis
  - Regular: For body text and most UI elements
- **Common mistakes to avoid**:
  - Using more than 4 font sizes
  - Introducing additional font weights
  - Inconsistent size application

### Typography Implementation
- **Reference shadcn's typography primitives** for consistent text styling
- **Use monospace variant** for numerical data when appropriate
- **data-slot attribute**: Every shadcn/ui primitive now has a data-slot attribute for styling
- **Maintain hierarchy** using consistent sizing patterns

## 8pt Grid System

### Spacing Guidelines
- **All spacing values MUST be divisible by 8 or 4**:
  - ✅ DO: Use 8, 16, 24, 32, 40, 48, etc.
  - ❌ DON'T: Use 25, 11, 7, 13, etc.

- **Practical examples**:
  - Instead of 25px padding → Use 24px (divisible by 8)
  - Instead of 11px margin → Use 12px (divisible by 4)
  - Instead of 15px gap → Use 16px (divisible by 8)

- **Use Tailwind's spacing utilities**:
  - p-4 (16px), p-6 (24px), p-8 (32px)
  - m-2 (8px), m-4 (16px), m-6 (24px)
  - gap-2 (8px), gap-4 (16px), gap-8 (32px)

- **Why this matters**:
  - Creates visual harmony
  - Simplifies decision-making
  - Establishes predictable patterns

### Implementation
- **Tailwind v4 dynamic spacing**: Spacing utilities accept any value without arbitrary syntax
- **Consistent component spacing**: Group related elements with matching gap values
- **Check responsive behavior**: Ensure grid system holds at all breakpoints

## 60/30/10 Color Rule

### Color Distribution
- **60%**: neutral color (bg-background)
  - Usually white or light gray in light mode
  - Dark gray or black in dark mode
  - Used for primary backgrounds, cards, containers

- **30%**: complementary color (text-foreground)
  - Usually dark gray or black in light mode
  - Light gray or white in dark mode
  - Used for text, icons, subtle UI elements

- **10%**: accent color (brand color)
  - Your primary brand color (red, blue, etc.)
  - Used sparingly for call-to-action buttons, highlights, important indicators
  - Avoid overusing to prevent visual stress

### Common Mistakes
- ❌ Overusing accent colors creates visual stress
- ❌ Not enough contrast between background and text
- ❌ Too many competing accent colors (stick to one primary accent)

### Implementation with shadcn/ui
- **Background/foreground convention**: Each component uses the background/foreground pattern
- **CSS variables in globals.css**:
  ```css
  :root {
    --background: oklch(1 0 0);
    --foreground: oklch(0.145 0 0);
    --primary: oklch(0.205 0 0);
    --primary-foreground: oklch(0.985 0 0);
    /* Additional variables */
  }
  
  @theme {
    --color-background: var(--background);
    --color-foreground: var(--foreground);
    /* Register other variables */
  }
  ```
- **OKLCH color format**: More accessible colors, especially in dark mode
- **Reserve accent colors** for important elements that need attention

## Component Architecture

### shadcn/ui Component Structure
- **2-layered architecture**:
  1. Structure and behavior layer (Radix UI primitives)
  2. Style layer (Tailwind CSS)
- **Class Variance Authority (CVA)** for variant styling
- **data-slot attribute** for styling component parts

### Implementation
- **Install components individually** using CLI (updated for v4) or manual installation
- **Component customization**: Modify components directly as needed
- **Radix UI primitives**: Base components for accessibility and behavior
- **New-York style**: Default recommended style for new projects (deprecated "default" style)

## Visual Hierarchy

### Design Principles
- **Simplicity over flashiness**: Focus on clarity and usability
- **Emphasis on what matters**: Highlight important elements
- **Reduced cognitive load**: Use consistent terminology and patterns
- **Visual connection**: Connect related UI elements through consistent patterns

### Implementation
- **Use shadcn/ui Blocks** for common UI patterns
- **Maintain consistent spacing** between related elements
- **Align elements properly** within containers
- **Logical grouping** of related functionality

## Installation & Setup

### Project Setup
- **CLI initialization**:
  ```bash
  npx create-next-app@latest my-app
  cd my-app
  npx shadcn-ui@latest init
  ```
- **Manual setup**: Follow the guide at [Manual Installation](mdc:https://ui.shadcn.com/docs/installation/manual)
- **components.json configuration**:
  ```json
  {
    "style": "new-york",
    "rsc": true,
    "tailwind": {
      "config": "",
      "css": "app/globals.css",
      "baseColor": "neutral",
      "cssVariables": true
    },
    "aliases": {
      "components": "@/components",
      "utils": "@/lib/utils"
    }
  }
  ```

### Adding Components
- **Use the CLI**: `npx shadcn-ui@latest add button`
- **Install dependencies**: Required for each component
- **Find components**: [Component Reference](mdc:https://ui.shadcn.com/docs/components)

## Advanced Features

### Dark Mode
- **Updated dark mode colors** for better accessibility using OKLCH
- **Consistent contrast ratios** across light and dark themes
- **Custom variant**: `@custom-variant dark (&:is(.dark *))`

### Container Queries
- **Built-in support** without plugins
- **Responsive components** that adapt to their container size
- **@min-* and @max-* variants** for container query ranges

### Data Visualization
- **Chart components**: Use with consistent styling
- **Consistent color patterns**: Use chart-1 through chart-5 variables

## Experience Design

### Motion & Animation
- **Consider transitions** between screens and states
- **Animation purpose**: Enhance usability, not distract
- **Consistent motion patterns**: Similar elements should move similarly

### Implementation
- **Test experiences** across the entire flow
- **Design with animation in mind** from the beginning
- **Balance speed and smoothness** for optimal user experience

## Resources

- [shadcn/ui Documentation](mdc:https://ui.shadcn.com/docs)
- [Tailwind CSS v4 Documentation](mdc:https://tailwindcss.com/docs)
- [shadcn/ui GitHub Repository](mdc:https://github.com/shadcn/ui)
- [Tailwind v4 Upgrade Guide](mdc:https://tailwindcss.com/docs/upgrade-guide)
- [shadcn/ui v4 Demo](mdc:https://v4.shadcn.com/)
- [Figma Design System](mdc:https://www.figma.com/community/file/1203061493325953101/shadcn-ui-design-system)

## Code Review Checklist

### Core Design Principles
- [ ] Typography: Uses only 4 font sizes and 2 font weights (Semibold, Regular)
- [ ] Spacing: All spacing values are divisible by 8 or 4
- [ ] Colors: Follows 60/30/10 color distribution (60% neutral, 30% complementary, 10% accent)
- [ ] Structure: Elements are logically grouped with consistent spacing

### Technical Implementation
- [ ] Uses proper OKLCH color variables
- [ ] Leverages @theme directive for variables
- [ ] Components implement data-slot attribute properly
- [ ] Visual hierarchy is clear and consistent
- [ ] Components use Class Variance Authority for variants
- [ ] Dark mode implementation is consistent
- [ ] Accessibility standards are maintained (contrast, keyboard navigation, etc.)

### Common Issues to Flag
- [ ] Too many font sizes (more than 4)
- [ ] Inconsistent spacing values (not divisible by 8 or 4)
- [ ] Overuse of accent colors (exceeding 10%)
- [ ] Random or inconsistent margins/padding
- [ ] Insufficient contrast between text and background
- [ ] Unnecessary custom CSS when Tailwind utilities would suffice
