# Tabs

**Purpose**: Organize content into multiple panels accessed via tab navigation. Tabs allow users to switch between different views within the same context.

## When to Use

- Switching between related content sections
- Organizing settings or configuration panels
- Dashboard views with different data perspectives
- Multi-step processes where steps are non-linear

## Component States

| State | Description | Visual Appearance |
|-------|-------------|-------------------|
| **Default Tab** | Inactive tab | Normal text color |
| **Active Tab** | Currently selected | Primary color, underline/highlight |
| **Hover** | Mouse over tab | Slightly highlighted |
| **Disabled** | Tab not clickable | Muted color, no interaction |

## API Props (Tabs)

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `activeKey` | Active tab key (controlled) | `string` | - |
| `defaultActiveKey` | Initial active tab | `string` | First tab |
| `onChange` | Tab change handler | `(activeKey: string) => void` | - |
| `items` | Tab items configuration | `TabItemType[]` | - |
| `type` | Tab style type | `'line' \| 'card' \| 'editable-card'` | `'line'` |
| `size` | Tab size | `'large' \| 'middle' \| 'small'` | `'middle'` |
| `tabPosition` | Tab bar position | `'top' \| 'right' \| 'bottom' \| 'left'` | `'top'` |
| `centered` | Center tabs | `boolean` | `false` |
| `tabBarGutter` | Gap between tabs | `number` | - |
| `tabBarExtraContent` | Extra content in tab bar | `ReactNode \| { left, right }` | - |
| `tabBarStyle` | Tab bar inline style | `CSSProperties` | - |
| `destroyOnHidden` | Destroy inactive tab content (v6) | `boolean` | `false` |
| `animated` | Animation config | `boolean \| { inkBar, tabPane }` | `true` |
| `indicator` | Custom indicator | `{ size, align }` | - |
| `onEdit` | Add/remove handler (editable-card) | `(action, info) => void` | - |
| `hideAdd` | Hide add button (editable-card) | `boolean` | `false` |
| `addIcon` | Custom add icon | `ReactNode` | - |

## Tab Item Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `key` | Unique identifier | `string` | - |
| `label` | Tab label | `ReactNode` | - |
| `children` | Tab content | `ReactNode` | - |
| `disabled` | Disabled state | `boolean` | `false` |
| `closable` | Show close button (editable-card) | `boolean` | `true` |
| `closeIcon` | Custom close icon | `ReactNode` | - |
| `icon` | Tab icon | `ReactNode` | - |
| `forceRender` | Force render even when inactive | `boolean` | `false` |
| `destroyOnClose` | Destroy content when closed | `boolean` | `false` |

## Design Tokens Used

### Seed Tokens
- `colorPrimary` - Active tab color, indicator color
- `fontSize` - Tab label size

### Alias Tokens
- `colorText` - Inactive tab color
- `colorTextDisabled` - Disabled tab color
- `colorBorder` - Card tab border
- `colorBgContainer` - Card tab background
- `padding` - Tab content padding
- `borderRadius` - Card tab radius

## Examples

### Basic Tabs
```tsx
import { Tabs } from 'antd';

<Tabs
  defaultActiveKey="1"
  items={[
    {
      key: '1',
      label: 'Tab 1',
      children: 'Content of Tab 1',
    },
    {
      key: '2',
      label: 'Tab 2',
      children: 'Content of Tab 2',
    },
    {
      key: '3',
      label: 'Tab 3',
      children: 'Content of Tab 3',
    },
  ]}
/>
```

### Controlled Tabs
```tsx
const [activeKey, setActiveKey] = useState('1');

<Tabs
  activeKey={activeKey}
  onChange={setActiveKey}
  items={items}
/>
```

### Disabled Tab
```tsx
<Tabs
  items={[
    { key: '1', label: 'Tab 1', children: 'Content 1' },
    { key: '2', label: 'Tab 2 (Disabled)', children: 'Content 2', disabled: true },
    { key: '3', label: 'Tab 3', children: 'Content 3' },
  ]}
/>
```

