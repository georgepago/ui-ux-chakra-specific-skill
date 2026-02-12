# {{TITLE}}

{{DESCRIPTION}}
{{QUICK_REFERENCE}}
## Prerequisites

Check if Python is installed:

```bash
python3 --version || python --version
```

If Python is not installed, install it based on user's OS:

**macOS:**
```bash
brew install python3
```

**Ubuntu/Debian:**
```bash
sudo apt update && sudo apt install python3
```

**Windows:**
```powershell
winget install Python.Python.3.12
```

---

## How to Use This {{SKILL_OR_WORKFLOW}}

When user requests UI/UX work (design, build, create, implement, review, fix, improve), follow this workflow:

### Step 1: Analyze User Requirements

Extract key information from user request:
- **Product type**: SaaS, e-commerce, portfolio, dashboard, landing page, etc.
- **Style keywords**: minimal, playful, professional, elegant, dark mode, etc.
- **Industry**: healthcare, fintech, gaming, education, etc.
- **Stack**: Auto-detect from package.json (Chakra UI, React, Next.js, Vue, Svelte, Tailwind), or ask user if unclear

### Step 2: Generate Design System (REQUIRED)

**Always start with `--design-system`** to get comprehensive recommendations with reasoning:

```bash
python3 {{SCRIPT_PATH}} "<product_type> <industry> <keywords>" --design-system --auto-detect [-p "Project Name"]
```

This command:
1. Auto-detects your framework stack from package.json
2. Searches 5 domains in parallel (product, style, color, landing, typography)
3. Applies reasoning rules from `ui-reasoning.csv` to select best matches
4. Returns complete design system: pattern, style, colors, typography, effects
5. Includes anti-patterns to avoid
6. For Chakra UI projects: outputs `extendTheme()` config and JSX component examples

**Example:**
```bash
python3 {{SCRIPT_PATH}} "beauty spa wellness service" --design-system -p "Serenity Spa"
```

### Step 2b: Persist Design System (Master + Overrides Pattern)

To save the design system for hierarchical retrieval across sessions, add `--persist`:

```bash
python3 {{SCRIPT_PATH}} "<query>" --design-system --persist -p "Project Name" --auto-detect
```

This creates:
- `design-system/MASTER.md` — Global Source of Truth with all design rules (framework-specific component specs)
- `design-system/pages/` — Folder for page-specific overrides

**With page-specific override:**
```bash
python3 {{SCRIPT_PATH}} "<query>" --design-system --persist -p "Project Name" --page "dashboard"
```

This also creates:
- `design-system/pages/dashboard.md` — Page-specific deviations from Master

**How hierarchical retrieval works:**
1. When building a specific page (e.g., "Checkout"), first check `design-system/pages/checkout.md`
2. If the page file exists, its rules **override** the Master file
3. If not, use `design-system/MASTER.md` exclusively

### Step 3: Supplement with Detailed Searches (as needed)

After getting the design system, use domain searches to get additional details:

```bash
python3 {{SCRIPT_PATH}} "<keyword>" --domain <domain> [-n <max_results>]
```

**When to use detailed searches:**

| Need | Domain | Example |
|------|--------|---------|
| More style options | `style` | `--domain style "glassmorphism dark"` |
| Chart recommendations | `chart` | `--domain chart "real-time dashboard"` |
| UX best practices | `ux` | `--domain ux "animation accessibility"` |
| Alternative fonts | `typography` | `--domain typography "elegant luxury"` |
| Landing structure | `landing` | `--domain landing "hero social-proof"` |

### Step 4: Stack Guidelines (Auto-Detect or Specify)

Get implementation-specific best practices. **Auto-detect** from the project's package.json, or specify manually.

```bash
# Auto-detect stack from project
python3 {{SCRIPT_PATH}} "<keyword>" --auto-detect

# Or specify explicitly
python3 {{SCRIPT_PATH}} "<keyword>" --stack chakra-ui
```

Available stacks: `chakra-ui`, `html-tailwind`, `react`, `nextjs`, `vue`, `svelte`, `astro`, `nuxtjs`, `nuxt-ui`, `shadcn`

---

## Search Reference

### Available Domains

| Domain | Use For | Example Keywords |
|--------|---------|------------------|
| `product` | Product type recommendations | SaaS, e-commerce, portfolio, healthcare, beauty, service |
| `style` | UI styles, colors, effects | glassmorphism, minimalism, dark mode, brutalism |
| `typography` | Font pairings, Google Fonts | elegant, playful, professional, modern |
| `color` | Color palettes by product type | saas, ecommerce, healthcare, beauty, fintech, service |
| `landing` | Page structure, CTA strategies | hero, hero-centric, testimonial, pricing, social-proof |
| `chart` | Chart types, library recommendations | trend, comparison, timeline, funnel, pie |
| `ux` | Best practices, anti-patterns | animation, accessibility, z-index, loading |
| `react` | React/Next.js performance | waterfall, bundle, suspense, memo, rerender, cache |
| `web` | Web interface guidelines | aria, focus, keyboard, semantic, virtualize |
| `prompt` | AI prompts, CSS keywords | (style name) |

### Available Stacks

| Stack | Focus |
|-------|-------|
| `chakra-ui` | Theme system, component props, colorScheme, dark mode, layout primitives |
| `html-tailwind` | Tailwind utilities, responsive, a11y |
| `react` | State, hooks, performance, patterns |
| `nextjs` | SSR, routing, images, API routes |
| `vue` | Composition API, Pinia, Vue Router |
| `svelte` | Runes, stores, SvelteKit |
| `astro` | Islands, content collections, SSG |
| `nuxtjs` | Nuxt 3, composables, Nitro |
| `nuxt-ui` | Nuxt UI components, theming |
| `shadcn` | shadcn/ui components, theming, forms, patterns |

