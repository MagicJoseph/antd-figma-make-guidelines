This project uses Ant Design (AntD) v6, a React UI component library, with **Phosphor Icons** replacing the default AntD icons. Files in the guidelines directory show how to use AntD components and design tokens.

**Requirements**: React 18 or higher is required. AntD v6 does not support React 17 or earlier.

Always read:
- All files with a name that starts with `overview-`
- All files in the `design-tokens` folder

Read the files in the `guidelines/components` directory when you want to use the component with that name. For example, if you want to use Button, read `guidelines/components/button.md`.

## Icon System - Phosphor Icons

This project uses **Phosphor Icons** (`@phosphor-icons/react`) instead of the default `@ant-design/icons`. Key differences:

1. **Weights instead of styles**: Phosphor uses `weight` prop (`regular`, `bold`, `fill`, `thin`, `light`, `duotone`) instead of AntD's naming convention (`Outlined`, `Filled`, `TwoTone`).

2. **Wrapper required**: Phosphor icons must be wrapped using `createPhosphorIcon()` utility to work with AntD components.

3. **Color with design tokens**: Use `theme.useToken()` to get semantic colors (`token.colorSuccess`, `token.colorError`, `token.colorWarning`).

**IMPORTANT**: Before using any icons, read `overview-icons.md` for the full integration pattern and icon mapping table.

## Component Usage Guidelines - READ THIS FIRST

IMPORTANT: Always prefer to use components from Ant Design if they exist. For example, prefer to use a Button component from `antd`, rather than native HTML button elements.

IMPORTANT: Follow these steps IN ORDER before writing any code:

### Step 1: Read Overview Files (REQUIRED)
Read ALL files with a name that starts with "overview-" in the guidelines directory:
- `overview-components.md`
- `overview-icons.md` - **Contains Phosphor Icons integration guide**

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
2. **Use Phosphor Icons**: Import icons from your `icons.ts` file, NOT from `@ant-design/icons`. See `overview-icons.md` for the full list.
3. **Use ConfigProvider for theming**: Wrap your app with ConfigProvider to customize the theme.
4. **Use Semantic DOM styling (v6)**: All components support `classNames` and `styles` props for fine-grained customization of internal DOM elements (e.g., `root`, `header`, `body`, `icon`, `content`). These can be objects or functions.
5. **Prefer controlled components**: Use `value` and `onChange` for form controls.
6. **Use Form for data collection**: Let Form handle form state, not individual component state.
7. **Use `variant` instead of `bordered`**: The `bordered` prop is deprecated in v6. Use `variant="borderless"` instead.
8. **Use `destroyOnHidden` instead of `destroyOnClose`**: The `destroyOnClose` prop is deprecated in v6 for Modal, Drawer, Tabs.

## Quick Icon Reference

| Context | Phosphor Icon | Weight | Example |
|---------|---------------|--------|---------|
| Button action | `SearchIcon`, `PlusIcon` | `bold` | `<Button icon={<SearchIcon weight="bold" />}>` |
| Menu item | `HouseIcon`, `GearIcon` | `regular` | `icon: <HouseIcon weight="regular" />` |
| Success status | `CheckCircleIcon` | `fill` | `<CheckCircleIcon color={token.colorSuccess} weight="fill" />` |
| Error status | `XCircleIcon` | `fill` | `<XCircleIcon color={token.colorError} weight="fill" />` |
| Warning status | `WarningCircleIcon` | `fill` | `<WarningCircleIcon color={token.colorWarning} weight="fill" />` |
| Input prefix | `UserIcon`, `LockIcon` | `regular` | `<Input prefix={<UserIcon weight="regular" />} />` |
| Tag close | `XIcon` | `bold` | `closeIcon={<XIcon size={12} weight="bold" />}` |
| Select dropdown | `CaretDownIcon` | `bold` | `suffixIcon={<CaretDownIcon weight="bold" />}` |
