# Select

**Purpose**: Provide a dropdown menu for selecting from a list of options. Use when users need to choose from multiple predefined choices.

## When to Use

- **4-20 options**: Select is ideal for moderate option counts
- **2-4 options**: Consider Radio buttons instead
- **20+ options**: Consider adding search or using AutoComplete
- **Dynamic/async data**: Select supports loading states and async fetching

## Component States

| State | Description | Visual Appearance |
|-------|-------------|-------------------|
| **Default** | Closed dropdown | Shows selected value or placeholder |
| **Hover** | Mouse over | Border color changes |
| **Focus/Open** | Dropdown visible | Primary border, dropdown panel shown |
| **Disabled** | Not selectable | Gray background, no interaction |
| **Loading** | Fetching options | Spinner in dropdown |
| **Error** | Validation failed | Red border |
| **Warning** | Validation warning | Yellow border |

## API Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `value` | Selected value (controlled) | `string \| string[] \| number \| number[]` | - |
| `defaultValue` | Initial value | Same as value | - |
| `onChange` | Selection change handler | `(value, option) => void` | - |
| `options` | Options array | `{ label, value, disabled? }[]` | - |
| `placeholder` | Placeholder text | `string` | - |
| `disabled` | Disabled state | `boolean` | `false` |
| `loading` | Loading state | `boolean` | `false` |
| `status` | Validation status | `'error' \| 'warning'` | - |
| `size` | Select size | `'large' \| 'middle' \| 'small'` | `'middle'` |
| `mode` | Selection mode | `'multiple' \| 'tags'` | - |
| `allowClear` | Show clear button | `boolean` | `false` |
| `showSearch` | Enable search | `boolean` | `false` (single), `true` (multiple) |
| `filterOption` | Filter function | `boolean \| (input, option) => boolean` | `true` |
| `optionFilterProp` | Prop to filter on | `string \| string[]` | `'value'` |
| `variant` | Select variant | `'outlined' \| 'borderless' \| 'filled'` | `'outlined'` |
| `open` | Dropdown open state (controlled) | `boolean` | - |
| `onDropdownVisibleChange` | Dropdown visibility handler | `(open) => void` | - |
| `dropdownRender` | Custom dropdown content | `(menu) => ReactNode` | - |
| `maxTagCount` | Max tags to display | `number \| 'responsive'` | - |
| `virtual` | Enable virtual scroll | `boolean` | `true` |

## Option Props

| Property | Description | Type |
|----------|-------------|------|
| `value` | Option value | `string \| number` |
| `label` | Display label | `ReactNode` |
| `disabled` | Disabled option | `boolean` |
| `title` | Title attribute | `string` |

## Design Tokens Used

### Seed Tokens
- `colorPrimary` - Focus border, selected option
- `colorError` - Error state border
- `colorWarning` - Warning state border
- `borderRadius` - Select corner radius
- `fontSize` - Text size

### Alias Tokens
- `colorBgContainer` - Select background
- `colorBgElevated` - Dropdown background
- `colorBorder` - Default border
- `colorText` - Text color
- `colorTextPlaceholder` - Placeholder color
- `colorTextDisabled` - Disabled text
- `colorPrimaryBg` - Selected option background
- `controlHeight` - Select height

## Examples

### Basic Select
```tsx
import { Select } from 'antd';

<Select
  style={{ width: 200 }}
  placeholder="Select an option"
  options={[
    { value: 'jack', label: 'Jack' },
    { value: 'lucy', label: 'Lucy' },
    { value: 'tom', label: 'Tom' },
  ]}
/>

// Controlled
const [value, setValue] = useState(null);

<Select
  value={value}
  onChange={setValue}
  style={{ width: 200 }}
  options={options}
/>
```

### With Disabled Options
```tsx
<Select
  style={{ width: 200 }}
  options={[
    { value: 'jack', label: 'Jack' },
    { value: 'lucy', label: 'Lucy' },
    { value: 'disabled', label: 'Disabled', disabled: true },
  ]}
/>
```

