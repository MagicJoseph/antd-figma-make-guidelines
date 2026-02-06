# DatePicker

**Purpose**: Select dates, date ranges, or date-time values from a calendar interface.

## When to Use

- Selecting a single date
- Selecting a date range (start/end)
- Selecting date and time
- Selecting week, month, quarter, or year

## DatePicker Variants

| Variant | Description | Use Case |
|---------|-------------|----------|
| **DatePicker** | Single date | Birthdates, single events |
| **RangePicker** | Date range | Booking periods, reports |
| **WeekPicker** | Week selection | Weekly reports |
| **MonthPicker** | Month selection | Monthly reports |
| **QuarterPicker** | Quarter selection | Quarterly reviews |
| **YearPicker** | Year selection | Annual data |

## API Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `value` | Selected date (controlled) | `Dayjs` | - |
| `defaultValue` | Initial date | `Dayjs` | - |
| `onChange` | Change handler | `(date, dateString) => void` | - |
| `picker` | Picker type | `'date' \| 'week' \| 'month' \| 'quarter' \| 'year'` | `'date'` |
| `showTime` | Enable time selection | `boolean \| object` | `false` |
| `format` | Display format | `string \| string[]` | `'YYYY-MM-DD'` |
| `disabled` | Disabled state | `boolean` | `false` |
| `disabledDate` | Disable specific dates | `(currentDate) => boolean` | - |
| `allowClear` | Show clear button | `boolean` | `true` |
| `placeholder` | Placeholder text | `string \| [string, string]` | - |
| `status` | Validation status | `'error' \| 'warning'` | - |
| `size` | Input size | `'large' \| 'middle' \| 'small'` | `'middle'` |
| `variant` | Input variant (v6) | `'outlined' \| 'borderless' \| 'filled'` | `'outlined'` |
| `open` | Dropdown open state | `boolean` | - |
| `placement` | Dropdown placement | `'bottomLeft' \| 'bottomRight' \| 'topLeft' \| 'topRight'` | `'bottomLeft'` |
| `presets` | Preset date ranges | `{ label, value }[]` | - |
| `cellRender` | Custom cell render | `(current, info) => ReactNode` | - |
| `minDate` | Minimum selectable date | `Dayjs` | - |
| `maxDate` | Maximum selectable date | `Dayjs` | - |

## RangePicker Additional Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `value` | Selected range | `[Dayjs, Dayjs]` | - |
| `defaultValue` | Initial range | `[Dayjs, Dayjs]` | - |
| `separator` | Range separator | `ReactNode` | `~` |

> **v6 Migration Note**: `bordered` prop is deprecated. Use `variant="borderless"` instead. Props `popupClassName` and `dropdownClassName` are deprecated - use `classNames.popup.root` instead.

## Design Tokens Used

### Seed Tokens
- `colorPrimary` - Selected date, today highlight
- `borderRadius` - Input and dropdown radius

### Alias Tokens
- `colorBgContainer` - Input background
- `colorBgElevated` - Dropdown background
- `colorBorder` - Input border
- `colorText` - Date text
- `colorTextDisabled` - Disabled date text
- `colorPrimaryBg` - Selected date background
- `controlHeight` - Input height

## Examples

### Basic DatePicker
```tsx
import { DatePicker } from 'antd';
import dayjs from 'dayjs';

<DatePicker onChange={(date, dateString) => console.log(date, dateString)} />

// Controlled
const [date, setDate] = useState(null);
<DatePicker value={date} onChange={setDate} />
```

### With Default Value
```tsx
<DatePicker defaultValue={dayjs('2024-01-01')} />
```

### Date Range Picker
```tsx
const { RangePicker } = DatePicker;

<RangePicker
  onChange={(dates, dateStrings) => {
    console.log('From:', dateStrings[0], 'To:', dateStrings[1]);
  }}
/>
```

### Date and Time
```tsx
<DatePicker showTime />

<DatePicker
  showTime={{ format: 'HH:mm' }}
  format="YYYY-MM-DD HH:mm"
/>

<RangePicker showTime />
```

### Different Pickers
```tsx
<DatePicker picker="week" />
<DatePicker picker="month" />
<DatePicker picker="quarter" />
<DatePicker picker="year" />
```

### Custom Format
```tsx
<DatePicker format="DD/MM/YYYY" />
<DatePicker format="MMMM D, YYYY" />

// Multiple formats for input
<DatePicker format={['DD/MM/YYYY', 'DD-MM-YYYY', 'DDMMYYYY']} />
```

### Disabled Dates
```tsx
// Disable past dates
<DatePicker
  disabledDate={(current) => current && current < dayjs().startOf('day')}
/>

// Disable future dates
<DatePicker
  disabledDate={(current) => current && current > dayjs().endOf('day')}
/>

// Disable specific days (weekends)
<DatePicker
  disabledDate={(current) => {
    const day = current.day();
    return day === 0 || day === 6;
  }}
/>

// Using minDate/maxDate (v5.14.0+)
<DatePicker
  minDate={dayjs('2024-01-01')}
  maxDate={dayjs('2024-12-31')}
/>
```

### Presets
```tsx
<RangePicker
  presets={[
    { label: 'Last 7 Days', value: [dayjs().subtract(7, 'day'), dayjs()] },
    { label: 'Last 30 Days', value: [dayjs().subtract(30, 'day'), dayjs()] },
    { label: 'This Month', value: [dayjs().startOf('month'), dayjs().endOf('month')] },
  ]}
/>
```

### Sizes
```tsx
<DatePicker size="large" />
<DatePicker size="middle" />
<DatePicker size="small" />
```

### Status
```tsx
<DatePicker status="error" />
<DatePicker status="warning" />
```

### With Form
```tsx
<Form.Item
  name="birthday"
  label="Birthday"
  rules={[{ required: true, message: 'Please select your birthday' }]}
>
  <DatePicker style={{ width: '100%' }} />
</Form.Item>

<Form.Item name="dateRange" label="Period">
  <RangePicker style={{ width: '100%' }} />
</Form.Item>
```

### Disabled
```tsx
<DatePicker disabled />
<RangePicker disabled />
```

## Usage Guidelines

1. **Use appropriate picker**: Choose picker type based on required precision.

2. **Provide clear placeholder**: Help users understand expected format.

3. **Use presets for common ranges**: Save users time with preset options.

4. **Disable invalid dates**: Prevent selection of impossible dates.

5. **Full width in forms**: Use `style={{ width: '100%' }}` in form layouts.

6. **Use dayjs for manipulation**: AntD v5+ uses dayjs instead of moment.
