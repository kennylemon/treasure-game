# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm install      # Install dependencies
npm run dev      # Start dev server on port 3000 (auto-opens browser)
npm run build    # Production build to build/
```

No test or lint scripts are configured.

## Architecture

This is a single-page React + TypeScript game with no backend.

**Core file:** [src/App.tsx](src/App.tsx) — all game state and logic lives here.
- State: `boxes[]` (each box has an `isOpen` and `hasItem` flag), `score`, `gameEnded`
- On mount, one of the 3 boxes is randomly assigned the treasure
- Clicking a box: +100 for treasure, -50 for skeleton; game ends when treasure is found or all boxes opened
- Animations via `motion/react` (Framer Motion) — 3D flip effect using `rotateY`
- Sound effects: `src/audios/chest_open.mp3` (treasure) and `chest_open_with_evil_laugh.mp3` (skeleton)

**UI components:** [src/components/ui/](src/components/ui/) — 46 shadcn/ui-style components built on Radix UI primitives. Import from here rather than adding new UI libraries.

**Styling:** Tailwind CSS with design tokens defined as CSS variables in [src/styles/globals.css](src/styles/globals.css). Use `@` as alias for `src/`.

**Assets:** Images in [src/assets/](src/assets/) (`treasure_closed.png`, `treasure_opened.png`, `treasure_opened_skeleton.png`, `key.png`). Use [src/components/figma/ImageWithFallback.tsx](src/components/figma/ImageWithFallback.tsx) for graceful image loading.
