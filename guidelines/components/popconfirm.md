# Popconfirm

**Purpose**: Confirmation dialog in a popover style. Use for simple confirmations without blocking the entire page.

## When to Use

- Confirming destructive actions (delete, remove)
- Quick yes/no decisions
- When Modal would be too heavy-handed

## API Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `title` | Confirmation title | `ReactNode \| () => ReactNode` | - |
| `description` | Additional description | `ReactNode \| () => ReactNode` | - |
| `onConfirm` | Confirm callback | `(e) => void` | - |
| `onCancel` | Cancel callback | `(e) => void` | - |
| `okText` | Confirm button text | `ReactNode` | `'OK'` |
| `cancelText` | Cancel button text | `ReactNode` | `'Cancel'` |
| `okType` | Confirm button type | `ButtonType` | `'primary'` |
| `okButtonProps` | Confirm button props | `ButtonProps` | - |
| `cancelButtonProps` | Cancel button props | `ButtonProps` | - |
| `icon` | Custom icon | `ReactNode` | `<ExclamationCircleFilled />` |
| `showCancel` | Show cancel button | `boolean` | `true` |
| `disabled` | Disable popup | `boolean` | `false` |
| `open` | Visibility (controlled) | `boolean` | - |
| `onOpenChange` | Visibility change | `(open, e) => void` | - |
| `placement` | Position | Same as Tooltip | `'top'` |
| `trigger` | Trigger mode | Same as Tooltip | `'click'` |
| `arrow` | Show arrow | `boolean \| { pointAtCenter }` | `true` |

## Design Tokens Used

### Alias Tokens
- `colorBgElevated` - Popconfirm background
- `colorWarning` - Default icon color
- `colorText` - Title text
- `colorTextSecondary` - Description text
- `borderRadius` - Popconfirm radius
- `boxShadow` - Popconfirm shadow

## Examples

### Basic Popconfirm
```tsx
import { Popconfirm, Button } from 'antd';

<Popconfirm
  title="Delete this item?"
  onConfirm={() => console.log('Deleted')}
  onCancel={() => console.log('Cancelled')}
>
  <Button danger>Delete</Button>
</Popconfirm>
```

### With Description
```tsx
<Popconfirm
  title="Delete this item?"
  description="This action cannot be undone."
  onConfirm={handleDelete}
>
  <Button danger>Delete</Button>
</Popconfirm>
```

### Custom Button Text
```tsx
<Popconfirm
  title="Are you sure?"
  okText="Yes"
  cancelText="No"
  onConfirm={handleConfirm}
>
  <a href="#">Delete</a>
</Popconfirm>
```

### Danger Button Style
```tsx
<Popconfirm
  title="Delete permanently?"
  okText="Delete"
  okType="danger"
  onConfirm={handleDelete}
>
  <Button danger>Delete</Button>
</Popconfirm>
```

### Custom Icon
```tsx
import { QuestionCircleOutlined } from '@ant-design/icons';

<Popconfirm
  title="Are you sure?"
  icon={<QuestionCircleOutlined style={{ color: 'red' }} />}
  onConfirm={handleConfirm}
>
  <Button>Confirm</Button>
</Popconfirm>
```

### Async Confirm
```tsx
const [confirmLoading, setConfirmLoading] = useState(false);

const handleConfirm = async () => {
  setConfirmLoading(true);
  await deleteItem();
  setConfirmLoading(false);
};

<Popconfirm
  title="Delete?"
  okButtonProps={{ loading: confirmLoading }}
  onConfirm={handleConfirm}
>
  <Button danger>Delete</Button>
</Popconfirm>
```

### Controlled
```tsx
const [open, setOpen] = useState(false);

const handleConfirm = () => {
  handleDelete();
  setOpen(false);
};

<Popconfirm
  title="Delete?"
  open={open}
  onOpenChange={setOpen}
  onConfirm={handleConfirm}
  onCancel={() => setOpen(false)}
>
  <Button danger>Delete</Button>
</Popconfirm>
```

### Conditional Confirm
```tsx
const [open, setOpen] = useState(false);

const handleOpenChange = (newOpen) => {
  if (!newOpen) {
    setOpen(false);
    return;
  }
  // Only show popconfirm if condition is met
  if (hasUnsavedChanges) {
    setOpen(true);
  } else {
    handleNavigate();
  }
};

<Popconfirm
  title="You have unsaved changes. Leave anyway?"
  open={open}
  onOpenChange={handleOpenChange}
  onConfirm={handleNavigate}
>
  <Button>Leave Page</Button>
</Popconfirm>
```

### Placement
```tsx
<Popconfirm title="Confirm?" placement="topLeft">
  <Button>Top Left</Button>
</Popconfirm>

<Popconfirm title="Confirm?" placement="bottom">
  <Button>Bottom</Button>
</Popconfirm>
```

### In Table Actions
```tsx
const columns = [
  // ... other columns
  {
    title: 'Action',
    render: (_, record) => (
      <Space>
        <a onClick={() => handleEdit(record)}>Edit</a>
        <Popconfirm
          title="Delete this record?"
          onConfirm={() => handleDelete(record.id)}
        >
          <a>Delete</a>
        </Popconfirm>
      </Space>
    ),
  },
];
```

## Usage Guidelines

1. **Use for destructive actions**: Popconfirm is ideal for delete/remove confirmations.

2. **Keep title concise**: A short question works best.

3. **Add description for context**: Use `description` for additional details.

4. **Use danger style for destructive**: Set `okType="danger"` for delete actions.

5. **Handle async operations**: Show loading state during async confirms.

6. **Popconfirm vs Modal.confirm**:
   - Popconfirm: Lightweight, inline confirmation
   - Modal.confirm: More prominent, page-level confirmation
