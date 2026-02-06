# Modal

**Purpose**: Display content in a layer above the page. Modals focus user attention on a specific task or information that requires interaction before continuing.

## When to Use

- Require user input or confirmation before proceeding
- Display important information that needs acknowledgment
- Complex forms or multi-step processes
- Viewing details without leaving the current page
- Confirmation before destructive actions

## Component States

| State | Description | Visual Appearance |
|-------|-------------|-------------------|
| **Closed** | Modal not visible | No modal, page accessible |
| **Open** | Modal visible | Centered dialog with backdrop |
| **Loading** | Confirming action | OK button shows spinner |
| **Closing** | Exit animation | Fade out animation |

## API Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `open` | Modal visibility | `boolean` | `false` |
| `title` | Modal title | `ReactNode` | - |
| `footer` | Footer content (null to hide) | `ReactNode \| null` | OK + Cancel buttons |
| `onOk` | OK button handler | `(e) => void` | - |
| `onCancel` | Cancel/close handler | `(e) => void` | - |
| `confirmLoading` | OK button loading state | `boolean` | `false` |
| `width` | Modal width | `string \| number` | `520` |
| `centered` | Vertically center | `boolean` | `false` |
| `closable` | Show close button | `boolean` | `true` |
| `closeIcon` | Custom close icon | `ReactNode` | `<CloseOutlined />` |
| `maskClosable` | Close on mask click | `boolean` | `true` |
| `keyboard` | Close on Esc key | `boolean` | `true` |
| `destroyOnHidden` | Destroy children on close | `boolean` | `false` |
| `forceRender` | Force render content | `boolean` | `false` |
| `okText` | OK button text | `ReactNode` | `'OK'` |
| `cancelText` | Cancel button text | `ReactNode` | `'Cancel'` |
| `okType` | OK button type | `ButtonType` | `'primary'` |
| `okButtonProps` | OK button props | `ButtonProps` | - |
| `cancelButtonProps` | Cancel button props | `ButtonProps` | - |
| `mask` | Show mask | `boolean` | `true` |
| `zIndex` | z-index value | `number` | `1000` |
| `getContainer` | Mount container | `HTMLElement \| () => HTMLElement \| string \| false` | `document.body` |
| `afterClose` | Callback after close animation | `() => void` | - |
| `afterOpenChange` | Callback after open/close | `(open: boolean) => void` | - |
| `loading` | Show skeleton placeholder | `boolean` | `false` |
| `styles` | Custom styles for parts | `{ header, body, footer, mask, content, wrapper }` | - |
| `classNames` | Custom classes for parts | `{ header, body, footer, mask, content, wrapper }` | - |

## Design Tokens Used

### Alias Tokens
- `colorBgElevated` - Modal background
- `colorBgMask` - Backdrop overlay color
- `colorText` - Content text
- `colorTextHeading` - Title text
- `borderRadius` - Modal corner radius (borderRadiusLG)
- `padding` - Content padding
- `boxShadow` - Modal shadow (boxShadowSecondary)

## Examples

### Basic Modal
```tsx
import { Modal, Button } from 'antd';
import { useState } from 'react';

const App = () => {
  const [open, setOpen] = useState(false);

  return (
    <>
      <Button type="primary" onClick={() => setOpen(true)}>
        Open Modal
      </Button>
      <Modal
        title="Basic Modal"
        open={open}
        onOk={() => setOpen(false)}
        onCancel={() => setOpen(false)}
      >
        <p>Modal content...</p>
      </Modal>
    </>
  );
};
```

### Async Close (with Loading)
```tsx
const [open, setOpen] = useState(false);
const [confirmLoading, setConfirmLoading] = useState(false);

const handleOk = async () => {
  setConfirmLoading(true);
  await submitData();
  setConfirmLoading(false);
  setOpen(false);
};

<Modal
  title="Submit Form"
  open={open}
  confirmLoading={confirmLoading}
  onOk={handleOk}
  onCancel={() => setOpen(false)}
>
  <p>Your data will be submitted...</p>
</Modal>
```

