---
name: isometric-ui-animations
description: Build isometric UI components and animations using React and Tailwind CSS (v3 & v4). Use this skill to create reusable 3D isometric buttons, cards, grids, and layered interactions as functional React components.
---

# Isometric UI & Animations (React + Tailwind)

Use this skill to design and implement 3D isometric components using React and Tailwind CSS. Perfect for strategy game UIs, architectural layouts, and engaging 3D web interfaces built with React.

## Tailwind CSS v4 Integration

With Tailwind CSS v4, you can create powerful `@utility` classes to encapsulate complex isometric transforms, keeping your React components clean.

Add this to your CSS entry point:

```css
@import "tailwindcss";

/* Encapsulate the core isometric projection */
@utility iso-plane {
  transform: translateZ(0) rotateX(60deg) rotateZ(-45deg);
  transform-style: preserve-3d;
}

/* Custom floating animation */
@theme {
  --animate-iso-float: iso-float 3s ease-in-out infinite both;
}

@keyframes iso-float {
  0%, 100% { transform: translateY(0) translateX(0) rotateX(60deg) rotateZ(-45deg); }
  50% { transform: translateY(-10px) translateX(-10px) rotateX(60deg) rotateZ(-45deg); }
}
```

## Core React Components

### 1) Isometric Card (`<IsometricCard>`)

Use for grid tiles, base structures, or floating UI cards.

```tsx
import React from 'react';

export const IsometricCard = ({ children, depthColor = '#334155', className = '' }) => {
  return (
    <div 
      // Using the v4 @utility `iso-plane` instead of verbose arbitrary values
      className={`relative iso-plane bg-slate-700 border border-slate-600 w-32 h-32 transition-all duration-300 ease-out hover:-translate-y-2 hover:-translate-x-2 ${className}`}
      style={{
        boxShadow: `1px 1px 0 ${depthColor}, 2px 2px 0 ${depthColor}, 3px 3px 0 ${depthColor}, 4px 4px 0 ${depthColor}`
      }}
    >
      {children}
    </div>
  );
};
```

*Note: For dynamic `depthColor`, inline styles for `boxShadow` are useful. If the color is static, prefer pure Tailwind classes like `shadow-[1px_1px_0_var(--color-slate-700),...]*.*

### 2) Isometric Button (`<IsometricButton>`)

Buttons must have a tactile "press" animation that reduces their 3D depth to 0. Tailwind's `active:` modifier handles the depression instantly.

```tsx
import React from 'react';

export const IsometricButton = ({ onClick, children, className = '' }) => {
  return (
    <button 
      onClick={onClick}
      className={`relative iso-plane bg-indigo-500 border border-indigo-400 text-white w-24 h-24 flex items-center justify-center transition-all duration-150 ease-out shadow-[1px_1px_0_#3730a3,2px_2px_0_#3730a3,3px_3px_0_#3730a3,4px_4px_0_#3730a3] -translate-y-1 -translate-x-1 active:translate-y-0 active:translate-x-0 active:shadow-none hover:brightness-110 ${className}`}
    >
      {children}
    </button>
  );
};
```

## Advanced Shape Composition (Multi-Face Prism)

For true 3D structures like cubes or buildings, use absolute positioning. 

```tsx
import React from 'react';

export const IsometricPrism = ({ 
  topColor = 'bg-sky-400', 
  leftColor = 'bg-sky-600', 
  rightColor = 'bg-sky-800' 
}) => {
  return (
    <div className="relative w-32 h-32 iso-plane">
      {/* Top Face */}
      <div className={`absolute inset-0 ${topColor}`}></div>
      
      {/* Left Face */}
      <div className={`absolute inset-0 ${leftColor} origin-bottom rotate-x-[-90deg] translate-y-full h-8`}></div>
      
      {/* Right Face */}
      <div className={`absolute inset-0 ${rightColor} origin-right rotate-y-[90deg] translate-x-full w-8`}></div>
    </div>
  );
};
```

## Dynamic Grids & Staggered Animations

When rendering a grid of isometric tiles, use React's `index` to dynamically apply inline animation delays for staggered entrance effects.

```tsx
import React from 'react';

const gridData = Array.from({ length: 9 });

export const IsometricGrid = () => {
  return (
    <div className="grid grid-cols-3 gap-8 p-12">
      {gridData.map((_, index) => (
        <div 
          key={index}
          className="animate-iso-float"
          style={{ animationDelay: `${index * 150}ms` }}
        >
          <IsometricCard />
        </div>
      ))}
    </div>
  );
};
```

## Interaction Rules

- **Hover**: Objects should "lift" (move up and left on screen: `-translate-y-* -translate-x-*`, increasing shadow length).
- **Active**: Objects should "press" (move down and right on screen: `translate-y-0 translate-x-0`, decreasing shadow length).
- **Cursors**: Use `cursor-pointer` for interactive isometric elements. Keep drag interactions to `cursor-grab`.

## Anti-Patterns

- Mixing 2D flat interactions (like standard scaling `active:scale-95`) with 3D isometric elements. 3D elements press down, they don't scale.
- Binding React state (`isPressed`) just to trigger translation classes when Tailwind's native `active:` handles it natively and faster.
