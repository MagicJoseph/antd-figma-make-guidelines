# Spin

**Purpose**: Loading indicator for in-progress operations. Spin shows that content is being loaded or an action is processing.

## When to Use

- Page or section loading
- Data fetching
- Button action processing
- Async operations

## API Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `spinning` | Loading state | `boolean` | `true` |
| `size` | Spinner size | `'small' \| 'default' \| 'large'` | `'default'` |
| `tip` | Loading text | `ReactNode` | - |
| `delay` | Delay before showing (ms) | `number` | - |
| `indicator` | Custom spinner | `ReactNode` | - |
| `fullscreen` | Full-screen mode | `boolean` | `false` |
| `percent` | Progress percentage | `number \| 'auto'` | - |
| `wrapperClassName` | Wrapper class | `string` | - |

## Design Tokens Used

### Seed Tokens
- `colorPrimary` - Spinner color

### Alias Tokens
- `fontSize` - Tip text size
- `colorTextDescription` - Tip text color

## Examples

### Basic Spin
```tsx
import { Spin } from 'antd';

<Spin />
```

### Sizes
```tsx
<Spin size="small" />
<Spin />
<Spin size="large" />
```

### With Tip
```tsx
<Spin tip="Loading...">
  <div style={{ padding: 50, background: '#f5f5f5' }}>
    Content
  </div>
</Spin>
```

### Controlled Spinning
```tsx
const [loading, setLoading] = useState(false);

<Spin spinning={loading}>
  <div>Content that can be loading</div>
</Spin>
```

### Delay (Avoid Flash)
```tsx
// Only show spinner if loading takes > 500ms
<Spin spinning={loading} delay={500}>
  <Content />
</Spin>
```

### Custom Indicator
```tsx
import { SpinnerGap } from '@phosphor-icons/react';
import { createPhosphorIcon } from './createPhosphorIcon';

const SpinnerIcon = createPhosphorIcon(SpinnerGap);

// Option 1: Using wrapped Phosphor icon with CSS animation
<Spin indicator={<SpinnerIcon weight="bold" className="animate-spin" style={{ fontSize: 24 }} />} />

// Option 2: Using raw Phosphor icon (simpler)
<Spin indicator={
  <SpinnerGap
    size={24}
    weight="bold"
    style={{ animation: 'spin 1s linear infinite' }}
  />
} />
```

### Nested Content
```tsx
<Spin spinning={loading} tip="Loading data...">
  <Alert
    message="Alert message title"
    description="Further details about the context of this alert."
    type="info"
  />
</Spin>
```

### Full-screen
```tsx
<Spin fullscreen spinning={loading} />
```

### With Progress
```tsx
<Spin percent={75} />
<Spin percent="auto" /> // Auto-incrementing
```

### In Card
```tsx
<Card title="Data">
  <Spin spinning={loading}>
    {data ? (
      <List dataSource={data} />
    ) : null}
  </Spin>
</Card>
```

### Button Loading
```tsx
// For buttons, use Button's loading prop instead
<Button type="primary" loading={loading}>
  Submit
</Button>

// But Spin can wrap any content
<Spin spinning={loading} size="small">
  <a href="#">Link with loading</a>
</Spin>
```

### Container Loading
```tsx
const [loading, setLoading] = useState(true);

useEffect(() => {
  fetchData().then(() => setLoading(false));
}, []);

<div style={{ position: 'relative', minHeight: 200 }}>
  {loading && (
    <div style={{
      position: 'absolute',
      top: 0,
      left: 0,
      right: 0,
      bottom: 0,
      display: 'flex',
      alignItems: 'center',
      justifyContent: 'center',
      background: 'rgba(255, 255, 255, 0.8)',
      zIndex: 1
    }}>
      <Spin />
    </div>
  )}
  <Content data={data} />
</div>
```

### Global Spin (Static Method)
```tsx
// Show global loading
Spin.setDefaultIndicator(<LoadingOutlined style={{ fontSize: 24 }} spin />);
```

### Table Loading
```tsx
<Table
  loading={loading}
  columns={columns}
  dataSource={data}
/>
// Table has built-in Spin support
```

## Usage Guidelines

1. **Use `delay` to prevent flash**: Set 200-500ms delay for quick operations.

2. **Show tip for longer waits**: Add descriptive text for operations > 1-2 seconds.

3. **Use Button's loading prop**: For buttons, use native `loading` prop.

4. **Cover content being loaded**: Wrap content that will change with Spin.

5. **Full-screen for page loads**: Use `fullscreen` for page-level loading.

6. **Custom indicator for branding**: Replace default with branded spinner.

7. **Avoid multiple spinners**: Don't show multiple spinners simultaneously.
