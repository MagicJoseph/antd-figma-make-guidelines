# Spacing & Sizing Design Tokens

## Spacing Scale

Ant Design uses a consistent spacing scale based on multiples of 4px.

## Padding Tokens

| Token | Default Value | Usage |
|-------|--------------|-------|
| `paddingXXS` | 4px | Minimal padding |
| `paddingXS` | 8px | Extra small padding |
| `paddingSM` | 12px | Small padding |
| `padding` | 16px | Default padding |
| `paddingMD` | 20px | Medium padding |
| `paddingLG` | 24px | Large padding |
| `paddingXL` | 32px | Extra large padding |

## Margin Tokens

| Token | Default Value | Usage |
|-------|--------------|-------|
| `marginXXS` | 4px | Minimal margin |
| `marginXS` | 8px | Extra small margin |
| `marginSM` | 12px | Small margin |
| `margin` | 16px | Default margin |
| `marginMD` | 20px | Medium margin |
| `marginLG` | 24px | Large margin |
| `marginXL` | 32px | Extra large margin |
| `marginXXL` | 48px | Extra extra large margin |

## Border Radius Tokens

| Token | Default Value | Usage |
|-------|--------------|-------|
| `borderRadiusXS` | 2px | Small elements |
| `borderRadiusSM` | 4px | Small components |
| `borderRadius` | 6px | Default radius |
| `borderRadiusLG` | 8px | Large components |
| `borderRadiusOuter` | 4px | Outer containers |

## Size Tokens (Component Heights)

| Token | Default Value | Usage |
|-------|--------------|-------|
| `controlHeightXS` | 24px | Extra small controls |
| `controlHeightSM` | 24px | Small controls |
| `controlHeight` | 32px | Default control height |
| `controlHeightLG` | 40px | Large controls |

## Line Width Tokens (Borders)

| Token | Default Value | Usage |
|-------|--------------|-------|
| `lineWidth` | 1px | Default border width |
| `lineWidthBold` | 2px | Bold/emphasis borders |
| `lineWidthFocus` | 4px | Focus ring width |

## Motion/Animation Tokens

| Token | Default Value | Usage |
|-------|--------------|-------|
| `motionDurationFast` | 0.1s | Fast transitions |
| `motionDurationMid` | 0.2s | Medium transitions |
| `motionDurationSlow` | 0.3s | Slow transitions |
| `motionEaseInOut` | cubic-bezier(0.645, 0.045, 0.355, 1) | Easing function |
| `motionEaseOut` | cubic-bezier(0.215, 0.61, 0.355, 1) | Ease out |
| `motionEaseIn` | cubic-bezier(0.55, 0.055, 0.675, 0.19) | Ease in |

## Using Spacing Tokens

```tsx
import { theme } from 'antd';

const { useToken } = theme;

const CardComponent = () => {
  const { token } = useToken();

  return (
    <div
      style={{
        padding: token.padding,
        marginBottom: token.marginLG,
        borderRadius: token.borderRadius,
        border: `${token.lineWidth}px solid ${token.colorBorder}`,
      }}
    >
      <h3
        style={{
          marginBottom: token.marginSM,
        }}
      >
        Card Title
      </h3>
      <p
        style={{
          marginBottom: token.marginXS,
        }}
      >
        Card content with proper spacing.
      </p>
    </div>
  );
};
```

## Space Component

AntD provides a Space component for consistent spacing between elements:

```tsx
import { Space, Button } from 'antd';

// Horizontal spacing (default)
<Space>
  <Button>Button 1</Button>
  <Button>Button 2</Button>
  <Button>Button 3</Button>
</Space>

// Vertical spacing
<Space direction="vertical">
  <Button>Button 1</Button>
  <Button>Button 2</Button>
</Space>

// Custom size
<Space size="small">...</Space>   // 8px
<Space size="middle">...</Space>  // 16px (default)
<Space size="large">...</Space>   // 24px
<Space size={32}>...</Space>      // Custom px value

// Wrap when overflow
<Space wrap>
  {items.map(item => <Tag key={item}>{item}</Tag>)}
</Space>

// Split with divider
<Space split={<Divider type="vertical" />}>
  <Link>Link 1</Link>
  <Link>Link 2</Link>
  <Link>Link 3</Link>
</Space>
```

## Flex Component

For more complex layouts, use the Flex component:

```tsx
import { Flex, Button } from 'antd';

// Horizontal with gap
<Flex gap="middle">
  <Button>Button 1</Button>
  <Button>Button 2</Button>
</Flex>

// Vertical
<Flex vertical gap="small">
  <Input />
  <Input />
</Flex>

// Justify and align
<Flex justify="space-between" align="center">
  <span>Left</span>
  <span>Right</span>
</Flex>

// Wrap
<Flex wrap="wrap" gap="small">
  {items.map(item => <Card key={item} />)}
</Flex>
```

## Grid System

For page-level layouts, use the Grid (Row/Col) system:

```tsx
import { Row, Col } from 'antd';

<Row gutter={[16, 16]}> {/* [horizontal, vertical] gap */}
  <Col span={12}>Half width</Col>
  <Col span={12}>Half width</Col>
</Row>

// Responsive
<Row gutter={{ xs: 8, sm: 16, md: 24 }}>
  <Col xs={24} sm={12} md={8}>Responsive</Col>
  <Col xs={24} sm={12} md={8}>Responsive</Col>
  <Col xs={24} sm={12} md={8}>Responsive</Col>
</Row>
```

## Customizing Spacing Scale

```tsx
<ConfigProvider
  theme={{
    token: {
      // Padding
      paddingXXS: 4,
      paddingXS: 8,
      paddingSM: 12,
      padding: 16,
      paddingMD: 20,
      paddingLG: 24,
      paddingXL: 32,

      // Margin
      marginXXS: 4,
      marginXS: 8,
      marginSM: 12,
      margin: 16,
      marginMD: 20,
      marginLG: 24,
      marginXL: 32,

      // Border radius
      borderRadius: 6,
      borderRadiusSM: 4,
      borderRadiusLG: 8,

      // Control sizes
      controlHeight: 32,
      controlHeightSM: 24,
      controlHeightLG: 40,
    },
  }}
>
  <App />
</ConfigProvider>
```

## Spacing Guidelines

1. **Use consistent increments**: Stick to the 4px grid (4, 8, 12, 16, 20, 24, 32, 48).

2. **Match spacing to content density**:
   - Dense UIs: Use `paddingSM`, `marginSM`
   - Comfortable UIs: Use default `padding`, `margin`
   - Spacious UIs: Use `paddingLG`, `marginLG`

3. **Create visual hierarchy**: Use larger spacing to separate major sections, smaller spacing for related items.

4. **Prefer Space/Flex components**: Use these over manual margin/padding when spacing multiple elements.
