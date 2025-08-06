# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Main Project Goal

We are updating the design and layout of the SimpleTPA website https://simpletpa.com/ from a legacy wordpress site, located in the legacy-example folder, to a modern, sleek, static Svelte website we will deploy on Vercel. We want the new website to mimic the design and feel of the https://linear.app/ website, shown in the design-inspiration folder.

## Development Commands

- **Start development server**: `npm run dev` - Runs Vite dev server with HMR
- **Build for production**: `npm run build` - Creates optimized production build in `dist/`
- **Preview production build**: `npm run preview` - Serves production build locally

## Project Architecture

This is a **Svelte 5 + Vite** project using the modern Svelte runes syntax (`$state`, `$derived`, etc.). Key architectural decisions:

### Build System
- **Vite** as the build tool and development server
- **@sveltejs/vite-plugin-svelte** for Svelte compilation
- Output directory: `dist/`
- Uses ES modules (`"type": "module"` in package.json)

### Svelte Configuration
- **Svelte 5** with runes enabled (modern reactive syntax)
- **vitePreprocess** for CSS/JS preprocessing
- Component structure follows standard Svelte patterns

### TypeScript/JavaScript Setup
- Uses JavaScript with TypeScript checking enabled (`checkJs: true`)
- **jsconfig.json** provides type checking for `.svelte` and `.js` files
- Modern ES module syntax with bundler module resolution
- Source maps enabled for debugging

### Application Structure
- **Entry point**: `src/main.js` - Uses Svelte 5's `mount()` API
- **Main component**: `src/App.svelte` - Root application component
- **Components**: Stored in `src/lib/` directory
- **Assets**: Static assets in `src/assets/` and `public/`
- **Styles**: Global styles in `src/app.css`

### State Management
- Uses Svelte 5 runes (`$state()`, `$derived()`) instead of legacy stores
- Components use modern reactive syntax with `let variable = $state(initialValue)`

### Deployment
- Configured for **Vercel** deployment with `vercel.json`
- Static site generation using `@vercel/static`

### Contact Form
The contact form will use FormSubmit.

## Important Notes

- This project uses **Svelte 5** syntax - avoid legacy `$:` reactive statements
- HMR state preservation is disabled by default (use external stores if needed)
- The project includes a large `legacy-example/` directory that contain the legacy SimpleTPA WordPress site assets. This will serve as the source of content for the new website.