# Workflow: Update UI From Stitch

This workflow defines the procedure for synchronizing UI designs, design tokens, and components exported from Stitch into the frontend applications in `apps/`.

---

## Objectives
- Maintain high-fidelity alignment between Stitch design specifications and frontend implementation.
- Preserve consistent design tokens (colors, typography, spacing, shadows).
- Avoid visual regressions and ensure responsive layout compliance.

---

## Process Steps

### Step 1: Ingest Stitch Specifications
1. Review the Stitch design export, spec tokens, or component files.
2. Note changes in:
   - Color palettes, typography hierarchy, border radiuses, and shadows.
   - Component layouts, responsiveness breakpoints, and interaction states (hover, active, focus, disabled).
   - Asset updates (SVGs, iconography, imagery).

### Step 2: Update Design Tokens & Styles
1. Update shared CSS custom properties or design token files in `apps/` or shared styling packages.
2. Ensure tokens use systematic naming conventions (`--color-primary`, `--spacing-md`, etc.).
3. Verify dark mode and contrast accessibility ratios meet WCAG AA standards.

### Step 3: Implement / Update UI Components
1. Apply layout changes using semantic HTML and clean CSS structure.
2. Avoid hardcoded ad-hoc styles; reference design system tokens.
3. Ensure interactive states have smooth transitions and micro-animations where appropriate.
4. Verify responsive behavior across mobile, tablet, and desktop breakpoints.

### Step 4: Verification & Visual Polish
1. Run local dev server and inspect rendered components in browser.
2. Compare side-by-side with Stitch reference designs.
3. Ensure accessibility (ARIA labels, keyboard navigation, tab index).
4. Run frontend tests and linters to verify clean integration.
