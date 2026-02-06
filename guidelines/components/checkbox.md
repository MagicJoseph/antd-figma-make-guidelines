# Checkbox

**Purpose**: Allow users to select one or more options from a set, or toggle a single option on/off.

## When to Use

- Multiple selections from several options
- Single boolean toggle (agree to terms, remember me)
- Select all / select none scenarios

## Component States

| State | Description | Visual Appearance |
|-------|-------------|-------------------|
| **Unchecked** | Not selected | Empty box |
| **Checked** | Selected | Box with checkmark |
| **Indeterminate** | Partial selection | Box with dash (for "select all") |
| **Disabled** | Not interactive | Grayed out |
| **Hover** | Mouse over | Border color change |
| **Focus** | Keyboard focus | Focus ring |

## API Props (Checkbox)

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `checked` | Checked state (controlled) | `boolean` | `false` |
| `defaultChecked` | Initial checked state | `boolean` | `false` |
| `onChange` | Change handler | `(e: CheckboxChangeEvent) => void` | - |
| `disabled` | Disabled state | `boolean` | `false` |
| `indeterminate` | Indeterminate state | `boolean` | `false` |
| `autoFocus` | Focus on mount | `boolean` | `false` |

## API Props (Checkbox.Group)

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `value` | Selected values (controlled) | `string[] \| number[]` | - |
| `defaultValue` | Initial selected values | `string[] \| number[]` | `[]` |
| `options` | Options array | `string[] \| number[] \| { label, value, disabled }[]` | - |
| `onChange` | Change handler | `(checkedValues) => void` | - |
| `disabled` | Disable all checkboxes | `boolean` | `false` |

## Design Tokens Used

### Seed Tokens
- `colorPrimary` - Checked checkbox color
- `borderRadius` - Checkbox corner radius (borderRadiusSM)

### Alias Tokens
- `colorBgContainer` - Unchecked background
- `colorBorder` - Unchecked border
- `colorText` - Label text
- `colorTextDisabled` - Disabled label
- `controlInteractiveSize` - Checkbox size

## Examples

### Basic Checkbox
```tsx
import { Checkbox } from 'antd';

<Checkbox onChange={(e) => console.log(e.target.checked)}>
  Checkbox
</Checkbox>
```

### Controlled Checkbox
```tsx
const [checked, setChecked] = useState(false);

<Checkbox
  checked={checked}
  onChange={(e) => setChecked(e.target.checked)}
>
  Controlled
</Checkbox>
```

### Disabled
```tsx
<Checkbox disabled>Disabled</Checkbox>
<Checkbox disabled checked>Disabled Checked</Checkbox>
```

### Checkbox Group
```tsx
const options = ['Apple', 'Pear', 'Orange'];

<Checkbox.Group
  options={options}
  defaultValue={['Apple']}
  onChange={(checkedValues) => console.log(checkedValues)}
/>
```

### Checkbox Group with Options Object
```tsx
const options = [
  { label: 'Apple', value: 'apple' },
  { label: 'Pear', value: 'pear' },
  { label: 'Orange', value: 'orange', disabled: true },
];

<Checkbox.Group options={options} />
```

### Select All (Indeterminate)
```tsx
const allOptions = ['Apple', 'Pear', 'Orange'];
const [checkedList, setCheckedList] = useState(['Apple', 'Pear']);

const checkAll = allOptions.length === checkedList.length;
const indeterminate = checkedList.length > 0 && checkedList.length < allOptions.length;

const onCheckAllChange = (e) => {
  setCheckedList(e.target.checked ? allOptions : []);
};

<>
  <Checkbox
    indeterminate={indeterminate}
    onChange={onCheckAllChange}
    checked={checkAll}
  >
    Check all
  </Checkbox>
  <Divider />
  <Checkbox.Group
    options={allOptions}
    value={checkedList}
    onChange={setCheckedList}
  />
</>
```

### Vertical Group
```tsx
<Checkbox.Group>
  <Space direction="vertical">
    <Checkbox value="A">Option A</Checkbox>
    <Checkbox value="B">Option B</Checkbox>
    <Checkbox value="C">Option C</Checkbox>
  </Space>
</Checkbox.Group>
```

### With Form
```tsx
<Form.Item
  name="agreement"
  valuePropName="checked"
  rules={[{ validator: (_, value) =>
    value ? Promise.resolve() : Promise.reject('Please accept the agreement')
  }]}
>
  <Checkbox>I agree to the terms</Checkbox>
</Form.Item>

<Form.Item name="fruits" label="Fruits">
  <Checkbox.Group options={['Apple', 'Pear', 'Orange']} />
</Form.Item>
```

## Usage Guidelines

1. **Use for multiple selections**: Checkbox allows selecting multiple options.

2. **Use `indeterminate` for "select all"**: Shows partial selection state.

3. **Vertical layout for many options**: Stack checkboxes vertically when list is long.

4. **Use `valuePropName="checked"` with Form**: Required for single checkbox in Form.Item.

5. **Provide clear labels**: Each checkbox should have a descriptive label.