### Custom Footer
```tsx
<Modal
  title="Custom Footer"
  open={open}
  footer={[
    <Button key="back" onClick={() => setOpen(false)}>
      Return
    </Button>,
    <Button key="submit" type="primary" loading={loading} onClick={handleSubmit}>
      Submit
    </Button>,
  ]}
  onCancel={() => setOpen(false)}
>
  <p>Modal content...</p>
</Modal>

// No footer
<Modal
  title="No Footer"
  open={open}
  footer={null}
  onCancel={() => setOpen(false)}
>
  <p>Content only, no buttons.</p>
</Modal>
```

### Centered Modal
```tsx
<Modal
  title="Centered Modal"
  open={open}
  centered
  onOk={() => setOpen(false)}
  onCancel={() => setOpen(false)}
>
  <p>This modal is vertically centered.</p>
</Modal>
```

### Custom Width
```tsx
<Modal
  title="Wide Modal"
  open={open}
  width={800}
  onOk={() => setOpen(false)}
  onCancel={() => setOpen(false)}
>
  <p>This modal is 800px wide.</p>
</Modal>

// Percentage width
<Modal width="80%">...</Modal>
```

### Confirmation Modal (Static Method)
```tsx
import { Modal, Button } from 'antd';
import { ExclamationCircleOutlined } from '@ant-design/icons';

// Confirm dialog
Modal.confirm({
  title: 'Do you want to delete this item?',
  icon: <ExclamationCircleOutlined />,
  content: 'This action cannot be undone.',
  okText: 'Yes',
  okType: 'danger',
  cancelText: 'No',
  onOk() {
    console.log('Deleted');
  },
  onCancel() {
    console.log('Cancelled');
  },
});

// Success
Modal.success({
  title: 'Success!',
  content: 'Your changes have been saved.',
});

// Error
Modal.error({
  title: 'Error',
  content: 'Something went wrong.',
});

// Warning
Modal.warning({
  title: 'Warning',
  content: 'Please review your input.',
});

// Info
Modal.info({
  title: 'Information',
  content: 'Here is some helpful info.',
});
```

### Destroy Confirmation on Close
```tsx
// For forms, destroy content on close to reset state
<Modal
  title="Form Modal"
  open={open}
  destroyOnHidden
  onCancel={() => setOpen(false)}
>
  <Form>
    <Form.Item name="field">
      <Input />
    </Form.Item>
  </Form>
</Modal>
```

### Modal with Form
```tsx
const [form] = Form.useForm();
const [open, setOpen] = useState(false);

const handleOk = async () => {
  try {
    const values = await form.validateFields();
    console.log('Form values:', values);
    setOpen(false);
    form.resetFields();
  } catch (error) {
    console.log('Validation failed:', error);
  }
};

<Modal
  title="Create User"
  open={open}
  onOk={handleOk}
  onCancel={() => {
    setOpen(false);
    form.resetFields();
  }}
>
  <Form form={form} layout="vertical">
    <Form.Item
      name="username"
      label="Username"
      rules={[{ required: true }]}
    >
      <Input />
    </Form.Item>
    <Form.Item
      name="email"
      label="Email"
      rules={[{ required: true, type: 'email' }]}
    >
      <Input />
    </Form.Item>
  </Form>
</Modal>
```

### Prevent Close on Mask Click
```tsx
<Modal
  title="Protected Modal"
  open={open}
  maskClosable={false}
  keyboard={false}
  onCancel={() => setOpen(false)}
>
  <p>Cannot close by clicking outside or pressing Esc.</p>
</Modal>
```

## Usage Guidelines

1. **Keep modals focused**: One task per modal; don't overload with multiple actions.

2. **Use appropriate width**: Default 520px works for most content; increase for complex forms/tables.

3. **Provide clear actions**: Use descriptive button text like "Save Changes" instead of just "OK".

4. **Handle loading states**: Show `confirmLoading` during async operations.

5. **Use confirmation modals for destructive actions**: `Modal.confirm` with `okType="danger"` for deletes.

6. **Reset forms on close**: Use `destroyOnHidden` or manually reset form state.

7. **Accessibility**: Modals trap focus and close on Esc by default (keep keyboard enabled).

8. **Avoid nested modals**: Opening a modal from another modal creates poor UX.
