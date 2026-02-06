# Tooltip

**Purpose**: Display informative text when users hover over, focus on, or tap an element.

## When to Use

- Explaining icons or abbreviated text
- Showing full text for truncated content
- Providing additional context without cluttering UI

## API Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `title` | Tooltip content | `ReactNode \| () => ReactNode` | - |
| `placement` | Position | `'top' \| 'left' \| 'right' \| 'bottom' \| 'topLeft' \| 'topRight' \| ...` | `'top'` |
| `arrow` | Show arrow | `boolean \| { pointAtCenter }` | `true` |
| `color` | Background color | `string` | - |
| `open` | Visibility (controlled) | `boolean` | - |
| `defaultOpen` | Initial visibility | `boolean` | `false` |
| `onOpenChange` | Visibility change handler | `(open: boolean) => void` | - |
| `trigger` | Trigger mode | `'hover' \| 'focus' \| 'click' \| 'contextMenu' \| Array` | `'hover'` |
| `mouseEnterDelay` | Delay before showing (seconds) | `number` | `0.1` |
| `mouseLeaveDelay` | Delay before hiding (seconds) | `number` | `0.1` |
| `destroyTooltipOnHide` | Destroy on hide | `boolean` | `false` |
| `overlayClassName` | Tooltip class | `string` | - |
| `overlayStyle` | Tooltip style | `CSSProperties` | - |
| `overlayInnerStyle` | Inner content style | `CSSProperties` | - |
| `getPopupContainer` | Mount container | `(triggerNode) => HTMLElement` | `() => document.body` |
| `zIndex` | z-index value | `number` | - |
| `fresh` | Always render fresh content | `boolean` | `false` |

## Design Tokens Used

### Alias Tokens
- `colorBgSpotlight` - Tooltip background (dark)
- `colorTextLightSolid` - Tooltip text (white)
- `borderRadius` - Tooltip border radius
- `fontSize` - Tooltip text size (fontSizeSM)
- `paddingXS` - Tooltip padding

## Examples

### Basic Tooltip
```tsx
import { Tooltip, Button } from 'antd';

<Tooltip title="Prompt text">
  <span>Hover me</span>
</Tooltip>
```

### Placements
```tsx
<Tooltip title="Top" placement="top">
  <Button>Top</Button>
</Tooltip>

<Tooltip title="Bottom" placement="bottom">
  <Button>Bottom</Button>
</Tooltip>

<Tooltip title="Left" placement="left">
  <Button>Left</Button>
</Tooltip>

<Tooltip title="Right" placement="right">
  <Button>Right</Button>
</Tooltip>

// Corner placements
<Tooltip title="Top Left" placement="topLeft">
  <Button>TL</Button>
</Tooltip>
```

### Colored Tooltip
```tsx
<Tooltip title="Blue tooltip" color="blue">
  <Button>Blue</Button>
</Tooltip>

<Tooltip title="Custom color" color="#f50">
  <Button>Custom</Button>
</Tooltip>

// Preset colors
const colors = ['pink', 'red', 'yellow', 'orange', 'cyan', 'green', 'blue', 'purple'];
{colors.map(color => (
  <Tooltip title={color} color={color} key={color}>
    <Button>{color}</Button>
  </Tooltip>
))}
```

### Without Arrow
```tsx
<Tooltip title="No arrow" arrow={false}>
  <Button>No Arrow</Button>
</Tooltip>

// Arrow pointing at center
<Tooltip title="Centered arrow" arrow={{ pointAtCenter: true }}>
  <Button>Centered</Button>
</Tooltip>
```

### Different Triggers
```tsx
<Tooltip title="Click to show" trigger="click">
  <Button>Click me</Button>
</Tooltip>

<Tooltip title="Focus to show" trigger="focus">
  <Input placeholder="Focus me" />
</Tooltip>

<Tooltip title="Right click" trigger="contextMenu">
  <span>Right click me</span>
</Tooltip>

// Multiple triggers
<Tooltip title="Hover or click" trigger={['hover', 'click']}>
  <Button>Hover or Click</Button>
</Tooltip>
```

### Controlled Tooltip
```tsx
const [open, setOpen] = useState(false);

<Tooltip
  title="Controlled tooltip"
  open={open}
  onOpenChange={setOpen}
>
  <Button onClick={() => setOpen(!open)}>
    Toggle Tooltip
  </Button>
</Tooltip>
```

### Tooltip on Disabled Element
```tsx
// Wrap disabled element in span
<Tooltip title="Disabled button info">
  <span>
    <Button disabled>Disabled</Button>
  </span>
</Tooltip>
```

### Custom Delay
```tsx
<Tooltip
  title="Delayed tooltip"
  mouseEnterDelay={0.5}
  mouseLeaveDelay={0.2}
>
  <Button>Delayed (0.5s)</Button>
</Tooltip>
```

### Rich Content
```tsx
<Tooltip
  title={
    <div>
      <strong>Title</strong>
      <p>Description text here</p>
    </div>
  }
>
  <Button>Rich Content</Button>
</Tooltip>
```

### Icon Button with Tooltip
```tsx
import { EditOutlined, DeleteOutlined } from '@ant-design/icons';

<Space>
  <Tooltip title="Edit">
    <Button type="text" icon={<EditOutlined />} />
  </Tooltip>
  <Tooltip title="Delete">
    <Button type="text" danger icon={<DeleteOutlined />} />
  </Tooltip>
</Space>
```

### Tooltip for Truncated Text
```tsx
<Tooltip title="Very long text that gets truncated">
  <Typography.Text ellipsis style={{ maxWidth: 100 }}>
    Very long text that gets truncated
  </Typography.Text>
</Tooltip>
```

## Usage Guidelines

1. **Keep content brief**: Tooltips are for short, helpful text.

2. **Don't put critical info in tooltips**: Users may miss hover-only content.

3. **Use for icons**: Always explain icon-only buttons.

4. **Wrap disabled elements**: Disabled elements need a wrapper for tooltip to work.

5. **Avoid on mobile**: Hover doesn't work well on touch devices.

6. **Use consistent placement**: Maintain consistent tooltip positions across your app.
