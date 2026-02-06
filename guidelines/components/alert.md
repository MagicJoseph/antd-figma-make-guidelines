# Alert

**Purpose**: Display important messages or feedback inline within the page content. Alerts are static and remain visible until dismissed.

## When to Use

- Important inline messages that shouldn't be missed
- Form validation summaries
- Page-level warnings or info
- Persistent status information

## Alert Types

| Type | Description | Visual Appearance |
|------|-------------|-------------------|
| **success** | Positive feedback | Green background |
| **error** | Error/problem | Red background |
| **warning** | Warning/caution | Yellow background |
| **info** | Information | Blue background |

## Component States

| State | Description | Visual Appearance |
|-------|-------------|-------------------|
| **Default** | Standard alert | Colored background with icon |
| **With Description** | Has description | Larger with title + description |
| **Closable** | Can be dismissed | X button visible |
| **Banner** | Full-width banner | No border, top of page |

## API Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `type` | Alert type | `'success' \| 'info' \| 'warning' \| 'error'` | `'info'` |
| `message` | Alert title | `ReactNode` | - |
| `description` | Additional content | `ReactNode` | - |
| `showIcon` | Show type icon | `boolean` | `false` |
| `icon` | Custom icon | `ReactNode` | - |
| `closable` | Show close button | `boolean` | `false` |
| `closeIcon` | Custom close icon | `ReactNode` | - |
| `closeText` | Close text instead of icon | `ReactNode` | - |
| `onClose` | Close callback | `(e) => void` | - |
| `afterClose` | After close animation | `() => void` | - |
| `banner` | Banner mode (no border) | `boolean` | `false` |
| `action` | Action area content | `ReactNode` | - |

## Design Tokens Used

### Alias Tokens
- `colorSuccessBg` - Success background
- `colorSuccessBorder` - Success border
- `colorSuccessText` - Success icon/title (with description)
- `colorErrorBg`, `colorErrorBorder`, `colorErrorText` - Error colors
- `colorWarningBg`, `colorWarningBorder`, `colorWarningText` - Warning colors
- `colorInfoBg`, `colorInfoBorder`, `colorInfoText` - Info colors
- `colorText` - Message text
- `colorTextSecondary` - Description text
- `borderRadius` - Alert border radius
- `padding` - Alert padding

## Examples

### Basic Alert Types
```tsx
import { Alert } from 'antd';

<Alert message="Success message" type="success" />
<Alert message="Info message" type="info" />
<Alert message="Warning message" type="warning" />
<Alert message="Error message" type="error" />
```

### With Description
```tsx
<Alert
  message="Success"
  description="Your account has been created successfully. You can now log in with your credentials."
  type="success"
/>
```

### With Icon
```tsx
<Alert message="Success" type="success" showIcon />
<Alert message="Info" type="info" showIcon />
<Alert message="Warning" type="warning" showIcon />
<Alert message="Error" type="error" showIcon />

// With description (different icon size)
<Alert
  message="Success"
  description="Detailed description here"
  type="success"
  showIcon
/>
```

### Closable
```tsx
const [visible, setVisible] = useState(true);

{visible && (
  <Alert
    message="Closable Alert"
    type="info"
    closable
    onClose={() => setVisible(false)}
  />
)}

// With custom close text
<Alert
  message="Alert"
  type="info"
  closable
  closeText="Close Now"
/>
```

### With Action Button
```tsx
<Alert
  message="Warning"
  description="Please update your payment method"
  type="warning"
  showIcon
  action={
    <Button size="small" type="primary">
      Update
    </Button>
  }
/>
```

### Banner Mode
```tsx
// Used at top of page, no border
<Alert
  message="Site maintenance scheduled for tomorrow"
  banner
  closable
/>

// Banner with types
<Alert message="Info banner" banner />
<Alert message="Warning banner" type="warning" banner />
```

### Custom Icon
```tsx
import { SmileOutlined } from '@ant-design/icons';

<Alert
  message="Custom icon"
  icon={<SmileOutlined />}
  showIcon
  type="info"
/>
```

### Form Validation Summary
```tsx
const errors = ['Username is required', 'Password must be at least 8 characters'];

{errors.length > 0 && (
  <Alert
    message="Please fix the following errors:"
    description={
      <ul style={{ margin: 0, paddingLeft: 20 }}>
        {errors.map((error, i) => (
          <li key={i}>{error}</li>
        ))}
      </ul>
    }
    type="error"
    showIcon
  />
)}
```

### Multiple Alerts
```tsx
<Space direction="vertical" style={{ width: '100%' }}>
  <Alert message="Success message" type="success" showIcon closable />
  <Alert message="Info message" type="info" showIcon closable />
  <Alert message="Warning message" type="warning" showIcon closable />
  <Alert message="Error message" type="error" showIcon closable />
</Space>
```

## Usage Guidelines

1. **Use appropriate type**: Match alert type to the nature of the message.

2. **Always show icon**: Use `showIcon` for better visual recognition.

3. **Use description for details**: Keep `message` short, put details in `description`.

4. **Closable when temporary**: Allow closing for dismissible messages.

5. **Banner for page-wide messages**: Use `banner` for site-wide announcements.

6. **Don't overuse**: Too many alerts reduce their impact.

7. **message vs alert**:
   - `message`: Brief, auto-dismissing feedback
   - `Alert`: Persistent, inline information
