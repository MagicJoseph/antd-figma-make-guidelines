# Progress

**Purpose**: Display the progress of an operation or show a percentage value.

## When to Use

- Showing completion status
- Upload/download progress
- Multi-step processes
- Loading indicators with progress

## Progress Types

| Type | Description | Visual |
|------|-------------|--------|
| **Line** | Horizontal bar | Default progress bar |
| **Circle** | Circular progress | Ring/donut chart |
| **Dashboard** | Semi-circle | Dashboard gauge |

## API Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `percent` | Progress percentage | `number` | `0` |
| `type` | Progress type | `'line' \| 'circle' \| 'dashboard'` | `'line'` |
| `status` | Progress status | `'success' \| 'exception' \| 'normal' \| 'active'` | - |
| `showInfo` | Show percentage/status | `boolean` | `true` |
| `format` | Custom format function | `(percent, successPercent) => ReactNode` | - |
| `strokeColor` | Progress bar color | `string \| { from, to, direction } \| string[]` | - |
| `trailColor` | Trail (unfilled) color | `string` | - |
| `strokeWidth` | Line width (line only) | `number` | `8` |
| `strokeLinecap` | Line end shape | `'round' \| 'butt' \| 'square'` | `'round'` |
| `size` | Size | `'small' \| 'default' \| number \| [width, height]` | `'default'` |
| `steps` | Total steps (line only) | `number` | - |
| `success` | Success segment config | `{ percent, strokeColor }` | - |

### Circle/Dashboard Specific

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `width` | Canvas width | `number` | `132` (circle), `120` (dashboard) |
| `gapDegree` | Gap degree (dashboard) | `number` | `75` |
| `gapPosition` | Gap position (dashboard) | `'top' \| 'bottom' \| 'left' \| 'right'` | `'bottom'` |

## Design Tokens Used

### Seed Tokens
- `colorPrimary` - Default progress color

### Alias Tokens
- `colorSuccess` - Success status
- `colorError` - Exception status
- `colorBgLayout` - Trail color
- `fontSize` - Info text size

## Examples

### Basic Progress
```tsx
import { Progress } from 'antd';

<Progress percent={30} />
<Progress percent={50} status="active" />
<Progress percent={70} status="exception" />
<Progress percent={100} />
```

### Small Size
```tsx
<Progress percent={30} size="small" />
```

### Custom Size
```tsx
<Progress percent={50} size={[300, 20]} />
```

### Without Info
```tsx
<Progress percent={30} showInfo={false} />
```

### Custom Format
```tsx
<Progress percent={75} format={(percent) => `${percent} Days`} />
<Progress percent={100} format={() => 'Done'} />
```

### Circle Progress
```tsx
<Progress type="circle" percent={75} />
<Progress type="circle" percent={70} status="exception" />
<Progress type="circle" percent={100} />
```

### Circle with Custom Icons (Phosphor)
```tsx
import { Progress, theme } from 'antd';
import { CheckIcon, XIcon, CheckCircleIcon } from './icons';

const { token } = theme.useToken();

// Success with check icon
<Progress
  type="circle"
  percent={100}
  status="success"
  format={() => <CheckIcon color={token.colorSuccess} size={32} weight="bold" />}
/>

// Error with X icon
<Progress
  type="circle"
  percent={70}
  status="exception"
  format={() => <XIcon color={token.colorError} size={32} weight="bold" />}
/>

// Line progress with status icon
<Progress
  percent={100}
  status="success"
  format={() => <CheckCircleIcon weight="fill" color={token.colorSuccess} />}
/>
```

### Circle Size
```tsx
<Progress type="circle" percent={30} width={80} />
```

### Dashboard
```tsx
<Progress type="dashboard" percent={75} />
<Progress type="dashboard" percent={75} gapDegree={30} />
```

### Custom Colors
```tsx
// Solid color
<Progress percent={50} strokeColor="#52c41a" />

// Gradient
<Progress
  percent={99.9}
  strokeColor={{
    '0%': '#108ee9',
    '100%': '#87d068',
  }}
/>

// Gradient with direction
<Progress
  percent={50}
  strokeColor={{
    from: '#108ee9',
    to: '#87d068',
    direction: 'to right',
  }}
/>
```

### Segmented Progress
```tsx
<Progress percent={60} success={{ percent: 30 }} />
```

### Steps Progress
```tsx
<Progress percent={50} steps={5} />
<Progress percent={30} steps={5} size="small" />
<Progress percent={100} steps={5} strokeColor="#52c41a" />
```

### Dynamic Progress
```tsx
const [percent, setPercent] = useState(0);

useEffect(() => {
  const timer = setInterval(() => {
    setPercent((prev) => {
      if (prev >= 100) {
        clearInterval(timer);
        return 100;
      }
      return prev + 10;
    });
  }, 500);
  return () => clearInterval(timer);
}, []);

<Progress percent={percent} />
```

### With Status
```tsx
const getStatus = (percent) => {
  if (percent === 100) return 'success';
  if (hasError) return 'exception';
  if (isLoading) return 'active';
  return 'normal';
};

<Progress percent={percent} status={getStatus(percent)} />
```

### Upload Progress
```tsx
{uploadProgress > 0 && uploadProgress < 100 && (
  <Progress
    percent={uploadProgress}
    status="active"
    strokeColor={{
      '0%': '#108ee9',
      '100%': '#87d068',
    }}
  />
)}
```

## Usage Guidelines

1. **Use appropriate type**: Line for inline, Circle/Dashboard for emphasis.

2. **Show status**: Use `status` prop to indicate success/failure.

3. **Custom format for context**: Show units or custom text with `format`.

4. **Animate with `active`**: Use `status="active"` for ongoing operations.

5. **Steps for discrete progress**: Use `steps` for multi-step processes.

6. **Gradients for visual interest**: Use gradient `strokeColor` for emphasis.
