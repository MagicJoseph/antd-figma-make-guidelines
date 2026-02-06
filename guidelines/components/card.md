# Card

**Purpose**: Container for displaying content and actions about a single subject. Cards group related information in a visually distinct box.

## When to Use

- Displaying grouped information about an item
- Grid layouts with multiple items
- Dashboard widgets
- Preview content with actions
- Organizing related content sections

## Component States

| State | Description | Visual Appearance |
|-------|-------------|-------------------|
| **Default** | Normal display | White background with border/shadow |
| **Hoverable** | Mouse interaction | Slight lift/shadow on hover |
| **Loading** | Content loading | Skeleton placeholder |
| **Bordered** | With border | Visible border line |
| **Borderless** | No border | Clean, flat appearance |

## API Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `title` | Card title | `ReactNode` | - |
| `extra` | Extra content in header | `ReactNode` | - |
| `variant` | Card variant (v6) | `'outlined' \| 'borderless'` | `'outlined'` |
| `hoverable` | Hover effect | `boolean` | `false` |
| `loading` | Loading skeleton | `boolean` | `false` |
| `cover` | Cover image/content | `ReactNode` | - |
| `actions` | Footer action buttons | `ReactNode[]` | - |
| `type` | Card style type | `'inner'` | - |
| `size` | Card padding | `'default' \| 'small'` | `'default'` |
| `styles` | Custom styles for parts (v6) | `{ header, body, extra, title, actions, cover }` | - |
| `classNames` | Custom classes for parts (v6) | `{ header, body, extra, title, actions, cover }` | - |

> **v6 Migration Note**: `bordered` prop is deprecated. Use `variant="borderless"` instead of `bordered={false}`. Props `headStyle` and `bodyStyle` are deprecated - use `styles.header` and `styles.body` instead.

## Card.Grid Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `hoverable` | Hover effect | `boolean` | `true` |
| `style` | Grid item style | `CSSProperties` | - |

## Card.Meta Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `avatar` | Avatar element | `ReactNode` | - |
| `title` | Title content | `ReactNode` | - |
| `description` | Description content | `ReactNode` | - |

## Design Tokens Used

### Alias Tokens
- `colorBgContainer` - Card background
- `colorBorder` - Border color (when bordered)
- `colorText` - Body text
- `colorTextHeading` - Title text
- `colorTextSecondary` - Description text
- `borderRadius` - Card corner radius (borderRadiusLG)
- `padding` - Card body padding
- `paddingLG` - Default card padding
- `paddingSM` - Small card padding
- `boxShadow` - Card shadow (when elevated)

## Examples

### Basic Card
```tsx
import { Card } from 'antd';

<Card title="Card Title" style={{ width: 300 }}>
  <p>Card content</p>
  <p>Card content</p>
</Card>
```

### Card with Extra Header Content
```tsx
<Card
  title="Card Title"
  extra={<a href="#">More</a>}
  style={{ width: 300 }}
>
  <p>Card content</p>
</Card>
```

### No Border (Borderless)
```tsx
// v6: Use variant instead of bordered
<Card title="No Border" variant="borderless" style={{ width: 300 }}>
  <p>Card without border</p>
</Card>
```

### Hoverable Card
```tsx
<Card
  hoverable
  style={{ width: 240 }}
  cover={<img alt="example" src="/image.png" />}
>
  <Card.Meta title="Card Title" description="Description text" />
</Card>
```

### Loading Card
```tsx
const [loading, setLoading] = useState(true);

<Card loading={loading} style={{ width: 300 }}>
  <Card.Meta
    avatar={<Avatar src="/avatar.png" />}
    title="Card Title"
    description="This is the description"
  />
</Card>
```

### Card with Cover Image
```tsx
<Card
  style={{ width: 300 }}
  cover={
    <img
      alt="example"
      src="https://example.com/image.jpg"
    />
  }
>
  <Card.Meta
    title="Product Name"
    description="Product description goes here"
  />
</Card>
```

### Card with Actions
```tsx
import { EditOutlined, EllipsisOutlined, SettingOutlined } from '@ant-design/icons';

<Card
  style={{ width: 300 }}
  actions={[
    <SettingOutlined key="setting" />,
    <EditOutlined key="edit" />,
    <EllipsisOutlined key="ellipsis" />,
  ]}
>
  <Card.Meta
    avatar={<Avatar src="/avatar.png" />}
    title="Card Title"
    description="Description text"
  />
</Card>
```

### Inner Card (Nested)
```tsx
<Card title="Outer Card">
  <Card type="inner" title="Inner Card" extra={<a href="#">More</a>}>
    Inner card content
  </Card>
  <Card type="inner" title="Inner Card" style={{ marginTop: 16 }}>
    Inner card content
  </Card>
</Card>
```

### Card Grid
```tsx
<Card title="Card Grid">
  <Card.Grid style={{ width: '25%', textAlign: 'center' }}>
    Content
  </Card.Grid>
  <Card.Grid style={{ width: '25%', textAlign: 'center' }}>
    Content
  </Card.Grid>
  <Card.Grid style={{ width: '25%', textAlign: 'center' }}>
    Content
  </Card.Grid>
  <Card.Grid style={{ width: '25%', textAlign: 'center' }}>
    Content
  </Card.Grid>
</Card>
```

### Card with Tabs
```tsx
const tabList = [
  { key: 'tab1', label: 'Tab 1' },
  { key: 'tab2', label: 'Tab 2' },
];

const contentList = {
  tab1: <p>Content of Tab 1</p>,
  tab2: <p>Content of Tab 2</p>,
};

const [activeTab, setActiveTab] = useState('tab1');

<Card
  title="Card with Tabs"
  tabList={tabList}
  activeTabKey={activeTab}
  onTabChange={setActiveTab}
>
  {contentList[activeTab]}
</Card>
```

### Small Size Card
```tsx
<Card size="small" title="Small Card" extra={<a href="#">More</a>}>
  <p>Compact card with less padding</p>
</Card>
```

### Card Meta (Title + Description + Avatar)
```tsx
<Card style={{ width: 300 }}>
  <Card.Meta
    avatar={<Avatar src="/user-avatar.png" />}
    title="User Name"
    description="User bio or description goes here. This can be longer text."
  />
</Card>
```

### Card List Grid
```tsx
import { Card, Row, Col } from 'antd';

const data = [
  { title: 'Card 1', content: 'Content 1' },
  { title: 'Card 2', content: 'Content 2' },
  { title: 'Card 3', content: 'Content 3' },
];

<Row gutter={[16, 16]}>
  {data.map((item, index) => (
    <Col key={index} xs={24} sm={12} md={8} lg={6}>
      <Card title={item.title} hoverable>
        {item.content}
      </Card>
    </Col>
  ))}
</Row>
```

## Usage Guidelines

1. **Use cards for grouped content**: Cards should contain related information about one subject.

2. **Keep card content scannable**: Don't overload cards with too much information.

3. **Use hoverable for interactive cards**: Enable `hoverable` when clicking the card triggers an action.

4. **Consistent card sizes in grids**: Use the same card size/height in grid layouts.

5. **Loading state for async content**: Show `loading` skeleton while fetching card data.

6. **Actions for quick operations**: Use `actions` for common operations like edit, delete, share.

7. **Cover images should be optimized**: Ensure cover images have consistent aspect ratios.
