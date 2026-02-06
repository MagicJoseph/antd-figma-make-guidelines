# Color Design Tokens

## Naming Pattern

AntD uses semantic color tokens following this pattern:
`color{Category}{Role}{State}`

- **Category**: What the color is for (Bg, Text, Border, etc.)
- **Role**: Semantic meaning (Primary, Success, Error, etc.)
- **State**: Interaction state (Hover, Active, Disabled)

## Color Categories

### Background Colors (`colorBg*`)

| Token | Description | Usage |
|-------|-------------|-------|
| `colorBgContainer` | Container background | Cards, panels, main content areas |
| `colorBgElevated` | Elevated surface background | Dropdowns, popovers, modals |
| `colorBgLayout` | Layout background | Page background, sidebars |
| `colorBgSpotlight` | Spotlight/highlight background | Focused or highlighted areas |
| `colorBgMask` | Mask/overlay background | Modal overlays |

### Text Colors (`colorText*`)

| Token | Description | Usage |
|-------|-------------|-------|
| `colorText` | Primary text color | Main content text |
| `colorTextSecondary` | Secondary text color | Descriptions, labels |
| `colorTextTertiary` | Tertiary text color | Placeholder text, hints |
| `colorTextQuaternary` | Quaternary text color | Disabled text, very subtle |
| `colorTextHeading` | Heading text color | Titles, headers |
| `colorTextLabel` | Label text color | Form labels |
| `colorTextDescription` | Description text color | Help text |
| `colorTextPlaceholder` | Placeholder text color | Input placeholders |
| `colorTextDisabled` | Disabled text color | Disabled states |

### Border Colors (`colorBorder*`)

| Token | Description | Usage |
|-------|-------------|-------|
| `colorBorder` | Default border color | General borders |
| `colorBorderSecondary` | Secondary border color | Subtle borders, dividers |

### Primary Color Palette (`colorPrimary*`)

These are Map Tokens derived from the `colorPrimary` Seed Token:

| Token | Description | Usage |
|-------|-------------|-------|
| `colorPrimary` | Primary brand color | Primary buttons, links |
| `colorPrimaryBg` | Light primary background | Subtle primary backgrounds |
| `colorPrimaryBgHover` | Primary background hover | Hover state |
| `colorPrimaryBorder` | Primary border color | Primary element borders |
| `colorPrimaryBorderHover` | Primary border hover | Border hover state |
| `colorPrimaryHover` | Primary color hover | Button hover state |
| `colorPrimaryActive` | Primary color active | Button pressed state |
| `colorPrimaryText` | Primary text color | Links, emphasis |
| `colorPrimaryTextHover` | Primary text hover | Link hover |
| `colorPrimaryTextActive` | Primary text active | Link active/pressed |

### Status Colors

Each status color (Success, Warning, Error, Info) follows the same pattern as Primary:

#### Success (`colorSuccess*`)
```
colorSuccess          - #52c41a (default green)
colorSuccessBg        - Light green background
colorSuccessBgHover   - Hover state
colorSuccessBorder    - Green border
colorSuccessBorderHover
colorSuccessHover
colorSuccessActive
colorSuccessText
colorSuccessTextHover
colorSuccessTextActive
```

#### Warning (`colorWarning*`)
```
colorWarning          - #faad14 (default yellow/orange)
colorWarningBg
colorWarningBgHover
colorWarningBorder
colorWarningBorderHover
colorWarningHover
colorWarningActive
colorWarningText
colorWarningTextHover
colorWarningTextActive
```

#### Error (`colorError*`)
```
colorError            - #ff4d4f (default red)
colorErrorBg
colorErrorBgHover
colorErrorBorder
colorErrorBorderHover
colorErrorHover
colorErrorActive
colorErrorText
colorErrorTextHover
colorErrorTextActive
```

#### Info (`colorInfo*`)
```
colorInfo             - #1890ff (default blue)
colorInfoBg
colorInfoBgHover
colorInfoBorder
colorInfoBorderHover
colorInfoHover
colorInfoActive
colorInfoText
colorInfoTextHover
colorInfoTextActive
```

## Quick Decision Tree

**Need a background color?**
→ Start with `colorBg*`
→ Use `colorBgContainer` for content areas
→ Use `colorBgElevated` for overlays/dropdowns
→ Use `colorBgLayout` for page-level backgrounds

**Need text on that background?**
→ Default background → use `colorText`
→ Need hierarchy → use `colorTextSecondary` or `colorTextTertiary`
→ Disabled state → use `colorTextDisabled`

**Need a colored/semantic background?**
→ Use `color{Status}Bg` (e.g., `colorSuccessBg`)
→ Text on solid semantic bg → use `#fff` (white)
→ Text on light semantic bg → use `color{Status}Text`

**Need a border?**
→ Default → use `colorBorder`
→ Subtle → use `colorBorderSecondary`
→ Semantic → use `color{Status}Border`

## Usage Example

```tsx
import { theme } from 'antd';

const { useToken } = theme;

const StatusBanner = ({ status, message }) => {
  const { token } = useToken();

  const getColors = () => {
    switch (status) {
      case 'success':
        return {
          bg: token.colorSuccessBg,
          border: token.colorSuccessBorder,
          text: token.colorSuccessText,
        };
      case 'error':
        return {
          bg: token.colorErrorBg,
          border: token.colorErrorBorder,
          text: token.colorErrorText,
        };
      case 'warning':
        return {
          bg: token.colorWarningBg,
          border: token.colorWarningBorder,
          text: token.colorWarningText,
        };
      default:
        return {
          bg: token.colorInfoBg,
          border: token.colorInfoBorder,
          text: token.colorInfoText,
        };
    }
  };

  const colors = getColors();

  return (
    <div
      style={{
        backgroundColor: colors.bg,
        border: `1px solid ${colors.border}`,
        color: colors.text,
        padding: token.padding,
        borderRadius: token.borderRadius,
      }}
    >
      {message}
    </div>
  );
};
```

## Preset Colors

AntD includes preset color palettes that can be used directly:

```tsx
// Available preset colors
const presetColors = [
  'blue', 'purple', 'cyan', 'green', 'magenta',
  'pink', 'red', 'orange', 'yellow', 'volcano',
  'geekblue', 'lime', 'gold'
];

// Usage with components that support color prop
<Tag color="blue">Blue Tag</Tag>
<Badge color="green" />
<Button color="danger">Danger</Button>
```
