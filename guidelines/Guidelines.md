This project uses Ant Design (AntD) v6, a React UI component library. Files in the guidelines directory show how to use AntD components and design tokens.

**Requirements**: React 18 or higher is required. AntD v6 does not support React 17 or earlier.

Always read:
- All files with a name that starts with `overview-`
- All files in the `design-tokens` folder

Read the files in the `guidelines/components` directory when you want to use the component with that name. For example, if you want to use Button, read `guidelines/components/button.md`.

## Component Usage Guidelines - READ THIS FIRST

IMPORTANT: Always prefer to use components from Ant Design if they exist. For example, prefer to use a Button component from `antd`, rather than native HTML button elements.

IMPORTANT: Follow these steps IN ORDER before writing any code:

### Step 1: Read Overview Files (REQUIRED)
Read ALL files with a name that starts with "overview-" in the guidelines directory:
- `overview-components.md`
- `overview-icons.md`

### Step 2: Read Design Tokens (REQUIRED)
Read ALL files in the `design-tokens/` folder. Do NOT skip this step. AntD v6 uses a three-layer token system (Seed, Map, Alias) for theming.

### Step 3: Plan What Components You Need (REQUIRED)
Identify which AntD components are needed for your task.

### Step 4: Read Component Guidelines BEFORE Using Components (REQUIRED)
BEFORE using ANY component, you MUST read its guidelines file first:
- Using Button? → Read `guidelines/components/button.md` FIRST
- Using Input? → Read `guidelines/components/input.md` FIRST
- Using Select? → Read `guidelines/components/select.md` FIRST
- Using Table? → Read `guidelines/components/table.md` FIRST
- Using Modal? → Read `guidelines/components/modal.md` FIRST
- Using Form? → Read `guidelines/components/form.md` FIRST

DO NOT write code using a component until you have read its specific guidelines.

### Step 5: Apply Design Tokens Correctly (REQUIRED)
When customizing styles, use the ConfigProvider with theme tokens instead of inline CSS. Reference the design-tokens documentation for available tokens.

## Key Rules

1. **Import from 'antd'**: All components are imported from the `antd` package.
2. **Use ConfigProvider for theming**: Wrap your app with ConfigProvider to customize the theme.
3. **Use Semantic DOM styling (v6)**: All components support `classNames` and `styles` props for fine-grained customization of internal DOM elements (e.g., `root`, `header`, `body`, `icon`, `content`). These can be objects or functions.
4. **Prefer controlled components**: Use `value` and `onChange` for form controls.
5. **Use Form for data collection**: Let Form handle form state, not individual component state.
6. **Use `variant` instead of `bordered`**: The `bordered` prop is deprecated in v6. Use `variant="borderless"` instead.
7. **Use `destroyOnHidden` instead of `destroyOnClose`**: The `destroyOnClose` prop is deprecated in v6 for Modal, Drawer, Tabs.
