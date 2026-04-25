---
name: frontend-skill
description: Build modern frontend features with strong UX, mobile-first responsive design, shadcn/ui components, Zustand state management, Tailwind CSS, and performance optimization. Use when implementing, refactoring, or reviewing UI work in this project.
---

# Frontend Development Skill

## When to Apply

Apply this skill when the user asks for:
- new UI screens or component work
- responsive or mobile-first behavior
- `shadcn/ui` integration or customization
- `zustand` store creation/refactor
- `tailwindcss` styling and design consistency
- frontend performance optimization

## Default Standards

1. Build mobile-first, then scale up with breakpoints.
2. Prioritize clarity, hierarchy, spacing, and interaction feedback.
3. Keep implementation consistent with the product design and design system.
4. Keep state minimal, explicit, and colocated unless shared.
5. Treat performance as a feature, not a final pass.

## UI/UX Expectations

- Use clear visual hierarchy: heading, supporting text, and primary action.
- Keep spacing and typography consistent; avoid random size jumps.
- Match existing design patterns, component behavior, and visual language.
- Provide interaction states (`hover`, `focus-visible`, `active`, `disabled`, loading).
- Ensure accessible contrast and keyboard navigability.
- Add skeleton/empty/error states for async content.

## Responsive Development (Mobile-First)

1. Start with base classes for small screens.
2. Add `sm:`, `md:`, `lg:`, `xl:` only when layout actually needs it.
3. Use fluid widths and wrapping; avoid fixed pixel widths unless required.
4. Validate critical flows in common mobile viewport sizes before desktop polish.
5. Keep touch targets practical and avoid cramped click areas.

## shadcn/ui Guidelines

- Prefer `shadcn/ui` primitives before custom components.
- Compose existing primitives (`Dialog`, `Sheet`, `Popover`, `DropdownMenu`, `Form`) for consistency.
- Use variants and class composition rather than forking component logic.
- Keep styling aligned with design tokens and existing theme variables.
- If behavior diverges from defaults, document why in the component code.

## Design Consistency Checklist

Before finalizing UI changes, verify:
- typography scale and weights match existing screens
- spacing rhythm is aligned with current layout patterns
- color usage follows theme tokens and semantic intent
- component states/animations feel consistent with the rest of the app
- no new visual pattern is introduced when an existing one already fits

## Zustand Guidelines

- Create focused stores by domain; avoid one giant global store.
- Store only shared client state; derived values should be computed selectors.
- Use selectors to minimize re-renders (`useStore((s) => s.value)`).
- Keep actions deterministic and side effects explicit.
- For persistence, persist only fields that improve UX and are safe to keep.

## Tailwind Guidelines

- Use utility classes directly in components for fast iteration.
- Extract repeated class sets into small reusable UI components.
- Prefer semantic layout patterns (`grid`, `flex`, `gap`, `space-*`) over ad hoc margins.
- Use `cn()` patterns consistently for conditional classes.
- Avoid over-specific combinations that make later overrides hard.

## Performance Optimization Checklist

During implementation and before finalizing:
- minimize unnecessary client boundaries and large client-only trees
- avoid expensive rerenders with memoization/selectors where needed
- lazy-load heavy UI chunks and non-critical modules
- optimize images/assets and avoid oversized payloads
- keep bundle impact in mind when adding libraries
- verify perceived performance (loading state, input responsiveness, transitions)

## Delivery Workflow

1. Understand user outcome and key UI states.
2. Build the smallest functional version in mobile layout.
3. Add desktop scaling and polish.
4. Wire shared state with `zustand` only where needed.
5. Align styling with `tailwind` + `shadcn/ui` patterns.
6. Run quick performance pass and trim avoidable overhead.
7. Validate UX states: loading, empty, error, success, and disabled.
