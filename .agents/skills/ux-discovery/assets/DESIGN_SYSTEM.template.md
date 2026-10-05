# Design System

## Status

Established / Partial / Not established.

## Figma

- Design system/library: <URL if available>
- Product design file(s): <URL if available>

## Foundations

Document only foundations that actually exist.

- Color
- Typography
- Spacing
- Radius
- Elevation
- Grid/layout
- Breakpoints
- Motion

## Tokens

Map semantic Figma variables to code tokens when known.

| Concept | Figma | Code |
| --- | --- | --- |
| Example | `color/background/primary` | `--color-background-primary` |

## Components

Map design components to code components when known.

| Figma component | Code component | Notes |
| --- | --- | --- |
| Example | `src/components/Button` | variants should stay aligned |

## Patterns

Reusable interaction or composition patterns that are broader than one component.

## Accessibility

Stable accessibility expectations for the system.

## Naming and implementation rules

- Prefer semantic tokens over raw values.
- Reuse existing components before creating new ones.
- Record actual project conventions here; do not invent conventions to fill this document.

## Known gaps / drift

Known differences between Figma and code, missing components, or migration work.
