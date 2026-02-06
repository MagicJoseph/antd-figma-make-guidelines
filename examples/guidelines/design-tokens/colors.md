# Color design tokens

## Naming pattern

FPL uses semantic color tokens following this pattern: `--color-{category}-{role}-{prominence}-{interaction}`
'category' is required; the remaining parts are optional. For instance, --color-bg-brand-hover has category, role, and interaction, but not prominence.

Use borders or background colors to separate sections.

### Quick Decision Tree to find a token

**Need a background color?**  
→ Start with `--color-bg-`  
→ Add role if semantic meaning needed  
→ Use `-hover` or `-pressed` for interactions

**Need text on that background?**  
→ If solid semantic color → use `--color-text-on{role}`  
→ If tertiary/light tint → use `--color-text-{role}`  
→ If default/neutral → use `--color-text`

**Need an icon color?**  
→ Usually matches the text color  
→ Same "on-" rules apply

**Need a border?**  
→ Start with `--color-border-`  
→ Add role/state as needed  
→ Use `-strong` for prominent outlines

## Categories

*   **bg**: Anytime you need a background or background-color
*   **text**: Anytime you need a color property for text
*   **icon**: For fill, stroke, or icon color CSS custom properties
*   **border**: For border, outline, border-color properties
*   **gauge**: Specifically for progress bars, loading indicators, status meters

## Roles

### Semantic/Status Roles

These communicate specific meanings in the UI:
- **`brand`** - Primary accent color (blue in Figma, purple in FigJam)  
 - Use for: Primary buttons, links, brand-colored elements  
 - Example: `--color-bg-brand`, `--color-text-brand`
- **`danger`** - Errors, destructive actions (red)  
 - Use for: Error messages, delete buttons, warnings requiring immediate attention  
 - Example: `--color-text-danger`, `--color-bg-danger`
...
- **`selected`** - Selection states (light blue/purple)  
 - Use for: Selected items, active states, focus indicators  
 - Example: `--color-bg-selected`, `--color-border-selected`
- **`info`** - Informational (blue)  
 - Use for: Informational banners, neutral alerts  
 - Example: `--color-bg-info`

### "On-" Roles

Content for text/icons that sit ON colored surfaces:
- **`onbrand`** - Content on brand-colored backgrounds (white)  
- **`ondanger`** - Content on danger-colored backgrounds (white)  
...
- **`onsuccess`** - Content on success-colored backgrounds (white)  
- **`onwarning`** - Content on warning-colored backgrounds (dark)  

```css
/* ✅ CORRECT - Solid colored backgrounds */  
.primaryButton {  
 background: var(--color-bg-brand);     /* Blue background */  
 color: var(--color-text-onbrand);      /* White text */  
 --color-icon: var(--color-icon-onbrand);  
}

.dangerButton {  
 background: var(--color-bg-danger);    /* Red background */  
 color: var(--color-text-ondanger);     /* White text */  
}

/* ❌ WRONG - Same-role tokens clash */  
.dangerButton {  
 background: var(--color-bg-danger);    /* Red */  
 color: var(--color-text-danger);       /* Also red - invisible! */  
}
```

**Rule:** If the background has a semantic color (brand, danger, success, warning), the content needs the "on-" version.

EXCEPTION: Do not use ON roles for light-tinted (usually tertiary) background colors:

```css
/* ✅ CORRECT - Tertiary (light tint) backgrounds */  
.errorBanner {  
 background: var(--color-bg-danger-tertiary);  /* Light red tint */  
 color: var(--color-text-danger);              /* Dark red text */  
}

.warningBanner {  
 background: var(--color-bg-warning-tertiary); /* Light yellow */  
 color: var(--color-text-warning);             /* Dark text */  
}

/* ❌ WRONG */  
.errorBanner {  
 background: var(--color-bg-danger-tertiary);  /* Light red */  
 color: var(--color-text-ondanger);            /* White - invisible! */  
}
```

**Rule:** Tertiary backgrounds are light tints, so they need regular-colored text for contrast.

### Product/Context-Specific Roles

