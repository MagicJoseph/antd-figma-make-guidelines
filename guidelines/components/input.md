# Input

**Purpose**: Accept text input from users. Used for forms, search fields, and any place where text data entry is needed.

## When to Use

- Single-line text input
- Password entry
- Search fields
- Numeric input (consider InputNumber for strict number validation)
- Text with prefix/suffix icons or labels

## Component States

| State | Description | Visual Appearance |
|-------|-------------|-------------------|
| **Default** | Normal resting state | Standard border |
| **Hover** | Mouse over | Border color changes to primary |
| **Focus** | Active input | Primary border color, focus shadow |
| **Disabled** | Not editable | Gray background, muted text |
| **Error** | Validation failed | Red border |
| **Warning** | Validation warning | Yellow/orange border |

## API Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `value` | Input value (controlled) | `string` | - |
| `defaultValue` | Initial value (uncontrolled) | `string` | - |
| `onChange` | Change handler | `(e: ChangeEvent) => void` | - |
| `placeholder` | Placeholder text | `string` | - |
| `disabled` | Disabled state | `boolean` | `false` |
| `status` | Validation status | `'error' \| 'warning'` | - |
| `size` | Input size | `'large' \| 'middle' \| 'small'` | `'middle'` |
| `prefix` | Prefix icon/element | `ReactNode` | - |
| `suffix` | Suffix icon/element | `ReactNode` | - |
| `addonBefore` | Addon before input | `ReactNode` | - |
| `addonAfter` | Addon after input | `ReactNode` | - |
| `allowClear` | Show clear button | `boolean \| { clearIcon: ReactNode }` | `false` |
| `maxLength` | Maximum characters | `number` | - |
| `showCount` | Show character count | `boolean \| { formatter }` | `false` |
| `bordered` | Show border | `boolean` | `true` |
| `variant` | Input variant | `'outlined' \| 'borderless' \| 'filled'` | `'outlined'` |

## Input.Password Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `visibilityToggle` | Show/hide toggle | `boolean \| { visible, onVisibleChange }` | `true` |
| `iconRender` | Custom visibility icon | `(visible: boolean) => ReactNode` | - |

## Input.TextArea Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `rows` | Number of rows | `number` | - |
| `autoSize` | Auto resize | `boolean \| { minRows, maxRows }` | `false` |
| `showCount` | Show character count | `boolean \| { formatter }` | `false` |
| `maxLength` | Maximum characters | `number` | - |

## Input.Search Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `enterButton` | Search button | `boolean \| ReactNode` | `false` |
| `loading` | Loading state | `boolean` | `false` |
| `onSearch` | Search callback | `(value, event, info) => void` | - |

## Design Tokens Used

### Seed Tokens
- `colorPrimary` - Focus border color
- `colorError` - Error state border
- `colorWarning` - Warning state border
- `borderRadius` - Input corner radius
- `fontSize` - Input text size

### Alias Tokens
- `colorBgContainer` - Input background
- `colorBorder` - Default border color
- `colorText` - Input text color
- `colorTextPlaceholder` - Placeholder text color
- `colorTextDisabled` - Disabled text color
- `colorBgContainerDisabled` - Disabled background
- `controlHeight` - Input height
- `controlHeightSM` - Small input height
- `controlHeightLG` - Large input height

## Examples

### Basic Input
```tsx
import { Input } from 'antd';

<Input placeholder="Enter text" />

// Controlled
const [value, setValue] = useState('');
<Input
  value={value}
  onChange={(e) => setValue(e.target.value)}
/>
```

### With Prefix/Suffix
```tsx
import { Input } from 'antd';
import { UserOutlined, InfoCircleOutlined } from '@ant-design/icons';

<Input
  prefix={<UserOutlined />}
  placeholder="Username"
/>

<Input
  suffix={<InfoCircleOutlined />}
  placeholder="With suffix icon"
/>
```

### With Addons
```tsx
<Input addonBefore="http://" addonAfter=".com" defaultValue="mysite" />

<Input
  addonBefore={
    <Select defaultValue="http://">
      <Select.Option value="http://">http://</Select.Option>
      <Select.Option value="https://">https://</Select.Option>
    </Select>
  }
  defaultValue="example.com"
/>
```

### Status (Error/Warning)
```tsx
<Input status="error" placeholder="Error input" />
<Input status="warning" placeholder="Warning input" />
```

### Clearable
```tsx
<Input allowClear placeholder="Clearable input" />
```

### Character Count
```tsx
<Input showCount maxLength={20} placeholder="Max 20 characters" />
```

### Sizes
```tsx
<Input size="large" placeholder="Large" />
<Input placeholder="Default" />
<Input size="small" placeholder="Small" />
```

### Password Input
```tsx
import { Input } from 'antd';

<Input.Password placeholder="Password" />

// Custom visibility toggle
<Input.Password
  placeholder="Password"
  iconRender={(visible) => (visible ? <EyeOutlined /> : <EyeInvisibleOutlined />)}
/>
```

### TextArea
```tsx
import { Input } from 'antd';

const { TextArea } = Input;

<TextArea rows={4} placeholder="Multi-line text" />

// Auto-resize
<TextArea
  autoSize={{ minRows: 2, maxRows: 6 }}
  placeholder="Auto-resizing textarea"
/>

// With character count
<TextArea
  showCount
  maxLength={100}
  placeholder="Max 100 characters"
/>
```

### Search Input
```tsx
import { Input } from 'antd';

const { Search } = Input;

<Search
  placeholder="Search..."
  onSearch={(value) => console.log(value)}
/>

// With button
<Search
  placeholder="Search..."
  enterButton="Search"
  size="large"
  onSearch={(value) => console.log(value)}
/>

// Loading state
<Search
  placeholder="Search..."
  loading={isSearching}
  onSearch={handleSearch}
/>
```

### Input Group (Compact)
```tsx
import { Input, Space } from 'antd';

<Space.Compact>
  <Input style={{ width: '20%' }} defaultValue="0571" />
  <Input style={{ width: '80%' }} defaultValue="26888888" />
</Space.Compact>
```

## Usage Guidelines

1. **Use appropriate input types**: Use `Input.Password` for passwords, `Input.Search` for search, `Input.TextArea` for multi-line.

2. **Always include placeholder text**: Help users understand what to enter.

3. **Show validation status**: Use `status` prop to indicate errors or warnings.

4. **Use icons for context**: Prefix icons help identify the input purpose (user icon for username, etc.).

5. **Limit character count when appropriate**: Use `maxLength` with `showCount` for limited fields.

6. **Form integration**: When using with Form, the Form.Item handles value and validation automatically.