---

## Example Workflow

**User request:** "Build a car insurance verification dashboard"

### Step 1: Analyze Requirements
- Product type: SaaS / Insurance
- Style keywords: professional, clean, trust
- Industry: Insurance / Automotive
- Stack: Auto-detect (Chakra UI detected from package.json)

### Step 2: Generate Design System (REQUIRED)

```bash
python3 {{SCRIPT_PATH}} "insurance SaaS dashboard professional" --design-system --auto-detect -p "MyCar"
```

**Output:** Complete design system with pattern, style, colors, typography, effects, and Chakra UI component specs.

### Step 3: Supplement with Detailed Searches (as needed)

```bash
# Get UX guidelines for forms and accessibility
python3 {{SCRIPT_PATH}} "form accessibility validation" --domain ux

# Get alternative typography options if needed
python3 {{SCRIPT_PATH}} "professional clean trust" --domain typography
```

### Step 4: Stack Guidelines

```bash
python3 {{SCRIPT_PATH}} "theme components layout" --stack chakra-ui
```

**Then:** Synthesize design system + detailed searches and implement the design.

---

## Output Formats

The `--design-system` flag supports two output formats:

```bash
# ASCII box (default) - best for terminal display
python3 {{SCRIPT_PATH}} "fintech crypto" --design-system

# Markdown - best for documentation
python3 {{SCRIPT_PATH}} "fintech crypto" --design-system -f markdown
```

---

## Tips for Better Results

1. **Be specific with keywords** - "healthcare SaaS dashboard" > "app"
2. **Use --auto-detect** - Let the skill detect your framework for framework-specific output
3. **Combine domains** - Style + Typography + Color = Complete design system
4. **Always check UX** - Search "animation", "z-index", "accessibility" for common issues
5. **Use stack flag** - Get implementation-specific best practices
6. **Iterate** - If first search doesn't match, try different keywords

---

## Common Rules for Professional UI

These are frequently overlooked issues that make UI look unprofessional:

### Icons & Visual Elements

| Rule | Do | Don't |
|------|----|----- |
| **No emoji icons** | Use SVG icons (Heroicons, Lucide, Simple Icons) | Use emojis as UI icons |
| **Stable hover states** | Use color/opacity transitions on hover | Use scale transforms that shift layout |
| **Correct brand logos** | Research official SVG from Simple Icons | Guess or use incorrect logo paths |
| **Consistent icon sizing** | Use fixed viewBox (24x24) with consistent sizing | Mix different icon sizes randomly |

### Interaction & Cursor

| Rule | Do | Don't |
|------|----|----- |
| **Cursor pointer** | Add cursor pointer to all clickable/hoverable cards (Chakra: `cursor='pointer'`) | Leave default cursor on interactive elements |
| **Hover feedback** | Provide visual feedback via framework pseudo props (Chakra: `_hover={{ }}`) | No indication element is interactive |
| **Smooth transitions** | Use `transition='all 200ms ease'` or framework equivalent | Instant state changes or too slow (>500ms) |

### Light/Dark Mode Contrast

| Rule | Do | Don't |
|------|----|----- |
| **Mode-aware backgrounds** | Use `useColorModeValue('white', 'gray.800')` or framework equivalent | Hardcode single-mode colors |
| **Text contrast** | Use dark text on light backgrounds (4.5:1 minimum ratio) | Use gray-400 or lighter for body text |
| **Muted text** | Use `color='gray.600'` minimum for secondary text | Use colors below 4.5:1 contrast ratio |
| **Border visibility** | Use visible borders in both modes | Use invisible or near-invisible borders |

### Layout & Spacing

| Rule | Do | Don't |
|------|----|----- |
| **Floating navbar** | Add spacing from viewport edges for floating nav | Pin navbar flush to edges with no breathing room |
| **Content padding** | Account for fixed navbar height with padding-top | Let content hide behind fixed elements |
| **Consistent max-width** | Use `Container maxW='container.xl'` or equivalent consistently | Mix different container widths across pages |

---

## Pre-Delivery Checklist

Before delivering UI code, verify these items:

### Visual Quality
- [ ] No emojis used as icons (use SVG instead — Heroicons/Lucide)
- [ ] Brand logos verified from Simple Icons
- [ ] Hover states don't cause layout shift
- [ ] Colors come from theme tokens, not hardcoded hex values

### Interaction
- [ ] All clickable elements have cursor pointer (Chakra: `cursor='pointer'`)
- [ ] Hover/focus states via pseudo props (Chakra: `_hover`, `_focus`)
- [ ] Transitions smooth (150-300ms) — use `transition` prop
- [ ] Focus rings visible for keyboard navigation

### Light/Dark Mode
- [ ] Text contrast 4.5:1 minimum in both modes
- [ ] Mode-aware values used (Chakra: `useColorModeValue`)
- [ ] Borders visible in both modes
- [ ] Test both modes before delivery

### Theme & Framework
- [ ] `extendTheme()` includes all custom colors/spacing/typography (Chakra)
- [ ] `colorScheme` props on interactive components (Chakra)
- [ ] Component variants defined in theme, not inline (Chakra)
- [ ] `ChakraProvider` wraps app with custom theme

### Layout
- [ ] Floating elements have proper spacing from edges
- [ ] No content hidden behind fixed navbars
- [ ] Responsive at 375px, 768px, 1024px, 1440px (use responsive array/object syntax)
- [ ] No horizontal scroll on mobile

### Accessibility
- [ ] All images have alt text
- [ ] Form inputs wrapped in `FormControl` with `FormLabel` (Chakra)
- [ ] `aria-label` on all icon-only buttons (Chakra: `IconButton`)
- [ ] `prefers-reduced-motion` respected
