## Components

Always prefer components from the Ant Design package (imported from `antd`) if they are available. Each component has a guidelines file that contains helpful examples and additional context. You must follow all relevant instructions.

### Component Categories

| Category | Components | Description |
|----------|------------|-------------|
| **General** | Button, Icon, Typography | Basic building blocks |
| **Layout** | Divider, Grid, Layout, Space, Splitter, Flex | Page structure and spacing |
| **Navigation** | Anchor, Breadcrumb, Dropdown, Menu, Pagination, Steps | User navigation |
| **Data Entry** | AutoComplete, Cascader, Checkbox, ColorPicker, DatePicker, Form, Input, InputNumber, Mentions, Radio, Rate, Select, Slider, Switch, TimePicker, Transfer, TreeSelect, Upload | Form inputs and controls |
| **Data Display** | Avatar, Badge, Calendar, Card, Carousel, Collapse, Descriptions, Empty, Image, List, Popover, QRCode, Segmented, Statistic, Table, Tabs, Tag, Timeline, Tooltip, Tour, Tree | Display data to users |
| **Feedback** | Alert, Drawer, Message, Modal, Notification, Popconfirm, Progress, Result, Skeleton, Spin | User feedback and status |

### Guidelines Files

| Component | Purpose | Guidelines File |
|-----------|---------|-----------------|
| Button | Trigger operations and actions | [button.md](components/button.md) |
| Input | Text input for forms | [input.md](components/input.md) |
| Select | Dropdown selection | [select.md](components/select.md) |
| Table | Display tabular data with sorting/filtering | [table.md](components/table.md) |
| Modal | Dialog overlays | [modal.md](components/modal.md) |
| Form | Form layout and validation | [form.md](components/form.md) |
| Card | Content containers | [card.md](components/card.md) |
| Tabs | Organize content into panels | [tabs.md](components/tabs.md) |
| Menu | Navigation menus | [menu.md](components/menu.md) |
| Checkbox | Multiple selection | [checkbox.md](components/checkbox.md) |
| Radio | Single selection | [radio.md](components/radio.md) |
| Switch | Toggle between states | [switch.md](components/switch.md) |
| DatePicker | Date selection | [datepicker.md](components/datepicker.md) |
| Upload | File uploads | [upload.md](components/upload.md) |
| Message | Global feedback messages | [message.md](components/message.md) |
| Notification | System notifications | [notification.md](components/notification.md) |
| Drawer | Side panel overlay | [drawer.md](components/drawer.md) |
| Popconfirm | Confirmation popover | [popconfirm.md](components/popconfirm.md) |
| Tooltip | Hover hints | [tooltip.md](components/tooltip.md) |
| Tag | Categorization labels | [tag.md](components/tag.md) |
| Badge | Status indicators | [badge.md](components/badge.md) |
| Avatar | User representation | [avatar.md](components/avatar.md) |
| Progress | Progress indicators | [progress.md](components/progress.md) |
| Spin | Loading indicator | [spin.md](components/spin.md) |
| Alert | Alert messages | [alert.md](components/alert.md) |
| Empty | Empty state placeholder | [empty.md](components/empty.md) |
| Result | Operation result feedback | [result.md](components/result.md) |

## General Component Usage Best Practices

### Import Pattern
```tsx
import { Button, Input, Form, Table } from 'antd';
```

### Controlled vs Uncontrolled
- **Controlled**: Component receives `value` and `onChange` props, parent manages state
- **Uncontrolled**: Component manages own state, use `defaultValue` for initial value
- Prefer controlled for most cases in modern React

### Sizing
Most components support a `size` prop with these values:
- `"small"` - Compact size for dense UIs
- `"middle"` - Default size (can be omitted)
- `"large"` - Larger size for emphasis

### Status States
Many form components support a `status` prop:
- `"error"` - Red styling for validation errors
- `"warning"` - Yellow styling for warnings

### Disabled State
All interactive components support a `disabled` prop:
```tsx
<Button disabled>Cannot Click</Button>
<Input disabled placeholder="Cannot type" />
```

### Loading State
Components that trigger actions support a `loading` prop:
```tsx
<Button loading>Submitting...</Button>
<Select loading options={[]} />
```

## Theming with ConfigProvider

Wrap your application with ConfigProvider to apply a custom theme:

```tsx
import { ConfigProvider } from 'antd';

const App = () => (
  <ConfigProvider
    theme={{
      token: {
        colorPrimary: '#1890ff',
        borderRadius: 6,
      },
    }}
  >
    <YourApp />
  </ConfigProvider>
);
```