### Multiple Selection
```tsx
<Select
  mode="multiple"
  style={{ width: '100%' }}
  placeholder="Select multiple"
  options={options}
/>

// With max tag count
<Select
  mode="multiple"
  maxTagCount="responsive"
  style={{ width: '100%' }}
  options={options}
/>
```

### Tags Mode (Create New)
```tsx
<Select
  mode="tags"
  style={{ width: '100%' }}
  placeholder="Select or create tags"
  options={options}
/>
```

### With Search
```tsx
<Select
  showSearch
  style={{ width: 200 }}
  placeholder="Search to Select"
  optionFilterProp="label"
  filterOption={(input, option) =>
    (option?.label ?? '').toLowerCase().includes(input.toLowerCase())
  }
  options={options}
/>
```

### Loading State
```tsx
<Select
  loading={isLoading}
  style={{ width: 200 }}
  placeholder="Loading options..."
  options={options}
/>
```

### Status (Error/Warning)
```tsx
<Select status="error" style={{ width: 200 }} />
<Select status="warning" style={{ width: 200 }} />
```

### Clearable
```tsx
<Select
  allowClear
  style={{ width: 200 }}
  placeholder="Clearable"
  options={options}
/>
```

### Sizes
```tsx
<Select size="large" style={{ width: 200 }} options={options} />
<Select style={{ width: 200 }} options={options} />
<Select size="small" style={{ width: 200 }} options={options} />
```

### Option Groups
```tsx
<Select
  style={{ width: 200 }}
  options={[
    {
      label: 'Manager',
      options: [
        { value: 'jack', label: 'Jack' },
        { value: 'lucy', label: 'Lucy' },
      ],
    },
    {
      label: 'Engineer',
      options: [
        { value: 'tom', label: 'Tom' },
      ],
    },
  ]}
/>
```

### Custom Option Render
```tsx
<Select
  style={{ width: 200 }}
  optionRender={(option) => (
    <Space>
      <Avatar size="small">{option.data.label[0]}</Avatar>
      {option.data.label}
    </Space>
  )}
  options={options}
/>
```

### Custom Dropdown with Extra Content
```tsx
import { PlusIcon, CaretDownIcon, XIcon, CheckIcon, XCircleIcon } from './icons';

<Select
  style={{ width: 200 }}
  suffixIcon={<CaretDownIcon weight="bold" />}
  dropdownRender={(menu) => (
    <>
      {menu}
      <Divider style={{ margin: '8px 0' }} />
      <Button type="text" icon={<PlusIcon weight="bold" />} block>
        Add item
      </Button>
    </>
  )}
  options={options}
/>

// Multiple select with custom icons
<Select
  mode="multiple"
  style={{ width: '100%' }}
  suffixIcon={<CaretDownIcon weight="bold" />}
  removeIcon={<XIcon size={12} weight="bold" />}
  menuItemSelectedIcon={<CheckIcon weight="bold" />}
  allowClear={{ clearIcon: <XCircleIcon weight="fill" /> }}
  options={options}
/>
```

### Async Options Loading
```tsx
const [options, setOptions] = useState([]);
const [loading, setLoading] = useState(false);

const handleSearch = async (searchText) => {
  setLoading(true);
  const results = await fetchOptions(searchText);
  setOptions(results);
  setLoading(false);
};

<Select
  showSearch
  loading={loading}
  onSearch={handleSearch}
  filterOption={false}
  options={options}
  style={{ width: 200 }}
/>
```

## Usage Guidelines

1. **Use `options` prop**: Prefer the `options` prop over `<Select.Option>` children for better performance.

2. **Set appropriate width**: Select needs explicit width; use `style={{ width: 200 }}` or CSS class.

3. **Enable search for long lists**: Use `showSearch` when options exceed ~10 items.

4. **Use descriptive labels**: Option labels should be clear and concise.

5. **Handle loading states**: Show loading indicator when fetching options asynchronously.

6. **Consider virtual scroll**: Enabled by default; keep it on for large option lists (100+).

7. **Form integration**: When using with Form, Form.Item handles value and validation automatically.
