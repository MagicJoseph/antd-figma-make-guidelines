# Menu

**Purpose**: Navigation menu for websites and applications. Menus provide hierarchical navigation with support for vertical and horizontal layouts.

## When to Use

- Site-wide navigation (header, sidebar)
- Nested navigation structures
- Context menus
- Dropdown navigation

## Component States

| State | Description | Visual Appearance |
|-------|-------------|-------------------|
| **Default** | Normal menu item | Standard text |
| **Hover** | Mouse over | Background highlight |
| **Selected** | Currently active | Primary color, background tint |
| **Disabled** | Not clickable | Muted color |
| **Open** | Submenu expanded | Arrow rotated, children visible |

## API Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `items` | Menu items configuration | `ItemType[]` | - |
| `mode` | Menu type | `'vertical' \| 'horizontal' \| 'inline'` | `'vertical'` |
| `theme` | Color theme | `'light' \| 'dark'` | `'light'` |
| `selectedKeys` | Selected item keys | `string[]` | - |
| `defaultSelectedKeys` | Initial selected keys | `string[]` | - |
| `openKeys` | Open submenu keys | `string[]` | - |
| `defaultOpenKeys` | Initial open submenus | `string[]` | - |
| `onSelect` | Selection handler | `({ key, keyPath, selectedKeys, domEvent }) => void` | - |
| `onClick` | Click handler | `({ key, keyPath, domEvent }) => void` | - |
| `onOpenChange` | Submenu open/close handler | `(openKeys: string[]) => void` | - |
| `inlineCollapsed` | Collapse inline menu | `boolean` | - |
| `inlineIndent` | Inline submenu indent | `number` | `24` |
| `triggerSubMenuAction` | Submenu trigger | `'hover' \| 'click'` | `'hover'` |
| `multiple` | Allow multiple selection | `boolean` | `false` |
| `selectable` | Allow selection | `boolean` | `true` |
| `expandIcon` | Custom expand icon | `ReactNode \| (props) => ReactNode` | - |

## Item Types

```tsx
type ItemType = {
  key: string;
  label: ReactNode;
  icon?: ReactNode;
  disabled?: boolean;
  danger?: boolean;
  children?: ItemType[]; // For submenus
  type?: 'group' | 'divider';
  // For type: 'group'
  // children contains group items
  // For type: 'divider'
  // Renders a divider line
};
```

## Design Tokens Used

### Seed Tokens
- `colorPrimary` - Selected item color
- `fontSize` - Menu item text size

### Alias Tokens
- `colorBgContainer` - Menu background (light)
- `colorBgElevated` - Popup menu background
- `colorText` - Item text color
- `colorTextDisabled` - Disabled item color
- `colorPrimaryBg` - Selected item background
- `padding` - Item padding
- `borderRadius` - Item hover radius

## Examples

### Basic Horizontal Menu
```tsx
import { Menu } from 'antd';
import { HouseIcon, SquaresFourIcon, GearIcon } from './icons';

const items = [
  { key: 'home', label: 'Home', icon: <HouseIcon weight="regular" /> },
  { key: 'app', label: 'Application', icon: <SquaresFourIcon weight="regular" /> },
  { key: 'settings', label: 'Settings', icon: <GearIcon weight="regular" /> },
];

<Menu mode="horizontal" items={items} defaultSelectedKeys={['home']} />
```

### Vertical Menu with Submenus
```tsx
import { EnvelopeIcon, SquaresFourIcon } from './icons';

const items = [
  {
    key: 'sub1',
    label: 'Navigation One',
    icon: <EnvelopeIcon weight="regular" />,
    children: [
      { key: '1', label: 'Option 1' },
      { key: '2', label: 'Option 2' },
    ],
  },
  {
    key: 'sub2',
    label: 'Navigation Two',
    icon: <SquaresFourIcon weight="regular" />,
    children: [
      { key: '3', label: 'Option 3' },
      { key: '4', label: 'Option 4' },
    ],
  },
];

<Menu
  mode="inline"
  defaultOpenKeys={['sub1']}
  defaultSelectedKeys={['1']}
  items={items}
/>
```

### Inline Collapsible Menu (Sidebar)
```tsx
const [collapsed, setCollapsed] = useState(false);

<Menu
  mode="inline"
  inlineCollapsed={collapsed}
  items={items}
/>
```

### Dark Theme
```tsx
<Menu
  theme="dark"
  mode="inline"
  items={items}
/>
```

### Menu Groups and Dividers
```tsx
const items = [
  {
    type: 'group',
    label: 'Group 1',
    children: [
      { key: '1', label: 'Option 1' },
      { key: '2', label: 'Option 2' },
    ],
  },
  { type: 'divider' },
  {
    type: 'group',
    label: 'Group 2',
    children: [
      { key: '3', label: 'Option 3' },
      { key: '4', label: 'Option 4' },
    ],
  },
];

<Menu mode="vertical" items={items} />
```

### Danger Item
```tsx
const items = [
  { key: 'edit', label: 'Edit' },
  { key: 'delete', label: 'Delete', danger: true },
];
```

### Controlled Menu
```tsx
const [selectedKeys, setSelectedKeys] = useState(['home']);
const [openKeys, setOpenKeys] = useState(['sub1']);

<Menu
  mode="inline"
  selectedKeys={selectedKeys}
  openKeys={openKeys}
  onSelect={({ selectedKeys }) => setSelectedKeys(selectedKeys)}
  onOpenChange={setOpenKeys}
  items={items}
/>
```

## Usage Guidelines

1. **Use `items` prop**: Prefer `items` array over `Menu.Item` children.

2. **Choose appropriate mode**:
   - `horizontal`: Top navigation bar
   - `vertical`: Simple side navigation
   - `inline`: Expandable side navigation

3. **Limit nesting depth**: Keep submenus to 2-3 levels maximum.

4. **Use icons for scannability**: Add icons to top-level items.

5. **Match theme to layout**: Use dark theme for dark sidebars.

6. **Handle collapsed state**: Save user preference for collapsed state.
