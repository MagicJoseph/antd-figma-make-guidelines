# Radio

**Purpose**: Allow users to select a single option from a set of mutually exclusive choices.

## When to Use

- Selecting one option from 2-5 choices
- When all options should be visible
- Mutually exclusive selections (only one can be chosen)

## Component States

| State | Description | Visual Appearance |
|-------|-------------|-------------------|
| **Unselected** | Not chosen | Empty circle |
| **Selected** | Currently chosen | Filled circle |
| **Disabled** | Not interactive | Grayed out |
| **Hover** | Mouse over | Border highlight |
| **Focus** | Keyboard focus | Focus ring |

## API Props (Radio)

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `checked` | Checked state (controlled) | `boolean` | - |
| `defaultChecked` | Initial checked state | `boolean` | `false` |
| `value` | Radio value | `any` | - |
| `disabled` | Disabled state | `boolean` | `false` |
| `autoFocus` | Focus on mount | `boolean` | `false` |

## API Props (Radio.Group)

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `value` | Selected value (controlled) | `any` | - |
| `defaultValue` | Initial selected value | `any` | - |
| `options` | Options array | `string[] \| number[] \| { label, value, disabled }[]` | - |
| `onChange` | Change handler | `(e: RadioChangeEvent) => void` | - |
| `disabled` | Disable all radios | `boolean` | `false` |
| `optionType` | Option style | `'default' \| 'button'` | `'default'` |
| `buttonStyle` | Button style (when optionType="button") | `'outline' \| 'solid'` | `'outline'` |
| `size` | Size (button style only) | `'large' \| 'middle' \| 'small'` | `'middle'` |

## Design Tokens Used

### Seed Tokens
- `colorPrimary` - Selected radio color
- `fontSize` - Label text size

### Alias Tokens
- `colorBgContainer` - Unselected background
- `colorBorder` - Unselected border
- `colorText` - Label text
- `colorTextDisabled` - Disabled text
- `controlInteractiveSize` - Radio size

## Examples

### Basic Radio Group
```tsx
import { Radio } from 'antd';

<Radio.Group onChange={(e) => console.log(e.target.value)} defaultValue="a">
  <Radio value="a">Option A</Radio>
  <Radio value="b">Option B</Radio>
  <Radio value="c">Option C</Radio>
</Radio.Group>
```

### Using Options Array
```tsx
const options = [
  { label: 'Apple', value: 'apple' },
  { label: 'Pear', value: 'pear' },
  { label: 'Orange', value: 'orange' },
];

<Radio.Group options={options} defaultValue="apple" />
```

### Controlled Radio Group
```tsx
const [value, setValue] = useState('apple');

<Radio.Group value={value} onChange={(e) => setValue(e.target.value)}>
  <Radio value="apple">Apple</Radio>
  <Radio value="pear">Pear</Radio>
  <Radio value="orange">Orange</Radio>
</Radio.Group>
```

### Vertical Layout
```tsx
<Radio.Group>
  <Space direction="vertical">
    <Radio value={1}>Option 1</Radio>
    <Radio value={2}>Option 2</Radio>
    <Radio value={3}>Option 3</Radio>
  </Space>
</Radio.Group>
```

### Radio Button Style
```tsx
<Radio.Group defaultValue="a" optionType="button">
  <Radio.Button value="a">Option A</Radio.Button>
  <Radio.Button value="b">Option B</Radio.Button>
  <Radio.Button value="c">Option C</Radio.Button>
</Radio.Group>

// Or with options
<Radio.Group
  options={options}
  optionType="button"
  defaultValue="apple"
/>
```

### Solid Button Style
```tsx
<Radio.Group
  options={options}
  optionType="button"
  buttonStyle="solid"
  defaultValue="apple"
/>
```

### Button Sizes
```tsx
<Radio.Group optionType="button" size="large" options={options} />
<Radio.Group optionType="button" size="middle" options={options} />
<Radio.Group optionType="button" size="small" options={options} />
```

### Disabled
```tsx
<Radio.Group disabled defaultValue="a">
  <Radio value="a">Option A</Radio>
  <Radio value="b">Option B</Radio>
</Radio.Group>

// Individual disabled
<Radio.Group>
  <Radio value="a">Option A</Radio>
  <Radio value="b" disabled>Option B (disabled)</Radio>
</Radio.Group>
```

### With Form
```tsx
<Form.Item name="gender" label="Gender" rules={[{ required: true }]}>
  <Radio.Group>
    <Radio value="male">Male</Radio>
    <Radio value="female">Female</Radio>
    <Radio value="other">Other</Radio>
  </Radio.Group>
</Form.Item>
```

## Usage Guidelines

1. **Use for mutually exclusive options**: Only one option can be selected.

2. **2-5 visible options**: For more options, consider Select or dropdown.

3. **All options visible**: Unlike Select, all Radio options are always shown.

4. **Use button style for segmented controls**: `optionType="button"` for compact selection.

5. **Vertical for long labels**: Stack vertically when labels are long or numerous.

6. **Always have a default**: Pre-select the most common or recommended option.
