# Button

**Purpose**: Trigger operations and actions. Buttons communicate actions users can take and allow them to interact with the system.

## When to Use

- **Primary button**: Main action in a section; use at most one primary button per area
- **Default button**: Series of actions without priority
- **Dashed button**: Adding actions (e.g., "Add item")
- **Text button**: Most secondary actions, minimal visual weight
- **Link button**: External links or navigation

## Component States

| State | Description | Visual Appearance |
|-------|-------------|-------------------|
| **Default** | Normal resting state | Standard button appearance |
| **Hover** | Mouse over | Slightly lighter/darker shade |
| **Active/Pressed** | Being clicked | Darker shade, slight scale |
| **Focus** | Keyboard focus | Focus ring outline |
| **Loading** | Action in progress | Spinner icon, disabled interaction |
| **Disabled** | Not available | Grayed out, no interaction |

## API Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `type` | Button type | `'primary' \| 'default' \| 'dashed' \| 'link' \| 'text'` | `'default'` |
| `color` | Button color | `'default' \| 'primary' \| 'danger' \| PresetColors` | - |
| `variant` | Button variant | `'outlined' \| 'dashed' \| 'solid' \| 'filled' \| 'text' \| 'link'` | - |
| `size` | Button size | `'large' \| 'middle' \| 'small'` | `'middle'` |
| `shape` | Button shape | `'default' \| 'circle' \| 'round'` | `'default'` |
| `icon` | Icon component | `ReactNode` | - |
| `iconPlacement` | Icon position | `'start' \| 'end'` | `'start'` |
| `loading` | Loading state | `boolean \| { delay: number, icon: ReactNode }` | `false` |
| `disabled` | Disabled state | `boolean` | `false` |
| `danger` | Danger/destructive action | `boolean` | `false` |
| `ghost` | Transparent background | `boolean` | `false` |
| `block` | Full width | `boolean` | `false` |
| `href` | Link URL (renders as `<a>`) | `string` | - |
| `target` | Link target | `string` | - |
| `htmlType` | Native button type | `'submit' \| 'reset' \| 'button'` | `'button'` |
| `onClick` | Click handler | `(event) => void` | - |
| `classNames` | Custom classes for semantic DOM | `{ root, icon, content } \| (info) => {...}` | - |
| `styles` | Custom styles for semantic DOM | `{ root, icon, content } \| (info) => {...}` | - |

## Semantic DOM Structure (v6)

Button has semantic DOM regions that can be styled via `classNames` and `styles`:

| Region | Description |
|--------|-------------|
| `root` | Main button container (borders, background, padding) |
| `icon` | Icon element (sizing, color) |
| `content` | Text content wrapper (typography) |

```tsx
// Example: Custom styling with classNames
<Button
  classNames={{
    root: 'my-button-root',
    icon: 'my-button-icon',
    content: 'my-button-content',
  }}
>
  Styled Button
</Button>

// Dynamic classNames based on props
<Button
  classNames={(info) => ({
    root: info.props.type === 'primary' ? 'primary-root' : 'default-root',
  })}
>
  Dynamic
</Button>
```

## Design Tokens Used

### Seed Tokens
- `colorPrimary` - Primary button background
- `colorError` - Danger button background (when `danger` prop)
- `borderRadius` - Button corner radius
- `fontSize` - Button text size

### Map Tokens
- `colorPrimaryHover` - Primary button hover state
- `colorPrimaryActive` - Primary button pressed state
- `colorErrorHover` - Danger button hover
- `colorErrorActive` - Danger button pressed

### Alias Tokens
- `colorBgContainer` - Default button background
- `colorBorder` - Default button border
- `colorText` - Default button text
- `colorTextDisabled` - Disabled button text
- `colorBgContainerDisabled` - Disabled button background

## Examples

### Basic Types
```tsx
import { Button } from 'antd';

<Button type="primary">Primary</Button>
<Button>Default</Button>
<Button type="dashed">Dashed</Button>
<Button type="text">Text</Button>
<Button type="link">Link</Button>
```

### With Icons
```tsx
import { Button } from 'antd';
import { SearchIcon, DownloadIcon } from './icons';

<Button type="primary" icon={<SearchIcon weight="bold" />}>
  Search
</Button>

<Button icon={<DownloadIcon weight="bold" />}>
  Download
</Button>

// Icon only (circle shape)
<Button type="primary" shape="circle" icon={<SearchIcon weight="bold" />} />
```

### Sizes
```tsx
<Button size="large">Large</Button>
<Button>Middle (Default)</Button>
<Button size="small">Small</Button>
```

### Loading State
```tsx
const [loading, setLoading] = useState(false);

<Button
  type="primary"
  loading={loading}
  onClick={() => {
    setLoading(true);
    // ... async action
  }}
>
  Submit
</Button>

// With delay (shows loading after 1 second)
<Button loading={{ delay: 1000 }}>
  Click me
</Button>
```

### Danger Button
```tsx
<Button danger>Danger Default</Button>
<Button type="primary" danger>Danger Primary</Button>
```

### Ghost Button (Transparent Background)
```tsx
<div style={{ background: '#1890ff', padding: 16 }}>
  <Button ghost>Ghost on colored background</Button>
</div>
```

### Block Button (Full Width)
```tsx
<Button type="primary" block>
  Full Width Button
</Button>
```

### Disabled State
```tsx
<Button disabled>Disabled</Button>
<Button type="primary" disabled>Primary Disabled</Button>
```

### Button Group
```tsx
import { Button, Space } from 'antd';

<Space>
  <Button>Cancel</Button>
  <Button type="primary">Submit</Button>
</Space>

// Or use Button.Group for connected buttons
<Button.Group>
  <Button>Left</Button>
  <Button>Middle</Button>
  <Button>Right</Button>
</Button.Group>
```

## Usage Guidelines

1. **One primary button per section**: Use primary buttons sparingly for the main action.

2. **Button text should be action-oriented**: Use verbs like "Submit", "Save", "Delete", "Create".

3. **Consistent sizing**: Use the same size for buttons in a group or row.

4. **Loading for async actions**: Always show loading state for actions that take time.

5. **Danger for destructive actions**: Use `danger` prop for delete, remove, or other irreversible actions.

6. **Accessible labels**: For icon-only buttons, add `aria-label`:
   ```tsx
   <Button
     shape="circle"
     icon={<TrashIcon weight="bold" />}
     aria-label="Delete item"
   />
   ```
