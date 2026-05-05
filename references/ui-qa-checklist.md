# UI QA Checklist

Use this for any frontend or product presentation work.

## States

- Loading state matches final layout dimensions.
- Empty state explains next action without marketing filler.
- Error state is specific and recoverable.
- Stale/offline/reconnecting state exists when data can become stale.
- Disabled/blocked state explains why action is unavailable.
- Success state is calm and clear.

## Interaction

- Keyboard focus is visible.
- Touch targets are at least 44px.
- Hover/active states exist for interactive controls.
- Motion uses transform/opacity, not layout properties.
- Reduced-motion fallback exists for non-essential animation.
- No animation hides or delays critical operational data.

## Responsive

- No horizontal overflow at common mobile widths.
- Text does not clip inside buttons, cards, tabs, tables, or nav.
- Dense tables have mobile handling: scroll, collapse, or summary.
- Safe-area and `100dvh` issues are handled for full-height surfaces.

## Visual Quality

- Color swatches and tokens are consistent.
- Typography scale is intentional.
- Numeric data uses tabular/monospace treatment where useful.
- Cards are not nested unnecessarily.
- Icons are consistent in family/stroke/size.
- No generic placeholder names, lorem ipsum, dead links, or fake-perfect metrics.

## Product Honesty

- UI does not imply backend enforcement that does not exist.
- UI copy matches actual behavior.
- User-visible labels match domain language.
