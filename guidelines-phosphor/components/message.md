# Message

**Purpose**: Display global feedback messages at the top of the page. Messages are lightweight notifications for simple feedback.

## When to Use

- Brief feedback after an action (success, error, warning)
- Non-blocking notifications that auto-dismiss
- Simple status updates that don't require user action

## Message Types

| Type | Description | Visual Appearance |
|------|-------------|-------------------|
| **success** | Action completed | Green icon, success text |
| **error** | Action failed | Red icon, error text |
| **warning** | Caution needed | Yellow icon, warning text |
| **info** | General information | Blue icon, info text |
| **loading** | Action in progress | Spinning icon |

## API (Static Methods)

| Method | Description | Signature |
|--------|-------------|-----------|
| `message.success` | Success message | `(content, duration?, onClose?)` |
| `message.error` | Error message | `(content, duration?, onClose?)` |
| `message.warning` | Warning message | `(content, duration?, onClose?)` |
| `message.info` | Info message | `(content, duration?, onClose?)` |
| `message.loading` | Loading message | `(content, duration?, onClose?)` |
| `message.open` | Custom message | `(config)` |
| `message.destroy` | Close all messages | `(key?)` |

## Config Options

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `content` | Message content | `ReactNode` | - |
| `duration` | Auto-close delay (seconds) | `number` | `3` |
| `onClose` | Close callback | `() => void` | - |
| `key` | Unique identifier | `string \| number` | - |
| `icon` | Custom icon | `ReactNode` | - |
| `style` | Custom style | `CSSProperties` | - |
| `className` | Custom class | `string` | - |
| `onClick` | Click handler | `() => void` | - |

## Global Config

```tsx
message.config({
  top: 100,           // Distance from top
  duration: 2,        // Default duration
  maxCount: 3,        // Max messages shown
  rtl: true,          // RTL support
  prefixCls: 'my-msg' // Custom prefix
});
```

## Design Tokens Used

### Alias Tokens
- `colorSuccess` - Success icon/text
- `colorError` - Error icon/text
- `colorWarning` - Warning icon/text
- `colorInfo` - Info icon/text
- `colorBgElevated` - Message background
- `boxShadow` - Message shadow
- `borderRadius` - Message border radius

## Examples

### Basic Messages
```tsx
import { message, Button } from 'antd';

const showSuccess = () => {
  message.success('Action completed successfully');
};

const showError = () => {
  message.error('Something went wrong');
};

const showWarning = () => {
  message.warning('Please check your input');
};

const showInfo = () => {
  message.info('Here is some information');
};
```

### Custom Duration
```tsx
// 5 seconds
message.success('This will close in 5 seconds', 5);

// Won't auto-close (0 = no auto-close)
message.loading('Loading...', 0);
```

### Loading then Success
```tsx
const handleSubmit = async () => {
  const hide = message.loading('Submitting...', 0);
  try {
    await submitData();
    hide();
    message.success('Submitted successfully');
  } catch (error) {
    hide();
    message.error('Submission failed');
  }
};
```

### Update Existing Message
```tsx
const key = 'updatable';

const openMessage = () => {
  message.loading({ content: 'Loading...', key });
  setTimeout(() => {
    message.success({ content: 'Loaded!', key, duration: 2 });
  }, 1000);
};
```

### With onClose Callback
```tsx
message.success('Action complete', 2, () => {
  console.log('Message closed');
});
```

### Custom Icon
```tsx
import { SmileyIcon, CheckCircleIcon, XCircleIcon, WarningCircleIcon } from './icons';
import { theme } from 'antd';

const { token } = theme.useToken();

message.open({
  content: 'Custom icon message',
  icon: <SmileyIcon weight="fill" style={{ color: '#108ee9' }} />,
});

// With semantic colors
message.open({
  type: 'success',
  content: 'Operation successful',
  icon: <CheckCircleIcon color={token.colorSuccess} size={20} weight="fill" />,
});

message.open({
  type: 'error',
  content: 'Operation failed',
  icon: <XCircleIcon color={token.colorError} size={20} weight="fill" />,
});

message.open({
  type: 'warning',
  content: 'Please check your input',
  icon: <WarningCircleIcon color={token.colorWarning} size={20} weight="fill" />,
});
```

### Promise Interface
```tsx
message
  .loading('Action in progress...', 2.5)
  .then(() => message.success('Loading finished', 2.5))
  .then(() => message.info('Loading finished is finished', 2.5));
```

### Hooks API (Recommended)
```tsx
import { message, App } from 'antd';

// Wrap your app with App component
const AppWrapper = () => (
  <App>
    <MyApp />
  </App>
);

// In your component
const MyComponent = () => {
  const { message } = App.useApp();

  const handleClick = () => {
    message.success('Success!');
  };

  return <Button onClick={handleClick}>Show Message</Button>;
};
```

### Destroy Messages
```tsx
// Destroy all
message.destroy();

// Destroy specific message by key
message.destroy('unique-key');
```

## Usage Guidelines

1. **Brief content**: Messages should be short (1-2 sentences max).

2. **Use appropriate type**: Match message type to the action result.

3. **Default duration is fine**: 3 seconds is appropriate for most messages.

4. **Loading + result pattern**: Show loading, then success/error.

5. **Use hooks API in modern apps**: `App.useApp()` provides better context handling.

6. **Don't overuse**: Messages shouldn't appear for every action.

7. **For important errors, use Notification**: Messages are for brief feedback; Notification for details.
