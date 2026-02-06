# Badge

**Purpose**: Display a status indicator or count. Badges attach to other elements to show status, notifications, or counts.

## When to Use

- Notification counts
- Status indicators
- New/unread markers
- Item counts

## Badge Variants

| Variant | Description | Visual Appearance |
|---------|-------------|-------------------|
| **Count** | Numeric count | Red circle with number |
| **Dot** | Simple indicator | Small colored dot |
| **Status** | Status with text | Dot + text label |
| **Ribbon** | Corner ribbon | Angled banner |

## API Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `count` | Number to display | `ReactNode` | - |
| `dot` | Show dot instead of count | `boolean` | `false` |
| `showZero` | Show when count is 0 | `boolean` | `false` |
| `overflowCount` | Max count before "+" | `number` | `99` |
| `offset` | Position offset `[x, y]` | `[number, number]` | - |
| `size` | Badge size | `'default' \| 'small'` | `'default'` |
| `status` | Status type | `'success' \| 'processing' \| 'default' \| 'error' \| 'warning'` | - |
| `color` | Custom color | `PresetColors \| string` | - |
| `text` | Status text | `ReactNode` | - |
| `title` | Hover title | `string` | - |

## Badge.Ribbon Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `text` | Ribbon text | `ReactNode` | - |
| `color` | Ribbon color | `PresetColors \| string` | - |
| `placement` | Ribbon position | `'start' \| 'end'` | `'end'` |

## Preset Colors

```tsx
'pink' | 'red' | 'yellow' | 'orange' | 'cyan' | 'green' |
'blue' | 'purple' | 'geekblue' | 'magenta' | 'volcano' |
'gold' | 'lime'
```

## Design Tokens Used

### Seed Tokens
- `colorError` - Default badge color (red)
- `fontSize` - Badge count text (fontSizeSM)

### Alias Tokens
- `colorSuccess` - Success status
- `colorWarning` - Warning status
- `colorText` - Status text
- `borderRadius` - Badge border radius

## Examples

### Basic Badge
```tsx
import { Badge, Avatar } from 'antd';

<Badge count={5}>
  <Avatar shape="square" size="large" />
</Badge>

<Badge count={0} showZero>
  <Avatar shape="square" size="large" />
</Badge>
```

### Overflow Count
```tsx
<Badge count={99}>
  <Avatar shape="square" size="large" />
</Badge>

<Badge count={100}>
  <Avatar shape="square" size="large" />
</Badge>

<Badge count={1000} overflowCount={999}>
  <Avatar shape="square" size="large" />
</Badge>
```

### Dot Badge
```tsx
<Badge dot>
  <NotificationOutlined style={{ fontSize: 20 }} />
</Badge>

<Badge dot>
  <a href="#">Link with dot</a>
</Badge>
```

### Status Badges
```tsx
<Badge status="success" />
<Badge status="error" />
<Badge status="default" />
<Badge status="processing" />
<Badge status="warning" />

// With text
<Badge status="success" text="Success" />
<Badge status="error" text="Error" />
<Badge status="default" text="Default" />
<Badge status="processing" text="Processing" />
<Badge status="warning" text="Warning" />
```

### Colored Badges
```tsx
// Preset colors
<Badge color="blue" />
<Badge color="green" />
<Badge color="red" />
<Badge color="yellow" />
<Badge color="pink" />
<Badge color="cyan" />

// Custom color
<Badge color="#f50" text="Custom" />
```

### Small Size
```tsx
<Badge count={5} size="small">
  <Avatar shape="square" size="large" />
</Badge>
```

### Badge with Offset
```tsx
<Badge count={5} offset={[10, 10]}>
  <Avatar shape="square" size={40} />
</Badge>
```

### Ribbon Badge
```tsx
<Badge.Ribbon text="Bestseller">
  <Card title="Product Card" size="small">
    Product content
  </Card>
</Badge.Ribbon>

// Placement
<Badge.Ribbon text="New" placement="start">
  <Card title="Card" size="small">Content</Card>
</Badge.Ribbon>

// Colored ribbon
<Badge.Ribbon text="Sale" color="red">
  <Card title="Card" size="small">Content</Card>
</Badge.Ribbon>
```

### Dynamic Badge
```tsx
const [count, setCount] = useState(5);
const [show, setShow] = useState(true);

<Badge count={show ? count : 0}>
  <Avatar shape="square" size="large" />
</Badge>

<Button.Group>
  <Button onClick={() => setCount(c => c - 1)}>
    <MinusOutlined />
  </Button>
  <Button onClick={() => setCount(c => c + 1)}>
    <PlusOutlined />
  </Button>
</Button.Group>

<Switch checked={show} onChange={setShow} />
```

### Badge in Menu/Tab
```tsx
// In menu items
const menuItems = [
  {
    key: 'mail',
    icon: <Badge count={5} size="small"><MailOutlined /></Badge>,
    label: 'Mail',
  },
];

// In tabs
const tabItems = [
  {
    key: '1',
    label: (
      <span>
        Messages
        <Badge count={8} style={{ marginLeft: 8 }} />
      </span>
    ),
  },
];
```

### Standalone Badge (No Child)
```tsx
// Just the badge number
<Badge count={25} />
<Badge count={4} style={{ backgroundColor: '#52c41a' }} />
<Badge count={109} style={{ backgroundColor: '#faad14' }} />
```

## Usage Guidelines

1. **Use for counts and status**: Badges show numeric counts or status indicators.

2. **Position matters**: Default position is top-right; adjust with `offset` if needed.

3. **Use `overflowCount` for large numbers**: Show "99+" instead of exact large counts.

4. **Dot for simple indicators**: Use `dot` when count doesn't matter, just presence.

5. **Status badges for lists**: Use `status` + `text` in lists and tables.

6. **Ribbon for cards**: Use `Badge.Ribbon` for promotional labels on cards.
