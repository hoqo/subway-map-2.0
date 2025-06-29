# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

### Development
- `yarn dev` - Start development server
- `yarn build` - Build for production
- `yarn preview` - Preview production build

### Code Quality
- `yarn lint` - Run ESLint and Prettier checks
- `yarn format` - Auto-format code with Prettier
- `yarn check` - Run TypeScript and Svelte type checking
- `yarn check:watch` - Type checking in watch mode

## Architecture Overview

This is an interactive Kyiv subway map built with SvelteKit. The application renders an SVG-based visualization of the Kyiv metro system based on the official map.

### Core Components

**Map Component** (`src/lib/components/Map/Map.svelte`)
- Main visualization component that renders subway lines and stations
- Uses D3.js for Catmull-Rom curve interpolation between stations
- Integrates River component as background layer
- Fixed SVG viewBox of 3500x3500 for precise coordinate mapping

**Data Structure** (`src/lib/components/Map/mocks.ts`)
- Defines three subway lines: Blue, Red, and Green
- Each line contains an array of station nodes with x/y coordinates
- Stations can have optional names and bend directions

**Type System**
- `tPoint`: `{ x: number; y: number }`
- `iSubwayStation`: Station with point, optional name, bend direction, and adjacent station
- `iSubwayLine`: Extends `iMapItem` with array of station nodes
- `tBend`: Direction indicator for curved segments ('left' | 'right')

### Layout Structure
- Fixed grid layout: 82px header, 747px main map area, flexible footer
- Legend component displays line colors and river
- Uses Tailwind CSS v4 with custom styles in LESS

### Technology Stack
- **Framework**: SvelteKit with Svelte 5
- **Visualization**: D3.js for line generation
- **Styling**: Tailwind CSS + LESS preprocessor
- **TypeScript**: Strict mode with bundler module resolution