- **`design`** - Design mode/files (blue)  
 - Use for: Design file indicators, design-specific features  
 - Example: `--color-bg-design`, `--color-icon-design`
- **`handoff`** - Dev mode/handoff features (green)  
 - Use for: Developer handoff features, dev mode indicators  
 - Example: `--color-bg-handoff`, `--color-text-handoff`
- **`measure`** - Measurement tools (red)  
 - Use for: Measurement indicators, spacing tools  
 - Example: `--color-bg-measure`, `--color-icon-measure`
- **`assistive`** - Assistive features (pink)  
 - Use for: Accessibility features, assistive tools  
 - Example: `--color-bg-assistive`, `--color-text-assistive`

### UI Context Roles

- **`menu`** - Menu items (dark grey)  
 - Use for: Dropdown menus, context menus  
 - Example: `--color-bg-menu`, `--color-text-menu`
- **`toolbar`** - Toolbar elements (dark grey)  
 - Use for: Top toolbar, floating toolbars  
 - Example: `--color-bg-toolbar`, `--color-icon-toolbar`
- **`tooltip`** - Tooltips (dark grey)  
 - Use for: Tooltip backgrounds and content  
 - Example: `--color-bg-tooltip`, `--color-text-tooltip`

### State/Appearance Roles

- **`disabled`** - Disabled/inactive states (grey)  
 - Use for: Disabled buttons, inputs, inactive elements  
 - Example: `--color-bg-disabled`, `--color-text-disabled`
- **`inverse`** - Inverse colors (dark on light, light on dark)  
 - Use for: Elements that need to contrast with the background  
 - Example: `--color-bg-inverse`, `--color-text-oninverse`
- **`elevated`** - Elevated surfaces (slightly brighter)  
 - Use for: Raised cards, popovers, elevated panels  
 - Example: `--color-bg-elevated`, `--color-bg-elevated-hover`
- **`transparent`** - Transparent/subtle backgrounds  
 - Use for: Ghost buttons, subtle hover states  
 - Example: `--color-bg-transparent`, `--color-bgtransparent`

## Prominence

- **`secondary`** - Secondary emphasis (lighter/less prominent)  
- **`tertiary`** - Tertiary emphasis (lightest/least prominent)  
- **`strong`** - Strong emphasis (darker/more prominent)

## Interaction states

- **`hover`** - Hover state  
- **`pressed`** - Active/pressed state

## Background colors

### Creating hierarchy

**color-bg**
Our default background color

**color-bg-secondary**
Our secondary background color for most containers.

**color-bg-tertiary**
Our tertiary background color for containers that need to sit within a secondary background.

### Common interaction states

**color-bg-hover**
A light grey hover fill color behind icons, and selectable elements.

**color-bg-selected**
A light blue selected fill color for selected elements.

**color-bg-disabled**
A light grey background fill color for elements that are not interactive (for example, a disabled button). Note, in these cases we tweak any text or icons to use color-text-ondisabled, or color-icon-ondisabled.

### Common Hues

Most often, our common hues will be used with the (default) background color, a -hover state, and a -secondary background color that can be used for containers that sit on top.

Note, when using text or icons on top of a tinted bg, we should typically use the -on version of a token (ex: color-text-ondanger)

**color-bg-brand**
Blue or purple fill colors for backgrounds like a blue primary button.

**color-bg-danger**
Red fill color behind destructive buttons, and error banners.

**color-bg-warning**
Yellow fill color for warning banners

**color-bg-success**
Green fill color for confirmation banners and buttons.

**color-bg-assistive**
Pink fill color for assistive UI

### Tertiary backgrounds

We also have -tertiary versions of these background colors, which are intended to be the "lightest" version of a hue. These are designed to work with our default color-text and color-icon colors.

### Special UI Elements

**color-bg-toolbar**
The dark fill color of our editor toolbar

**color-bg-toolbar-hover**
The hover state for elements in the toolbar

**color-bg-toolbar-selected**
The blue selection state for elements in the toolbar

**color-bg-menu**
The dark fill color of our menus (which are darker than our toolbar)

**color-bg-tooltip**
The dark fill color of our tooltips (which are darker than our toolbar)
