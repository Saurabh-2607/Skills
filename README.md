# UI Skills Repository

This repository contains a collection of advanced UI/UX and styling skills tailored for AI agents, primarily focusing on Tailwind CSS and React.

## Included Skills

### 1. Skeuomorphic UI (`skeuomorphic-ui`)
Generates hyper-real, tactile graphical components using Tailwind CSS. Enforces rules for precise photon scattering, z-axis ordering, material emulation, and complex drop-shadow layering to create authentic hardware interfaces.

### 2. Isometric UI Animations (`isometric-ui-animations`)
Builds 3D isometric components and animations using React and Tailwind CSS. Perfect for strategy game UIs, architectural layouts, and engaging 3D web interfaces. Features true isometric projection using CSS transforms and tactile hover/press interaction states.

## Installation

You can install these skills directly into your agent via `npx skills add`:

```bash
npx skills add https://github.com/Saurabh-2607/Skills --skill skeuomorphic-ui
npx skills add https://github.com/Saurabh-2607/Skills --skill isometric-ui-animations
```

## Quick Examples

### Skeuomorphic Dark Mode Button
A tactile button that mimics darkened, non-glossy polymer separating from the backdrop.

```html
<button class="
  bg-gradient-to-b from-[#252525] to-[#1c1c1c]
  border border-black/20
  shadow-[0_2px_1px_#ffffff15_inset,0_1px_2px_#ffffff20_inset,0_20px_32px_-4px_#00000050,0_40px_64px_-8px_#00000035,0_0px_30px_4px_#00000025]
  rounded-lg px-6 py-3 text-[#e0e0e0] font-medium
  active:scale-[0.97] transition-all duration-75 ease-out
">
  Power On
</button>
```

### Isometric Card (React + Tailwind)
A 3D isometric tile utilizing React inline styles for dynamic shadow depth and Tailwind CSS for rotational projection.

```tsx
<div 
  className="relative transform-gpu preserve-3d rotate-x-[60deg] -rotate-z-[45deg] bg-slate-700 border border-slate-600 w-32 h-32 transition-all duration-300 ease-out hover:-translate-y-2 hover:-translate-x-2"
  style={{
    boxShadow: `1px 1px 0 #334155, 2px 2px 0 #334155, 3px 3px 0 #334155, 4px 4px 0 #334155`
  }}
>
  Tile Content
</div>
```
