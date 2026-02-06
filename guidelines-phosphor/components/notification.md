# Notification

**Purpose**: Display system notifications in a corner of the screen. Notifications are for more detailed feedback that requires user attention.

## When to Use

- Detailed feedback after system events
- Messages that need more space or context
- Notifications that may require user action
- Multi-line content with titles

## Notification Types

| Type | Description | Visual Appearance |
|------|-------------|-------------------|
| **success** | Positive result | Green icon |
| **error** | Error/failure | Red icon |
| **warning** | Warning/caution | Yellow icon |
| **info** | Information | Blue icon |
| **open** | Custom/no icon | No default icon |

## API (Static Methods)

| Method | Description |
|--------|-------------|
| `notification.success(config)` | Success notification |
| `notification.error(config)` | Error notification |
| `notification.warning(config)` | Warning notification |
| `notification.info(config)` | Info notification |
| `notification.open(config)` | Custom notification |
| `notification.destroy(key?)` | Close notifications |

## Config Options

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `message` | Notification title | `ReactNode` | - |
| `description` | Notification content | `ReactNode` | - |
| `duration` | Auto-close delay (seconds) | `number \| null` | `4.5` |
| `placement` | Position on screen | `'topLeft' \| 'topRight' \| 'bottomLeft' \| 'bottomRight'` | `'topRight'` |
| `key` | Unique identifier | `string` | - |
| `onClose` | Close callback | `() => void` | - |
| `onClick` | Click handler | `() => void` | - |
| `icon` | Custom icon | `ReactNode` | - |
| `btn` | Custom buttons | `ReactNode` | - |
| `closeIcon` | Custom close icon | `ReactNode` | - |
| `closable` | Show close button | `boolean` | `true` |
| `style` | Custom style | `CSSProperties` | - |
| `className` | Custom class | `string` | - |
| `role` | Accessibility role | `'alert' \| 'status'` | `'alert'` |
| `showProgress` | Show auto-close progress | `boolean` | `false` |
| `pauseOnHover` | Pause timer on hover | `boolean` | `true` |

## Design Tokens Used

### Alias Tokens
- `colorSuccess` - Success notification
- `colorError` - Error notification
- `colorWarning` - Warning notification
- `colorInfo` - Info notification
- `colorBgElevated` - Notification background
- `colorText` - Title text
- `colorTextSecondary` - Description text
- `boxShadowSecondary` - Notification shadow
- `borderRadiusLG` - Border radius

## Examples

### Basic Notifications
```tsx
import { notification, Button } from 'antd';

const showSuccess = () => {
  notification.success({
    message: 'Success',
    description: 'Your changes have been saved successfully.',
  });
};

const showError = () => {
  notification.error({
    message: 'Error',
    description: 'There was an error processing your request. Please try again.',
  });
};

const showWarning = () => {
  notification.warning({
    message: 'Warning',
    description: 'Your session will expire in 5 minutes.',
  });
};

const showInfo = () => {
  notification.info({
    message: 'Information',
    description: 'A new version is available. Refresh to update.',
  });
};
```

### Custom Duration
```tsx
// 10 seconds
notification.info({
  message: 'Long notification',
  description: 'This stays for 10 seconds',
  duration: 10,
});

// Never auto-close
notification.info({
  message: 'Persistent',
  description: 'Click X to close',
  duration: null,
});
```

### Placement
```tsx
notification.info({
  message: 'Bottom Left',
  description: 'This appears in the bottom left corner',
  placement: 'bottomLeft',
});
```

### With Action Buttons
```tsx
const key = `open${Date.now()}`;

notification.open({
  message: 'Confirm Action',
  description: 'Do you want to proceed with this action?',
  btn: (
    <Space>
      <Button size="small" onClick={() => notification.destroy(key)}>
        Cancel
      </Button>
      <Button type="primary" size="small" onClick={() => {
        handleConfirm();
        notification.destroy(key);
      }}>
        Confirm
      </Button>
    </Space>
  ),
  key,
  duration: null,
});
```

### Custom Icon
```tsx
import { SmileyIcon, CheckCircleIcon, XCircleIcon, WarningCircleIcon } from './icons';
import { theme } from 'antd';

const { token } = theme.useToken();

notification.open({
  message: 'Custom Icon',
  description: 'Notification with a custom icon',
  icon: <SmileyIcon weight="fill" style={{ color: '#108ee9' }} />,
});

// With semantic colors
notification.open({
  message: 'Success',
  description: 'Your changes have been saved successfully.',
  icon: <CheckCircleIcon color={token.colorSuccess} size={24} weight="fill" />,
});

notification.open({
  message: 'Error',
  description: 'There was an error processing your request.',
  icon: <XCircleIcon color={token.colorError} size={24} weight="fill" />,
});

notification.open({
  message: 'Warning',
  description: 'Your session will expire in 5 minutes.',
  icon: <WarningCircleIcon color={token.colorWarning} size={24} weight="fill" />,
});
```

### Update Existing Notification
```tsx
const key = 'updatable';

notification.open({
  key,
  message: 'Uploading...',
  description: 'Please wait while we upload your file.',
  duration: null,
});

// Later...
notification.open({
  key,
  message: 'Upload Complete',
  description: 'Your file has been uploaded successfully.',
  duration: 4.5,
});
```

### With Progress Bar
```tsx
notification.open({
  message: 'Auto-closing',
  description: 'Watch the progress bar',
  showProgress: true,
  pauseOnHover: true,
});
```

### Hooks API (Recommended)
```tsx
import { App } from 'antd';

const MyComponent = () => {
  const { notification } = App.useApp();

  const handleClick = () => {
    notification.success({
      message: 'Success',
      description: 'Operation completed',
    });
  };

  return <Button onClick={handleClick}>Notify</Button>;
};
```

### Stack Multiple
```tsx
// Notifications stack in their placement corner
for (let i = 0; i < 3; i++) {
  notification.info({
    message: `Notification ${i + 1}`,
    description: `This is notification number ${i + 1}`,
  });
}
```

## Usage Guidelines

1. **Use for detailed feedback**: Notifications have title + description for more context.

2. **Don't overuse**: Reserve for important events, not routine actions.

3. **Include actionable buttons when needed**: Use `btn` prop for user actions.

4. **Choose appropriate placement**: `topRight` for most apps; consider workflow.

5. **Use hooks API**: `App.useApp()` provides better React context handling.

6. **message vs notification**:
   - `message`: Brief, single-line feedback
   - `notification`: Detailed, multi-line notifications
