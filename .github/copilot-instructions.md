# Copilot Instructions for SvelteKit Project

## Project Overview
This is a modern SvelteKit project using TypeScript, Tailwind CSS v4, and Vite. The project follows SvelteKit's file-based routing conventions and is set up with comprehensive tooling for a professional development workflow.

## Key Architecture Patterns

### SvelteKit Structure
- **Routes**: Use the `src/routes/` directory with SvelteKit's file-based routing
- **Components**: Place reusable components in `src/lib/` (accessible via `$lib` alias)
- **App Shell**: Root layout in `src/routes/+layout.svelte`, HTML template in `src/app.html`
- **Static Assets**: Place in `static/` for direct serving, or `src/lib/assets/` for bundled assets

### Svelte 5 Syntax
- Use **runes syntax**: `let { children } = $props();` for component props
- Render children with: `{@render children?.()}`
- Import assets from `$lib/assets/` and reference them directly in templates

### Styling with Tailwind CSS v4
- Global styles in `src/app.css` with `@import 'tailwindcss';`
- Tailwind v4 is configured via Vite plugin in `vite.config.ts`
- Use utility classes directly in Svelte components

## Development Workflow

### Essential Commands
```bash
npm run dev          # Start development server
npm run build        # Production build
npm run preview      # Preview production build
npm run check        # Type checking with svelte-check
npm run check:watch  # Watch mode type checking
npm run lint         # ESLint + Prettier validation
npm run format       # Auto-format with Prettier
```

### Code Quality Setup
- **ESLint**: Modern flat config in `eslint.config.js` with TypeScript, Svelte, and Prettier integration
- **TypeScript**: Strict mode enabled, extends SvelteKit's generated config
- **Prettier**: Configured with Svelte and Tailwind plugins
- **Git Integration**: `.gitignore` patterns handled via `@eslint/compat`

## File Naming Conventions
- **Route files**: `+page.svelte`, `+layout.svelte`, `+error.svelte`
- **Load functions**: `+page.ts`, `+layout.ts`
- **Server routes**: `+page.server.ts`, `+layout.server.ts`
- **Components**: PascalCase `.svelte` files in `src/lib/`

## Import Patterns
```typescript
// SvelteKit aliases
import Component from '$lib/components/Component.svelte';
import { helper } from '$lib/utils';
import icon from '$lib/assets/icon.svg';

// Relative imports for routes
import '../app.css';
```

## Build Configuration Notes
- **Vite**: Handles bundling with SvelteKit and Tailwind plugins
- **Adapter**: Uses `@sveltejs/adapter-auto` for automatic deployment target detection
- **Preprocessing**: Uses `vitePreprocess()` for TypeScript/PostCSS support
- **Module Resolution**: Set to "bundler" mode for optimal Vite integration

## Best Practices
- Always run `npm run check` before committing to catch type errors
- Use the `$lib` alias for internal imports to maintain clean import paths
- Follow SvelteKit's conventions for data loading and form actions in route files
- Leverage Tailwind's utility-first approach instead of writing custom CSS