### Tabs with Icons
```tsx
import { HomeOutlined, SettingOutlined, UserOutlined } from '@ant-design/icons';

<Tabs
  items={[
    {
      key: '1',
      label: 'Home',
      icon: <HomeOutlined />,
      children: 'Home content',
    },
    {
      key: '2',
      label: 'Profile',
      icon: <UserOutlined />,
      children: 'Profile content',
    },
    {
      key: '3',
      label: 'Settings',
      icon: <SettingOutlined />,
      children: 'Settings content',
    },
  ]}
/>
```

### Card Type Tabs
```tsx
<Tabs
  type="card"
  items={[
    { key: '1', label: 'Card Tab 1', children: 'Content 1' },
    { key: '2', label: 'Card Tab 2', children: 'Content 2' },
  ]}
/>
```

### Editable Card Tabs (Add/Remove)
```tsx
const [items, setItems] = useState(initialItems);
const [activeKey, setActiveKey] = useState(initialItems[0].key);
const newTabIndex = useRef(0);

const add = () => {
  const newKey = `newTab${newTabIndex.current++}`;
  setItems([...items, {
    key: newKey,
    label: 'New Tab',
    children: 'New tab content',
  }]);
  setActiveKey(newKey);
};

const remove = (targetKey) => {
  const targetIndex = items.findIndex((item) => item.key === targetKey);
  const newItems = items.filter((item) => item.key !== targetKey);
  if (newItems.length && targetKey === activeKey) {
    const newActiveKey = newItems[targetIndex === newItems.length ? targetIndex - 1 : targetIndex].key;
    setActiveKey(newActiveKey);
  }
  setItems(newItems);
};

const onEdit = (targetKey, action) => {
  if (action === 'add') {
    add();
  } else {
    remove(targetKey);
  }
};

<Tabs
  type="editable-card"
  activeKey={activeKey}
  onChange={setActiveKey}
  onEdit={onEdit}
  items={items}
/>
```

### Tab Position
```tsx
// Left position
<Tabs tabPosition="left" items={items} />

// Right position
<Tabs tabPosition="right" items={items} />

// Bottom position
<Tabs tabPosition="bottom" items={items} />
```

### Centered Tabs
```tsx
<Tabs centered items={items} />
```

### Extra Content in Tab Bar
```tsx
<Tabs
  tabBarExtraContent={<Button>Extra Action</Button>}
  items={items}
/>

// Left and right extra content
<Tabs
  tabBarExtraContent={{
    left: <span>Left content</span>,
    right: <Button>Right action</Button>,
  }}
  items={items}
/>
```

### Sizes
```tsx
<Tabs size="large" items={items} />
<Tabs size="middle" items={items} />
<Tabs size="small" items={items} />
```

### Custom Tab Label
```tsx
<Tabs
  items={[
    {
      key: '1',
      label: (
        <span>
          <Badge count={5}>
            Messages
          </Badge>
        </span>
      ),
      children: 'Messages content',
    },
    {
      key: '2',
      label: (
        <span>
          <Tag color="green">New</Tag>
          Features
        </span>
      ),
      children: 'Features content',
    },
  ]}
/>
```

### Destroy Inactive Tabs
```tsx
// Useful for forms or heavy components
<Tabs
  destroyOnHidden
  items={items}
/>
```

## Usage Guidelines

1. **Use `items` prop**: Prefer `items` array over `Tabs.TabPane` children for better performance.

2. **Keep tab labels short**: Labels should be scannable (1-2 words ideally).

3. **Use icons for visual scanning**: Add icons to help users quickly identify tab purpose.

4. **Consistent content structure**: Tab content should have similar structure/layout.

5. **Consider loading states**: Use `forceRender` or handle loading in each tab panel.

6. **Use `destroyOnHidden` carefully**: Enables for forms to reset state, but can hurt performance.

7. **Limit number of tabs**: Too many tabs become hard to navigate (consider dropdown for 7+).

8. **Position based on content**: Use vertical tabs (`tabPosition="left"`) for settings/navigation in desktop apps.
