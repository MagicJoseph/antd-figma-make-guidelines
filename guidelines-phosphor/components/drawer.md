# Drawer

**Purpose**: Panel that slides out from the edge of the screen. Drawers provide supplementary content without leaving the current page.

## When to Use

- Side panels for details or forms
- Mobile navigation menus
- Settings panels
- Preview/edit content without full page navigation

## API Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `open` | Drawer visibility | `boolean` | `false` |
| `onClose` | Close handler | `(e) => void` | - |
| `title` | Drawer title | `ReactNode` | - |
| `placement` | Drawer position | `'top' \| 'right' \| 'bottom' \| 'left'` | `'right'` |
| `width` | Width (left/right) | `number \| string` | `378` |
| `height` | Height (top/bottom) | `number \| string` | `378` |
| `closable` | Show close button | `boolean` | `true` |
| `closeIcon` | Custom close icon | `ReactNode` | - |
| `mask` | Show mask | `boolean` | `true` |
| `maskClosable` | Close on mask click | `boolean` | `true` |
| `keyboard` | Close on Esc | `boolean` | `true` |
| `footer` | Footer content | `ReactNode` | - |
| `extra` | Extra header content | `ReactNode` | - |
| `destroyOnHidden` | Destroy children on close | `boolean` | `false` |
| `forceRender` | Force render content | `boolean` | `false` |
| `getContainer` | Mount container | `HTMLElement \| () => HTMLElement \| string \| false` | `body` |
| `push` | Push content when nested | `boolean \| { distance }` | `true` |
| `zIndex` | z-index value | `number` | `1000` |
| `afterOpenChange` | Open/close animation callback | `(open) => void` | - |
| `styles` | Custom styles | `{ header, body, footer, mask, content, wrapper }` | - |
| `classNames` | Custom classes | Same as styles | - |
| `loading` | Show loading skeleton | `boolean` | `false` |

## Design Tokens Used

### Alias Tokens
- `colorBgElevated` - Drawer background
- `colorBgMask` - Mask overlay
- `colorText` - Content text
- `colorTextHeading` - Title text
- `padding` - Content padding
- `paddingLG` - Large padding

## Examples

### Basic Drawer
```tsx
import { Drawer, Button } from 'antd';
import { useState } from 'react';

const App = () => {
  const [open, setOpen] = useState(false);

  return (
    <>
      <Button type="primary" onClick={() => setOpen(true)}>
        Open Drawer
      </Button>
      <Drawer
        title="Basic Drawer"
        onClose={() => setOpen(false)}
        open={open}
      >
        <p>Drawer content...</p>
      </Drawer>
    </>
  );
};
```

### Different Placements
```tsx
<Drawer placement="left" open={open} onClose={onClose}>
  Left Drawer
</Drawer>

<Drawer placement="right" open={open} onClose={onClose}>
  Right Drawer
</Drawer>

<Drawer placement="top" open={open} onClose={onClose}>
  Top Drawer
</Drawer>

<Drawer placement="bottom" open={open} onClose={onClose}>
  Bottom Drawer
</Drawer>
```

### Custom Width/Height
```tsx
<Drawer
  title="Wide Drawer"
  placement="right"
  width={720}
  open={open}
  onClose={onClose}
>
  Content
</Drawer>

<Drawer
  title="Tall Drawer"
  placement="bottom"
  height={400}
  open={open}
  onClose={onClose}
>
  Content
</Drawer>
```

### With Footer
```tsx
<Drawer
  title="Form Drawer"
  open={open}
  onClose={onClose}
  footer={
    <Space>
      <Button onClick={onClose}>Cancel</Button>
      <Button type="primary" onClick={handleSubmit}>
        Submit
      </Button>
    </Space>
  }
>
  <Form layout="vertical">
    <Form.Item label="Name" name="name">
      <Input />
    </Form.Item>
  </Form>
</Drawer>
```

### With Extra Header Content
```tsx
<Drawer
  title="Drawer with Extra"
  extra={
    <Space>
      <Button onClick={onClose}>Cancel</Button>
      <Button type="primary" onClick={handleSave}>
        Save
      </Button>
    </Space>
  }
  open={open}
  onClose={onClose}
>
  Content
</Drawer>
```

### Multi-level Drawer
```tsx
const [open, setOpen] = useState(false);
const [childOpen, setChildOpen] = useState(false);

<Drawer
  title="Parent Drawer"
  open={open}
  onClose={() => setOpen(false)}
>
  <Button type="primary" onClick={() => setChildOpen(true)}>
    Open Child Drawer
  </Button>
  <Drawer
    title="Child Drawer"
    open={childOpen}
    onClose={() => setChildOpen(false)}
  >
    Child content
  </Drawer>
</Drawer>
```

### Form in Drawer
```tsx
const [form] = Form.useForm();

<Drawer
  title="Create User"
  open={open}
  onClose={() => {
    form.resetFields();
    setOpen(false);
  }}
  footer={
    <Space>
      <Button onClick={() => setOpen(false)}>Cancel</Button>
      <Button type="primary" onClick={() => form.submit()}>
        Submit
      </Button>
    </Space>
  }
  destroyOnHidden
>
  <Form form={form} layout="vertical" onFinish={handleFinish}>
    <Form.Item name="name" label="Name" rules={[{ required: true }]}>
      <Input />
    </Form.Item>
    <Form.Item name="email" label="Email" rules={[{ required: true, type: 'email' }]}>
      <Input />
    </Form.Item>
  </Form>
</Drawer>
```

### Loading State
```tsx
<Drawer
  title="Loading Drawer"
  open={open}
  loading={isLoading}
  onClose={onClose}
>
  {data && <div>{data.content}</div>}
</Drawer>
```

### Prevent Close
```tsx
<Drawer
  title="Protected Drawer"
  open={open}
  maskClosable={false}
  keyboard={false}
  closable={false}
  onClose={onClose}
  footer={
    <Button type="primary" onClick={onClose}>
      Close
    </Button>
  }
>
  Cannot close by clicking outside or pressing Esc
</Drawer>
```

## Usage Guidelines

1. **Use for contextual content**: Drawers keep users on the current page.

2. **Choose appropriate placement**:
   - `right`: Forms, details panels (default)
   - `left`: Navigation menus
   - `bottom`: Mobile actions, filters
   - `top`: Notifications, announcements

3. **Use footer for actions**: Place submit/cancel buttons in footer.

4. **Reset form on close**: Use `destroyOnHidden` or manual reset.

5. **Reasonable width**: 378px default is good; 720px for complex forms.

6. **Drawer vs Modal**:
   - Modal: Quick confirmations, small forms
   - Drawer: Detailed forms, side panels, navigation
