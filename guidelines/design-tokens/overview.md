# Design Tokens Overview

Ant Design v6 uses a three-layer token system for theming. Understanding this hierarchy is essential for proper theme customization.

## Token Hierarchy

```
Seed Tokens (Base values you set)
    ↓ [Algorithms calculate derived values]
Map Tokens (Calculated from Seed Tokens)
    ↓ [Further processing]
Alias Tokens (Component-specific tokens)
```

### 1. Seed Tokens (Primary)
Fundamental design values that you define. Changing a Seed Token triggers automatic recalculation of all related Map and Alias tokens.

**Examples:**
- `colorPrimary` - Primary brand color
- `colorSuccess` - Success state color
- `colorWarning` - Warning state color
- `colorError` - Error state color
- `colorInfo` - Information state color
- `borderRadius` - Base border radius
- `fontSize` - Base font size

### 2. Map Tokens (Derived)
Automatically calculated from Seed Tokens using algorithms. These create color palettes and derived values.

**Examples:**
- `colorPrimaryBg` - Light background tint of primary color
- `colorPrimaryBgHover` - Hover state of primary background
- `colorPrimaryBorder` - Border color derived from primary
- `colorPrimaryBorderHover` - Hover state of primary border
- `colorPrimaryHover` - Hover state of primary color
- `colorPrimaryActive` - Active/pressed state of primary color
- `colorPrimaryText` - Text color for primary contexts
- `colorPrimaryTextHover` - Hover state of primary text
- `colorPrimaryTextActive` - Active state of primary text

### 3. Alias Tokens (Component-Specific)
Tokens that map to specific component styles. These reference Map Tokens or Seed Tokens.

**Examples:**
- `colorBgContainer` - Background for container elements
- `colorBgElevated` - Background for elevated elements (dropdowns, modals)
- `colorBgLayout` - Background for layout areas
- `colorBgSpotlight` - Spotlight/highlight background
- `colorBorder` - Default border color
- `colorBorderSecondary` - Secondary border color
- `colorText` - Default text color
- `colorTextSecondary` - Secondary text color
- `colorTextTertiary` - Tertiary text color
- `colorTextQuaternary` - Quaternary text color

## Applying Tokens with ConfigProvider

```tsx
import { ConfigProvider } from 'antd';

const App = () => (
  <ConfigProvider
    theme={{
      token: {
        // Seed Tokens
        colorPrimary: '#1890ff',
        colorSuccess: '#52c41a',
        colorWarning: '#faad14',
        colorError: '#ff4d4f',
        borderRadius: 6,
        fontSize: 14,

        // You can also override Map/Alias tokens directly
        colorBgContainer: '#ffffff',
        colorBgElevated: '#ffffff',
      },
    }}
  >
    <YourApp />
  </ConfigProvider>
);
```

## Accessing Tokens in Components

Use the `useToken` hook to access current theme tokens:

```tsx
import { theme } from 'antd';

const { useToken } = theme;

const MyComponent = () => {
  const { token } = useToken();

  return (
    <div
      style={{
        backgroundColor: token.colorBgContainer,
        padding: token.padding,
        borderRadius: token.borderRadius,
        color: token.colorText,
        fontSize: token.fontSize,
      }}
    >
      Content using design tokens
    </div>
  );
};
```

## Theme Algorithms

Ant Design provides built-in algorithms for generating Map Tokens:

```tsx
import { ConfigProvider, theme } from 'antd';

const { defaultAlgorithm, darkAlgorithm, compactAlgorithm } = theme;

// Default (light) theme
<ConfigProvider theme={{ algorithm: defaultAlgorithm }}>

// Dark theme
<ConfigProvider theme={{ algorithm: darkAlgorithm }}>

// Compact theme (smaller spacing)
<ConfigProvider theme={{ algorithm: compactAlgorithm }}>

// Combined algorithms
<ConfigProvider theme={{ algorithm: [darkAlgorithm, compactAlgorithm] }}>
```

## Quick Decision Tree

**Need to change brand color?**
→ Set `colorPrimary` (Seed Token)
→ All primary-related colors will be recalculated automatically

**Need to change background colors?**
→ Set `colorBgContainer`, `colorBgElevated`, or `colorBgLayout` (Alias Tokens)

**Need to change text colors?**
→ Set `colorText`, `colorTextSecondary`, etc. (Alias Tokens)

**Need to change border colors?**
→ Set `colorBorder`, `colorBorderSecondary` (Alias Tokens)

**Need to change spacing/sizing?**
→ Set `fontSize`, `borderRadius`, `padding`, `margin` (Seed Tokens)

**Need dark mode?**
→ Use `darkAlgorithm` theme algorithm
