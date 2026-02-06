# Switch

**Purpose**: Toggle between two states (on/off). Switches provide an immediate effect when toggled.

## When to Use

- Toggling a setting on or off
- Binary choices that take effect immediately
- Enabling/disabling features

## Component States

| State | Description | Visual Appearance |
|-------|-------------|-------------------|
| **Off** | Unchecked/disabled | Gray track, handle on left |
| **On** | Checked/enabled | Primary color track, handle on right |
| **Disabled** | Not interactive | Muted colors, no cursor |
| **Loading** | Processing change | Spinner in handle |

## API Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `checked` | Checked state (controlled) | `boolean` | `false` |
| `defaultChecked` | Initial checked state | `boolean` | `false` |
| `onChange` | Change handler | `(checked: boolean, event) => void` | - |
| `disabled` | Disabled state | `boolean` | `false` |
| `loading` | Loading state | `boolean` | `false` |
| `size` | Switch size | `'default' \| 'small'` | `'default'` |
| `checkedChildren` | Content when checked | `ReactNode` | - |
| `unCheckedChildren` | Content when unchecked | `ReactNode` | - |
| `autoFocus` | Focus on mount | `boolean` | `false` |

## Design Tokens Used

### Seed Tokens
- `colorPrimary` - Checked track color
- `borderRadius` - Handle radius

### Alias Tokens
- `colorTextQuaternary` - Unchecked track color
- `colorTextTertiary` - Unchecked track hover
- `colorBgContainer` - Handle color
- `controlHeight` - Switch height

## Examples

### Basic Switch
```tsx
import { Switch } from 'antd';

<Switch onChange={(checked) => console.log(checked)} />
```

### Controlled Switch
```tsx
const [checked, setChecked] = useState(false);

<Switch checked={checked} onChange={setChecked} />
```

### Default Checked
```tsx
<Switch defaultChecked />
```

### Disabled
```tsx
<Switch disabled />
<Switch disabled checked />
```

### Loading
```tsx
const [loading, setLoading] = useState(false);
const [checked, setChecked] = useState(false);

const handleChange = async (value) => {
  setLoading(true);
  await saveSettings(value);
  setChecked(value);
  setLoading(false);
};

<Switch
  checked={checked}
  loading={loading}
  onChange={handleChange}
/>
```

### With Text
```tsx
<Switch
  checkedChildren="ON"
  unCheckedChildren="OFF"
/>

<Switch
  checkedChildren="1"
  unCheckedChildren="0"
/>
```

### With Icons
```tsx
import { CheckOutlined, CloseOutlined } from '@ant-design/icons';

<Switch
  checkedChildren={<CheckOutlined />}
  unCheckedChildren={<CloseOutlined />}
/>
```

### Sizes
```tsx
<Switch size="default" />
<Switch size="small" />
```

### With Form
```tsx
<Form.Item name="notifications" label="Notifications" valuePropName="checked">
  <Switch />
</Form.Item>

// With label beside switch
<Form.Item name="darkMode" valuePropName="checked">
  <Space>
    <Switch />
    <span>Enable Dark Mode</span>
  </Space>
</Form.Item>
```

### In Settings List
```tsx
<List>
  <List.Item
    actions={[<Switch key="switch" defaultChecked />]}
  >
    <List.Item.Meta
      title="Email Notifications"
      description="Receive email updates about your account"
    />
  </List.Item>
  <List.Item
    actions={[<Switch key="switch" />]}
  >
    <List.Item.Meta
      title="Push Notifications"
      description="Receive push notifications on your device"
    />
  </List.Item>
</List>
```

## Usage Guidelines

1. **Immediate effect**: Switch changes should take effect immediately without a save button.

2. **Binary choice only**: Use for on/off, yes/no, enable/disable choices.

3. **Show loading for async**: Use `loading` when the toggle triggers an async operation.

4. **Label describes the "on" state**: The label should describe what happens when enabled.

5. **Use `valuePropName="checked"` with Form**: Required for proper Form integration.

6. **Consider Checkbox for form submissions**: If the change requires a form submit, use Checkbox instead.
