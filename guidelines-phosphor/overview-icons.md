## Icons - Phosphor Icons Integration

This project uses **Phosphor Icons** instead of the default Ant Design icons. Phosphor is a flexible icon family with 6 weight variants and consistent design language that integrates seamlessly with AntD v6.

### Installation

```bash
npm install @phosphor-icons/react @ant-design/colors
```

### Icon Weights

Phosphor Icons support 6 different weights:

| Weight | Description | Best For |
|--------|-------------|----------|
| `regular` | Default, balanced stroke width | General UI, menus, navigation |
| `bold` | Thicker strokes | Buttons, emphasis, action icons |
| `fill` | Solid filled icons | Status indicators, alerts, badges |
| `thin` | Delicate, light strokes | Subtle decorative elements |
| `light` | Slightly heavier than thin | Secondary UI elements |
| `duotone` | Two-tone with opacity layers | Decorative, marketing sections |

### AntD Integration Pattern

To use Phosphor icons with AntD components, wrap them using the `createPhosphorIcon` utility:

```tsx
// createPhosphorIcon.tsx
import { useMemo, type CSSProperties } from 'react';
import Icon from '@ant-design/icons';
import type { CustomIconComponentProps } from '@ant-design/icons/lib/components/Icon';
import type { Icon as PhosphorIconType, IconWeight } from '@phosphor-icons/react';

interface PhosphorAntIconProps {
  weight?: IconWeight;
  color?: string;
  size?: string | number;
  style?: CSSProperties;
  className?: string;
}

export function createPhosphorIcon(PhosphorComponent: PhosphorIconType) {
  const Created = (props: PhosphorAntIconProps) => {
    const { weight = 'regular', color, size, style, className } = props;

    const BridgeSvg = useMemo(
      () =>
        Object.assign(
          (svgProps: CustomIconComponentProps) => (
            <PhosphorComponent
              weight={weight}
              color={color}
              size={size ?? svgProps.width}
              style={{ display: 'block' }}
            />
          ),
          { displayName: `Bridge(${PhosphorComponent.displayName ?? 'Phosphor'})` },
        ),
      [weight, color, size],
    );

    return (
      <Icon
        component={BridgeSvg as any}
        style={style}
        className={className}
      />
    );
  };

  Created.displayName = `PhosphorAntIcon(${PhosphorComponent.displayName ?? 'Phosphor'})`;
  return Created;
}
```

### Creating Icon Exports

Create a central icons file with all your wrapped icons:

```tsx
// icons.ts
import {
  Envelope,
  Gear,
  MagnifyingGlass,
  Check,
  X,
  CaretLeft,
  CaretRight,
  CaretDown,
  Trash,
  CheckCircle,
  XCircle,
  Clock,
  UploadSimple,
  Paperclip,
  Image as ImageIcon,
  Warning,
  WarningCircle,
  Circle,
  User,
  House,
  Plus,
  Minus,
  ArrowLeft,
  ArrowRight,
  Bell,
  ChatCircle,
  File,
  Folder,
  Eye,
  EyeSlash,
  Lock,
  SignOut,
  Copy,
  Download,
  Share,
  Funnel,
  SortAscending,
} from '@phosphor-icons/react';
import { createPhosphorIcon } from './createPhosphorIcon';

// Navigation
export const EnvelopeIcon = createPhosphorIcon(Envelope);
export const HouseIcon = createPhosphorIcon(House);
export const GearIcon = createPhosphorIcon(Gear);
export const BellIcon = createPhosphorIcon(Bell);

// Actions
export const SearchIcon = createPhosphorIcon(MagnifyingGlass);
export const PlusIcon = createPhosphorIcon(Plus);
export const MinusIcon = createPhosphorIcon(Minus);
export const TrashIcon = createPhosphorIcon(Trash);
export const CopyIcon = createPhosphorIcon(Copy);
export const DownloadIcon = createPhosphorIcon(Download);
export const ShareIcon = createPhosphorIcon(Share);
export const UploadIcon = createPhosphorIcon(UploadSimple);
export const FilterIcon = createPhosphorIcon(Funnel);
export const SortIcon = createPhosphorIcon(SortAscending);

// Status
export const CheckIcon = createPhosphorIcon(Check);
export const XIcon = createPhosphorIcon(X);
export const CheckCircleIcon = createPhosphorIcon(CheckCircle);
export const XCircleIcon = createPhosphorIcon(XCircle);
export const WarningIcon = createPhosphorIcon(Warning);
export const WarningCircleIcon = createPhosphorIcon(WarningCircle);
export const ClockIcon = createPhosphorIcon(Clock);
export const CircleIcon = createPhosphorIcon(Circle);

// Arrows & Carets
export const CaretLeftIcon = createPhosphorIcon(CaretLeft);
export const CaretRightIcon = createPhosphorIcon(CaretRight);
export const CaretDownIcon = createPhosphorIcon(CaretDown);
export const ArrowLeftIcon = createPhosphorIcon(ArrowLeft);
export const ArrowRightIcon = createPhosphorIcon(ArrowRight);

// User & Account
export const UserIcon = createPhosphorIcon(User);
export const LockIcon = createPhosphorIcon(Lock);
export const SignOutIcon = createPhosphorIcon(SignOut);

// Communication
export const ChatIcon = createPhosphorIcon(ChatCircle);

// Files
export const FileIcon = createPhosphorIcon(File);
export const FolderIcon = createPhosphorIcon(Folder);
export const ImageIconAnt = createPhosphorIcon(ImageIcon);
export const PaperclipIcon = createPhosphorIcon(Paperclip);

// Visibility
export const EyeIcon = createPhosphorIcon(Eye);
export const EyeSlashIcon = createPhosphorIcon(EyeSlash);
```

### AntD Icon to Phosphor Mapping

| AntD Icon | Phosphor Icon | Import Name |
|-----------|---------------|-------------|
| `SearchOutlined` | `MagnifyingGlass` | `SearchIcon` |
| `UserOutlined` | `User` | `UserIcon` |
| `HomeOutlined` | `House` | `HouseIcon` |
| `SettingOutlined` | `Gear` | `GearIcon` |
| `MailOutlined` | `Envelope` | `EnvelopeIcon` |
| `CheckOutlined` | `Check` | `CheckIcon` |
| `CloseOutlined` | `X` | `XIcon` |
| `PlusOutlined` | `Plus` | `PlusIcon` |
| `MinusOutlined` | `Minus` | `MinusIcon` |
| `DeleteOutlined` | `Trash` | `TrashIcon` |
| `EditOutlined` | `PencilSimple` | `EditIcon` |
| `CopyOutlined` | `Copy` | `CopyIcon` |
| `DownloadOutlined` | `Download` | `DownloadIcon` |
| `UploadOutlined` | `UploadSimple` | `UploadIcon` |
| `CheckCircleOutlined` | `CheckCircle` | `CheckCircleIcon` |
| `CloseCircleOutlined` | `XCircle` | `XCircleIcon` |
| `ExclamationCircleOutlined` | `WarningCircle` | `WarningCircleIcon` |
| `WarningOutlined` | `Warning` | `WarningIcon` |
| `InfoCircleOutlined` | `Info` | `InfoIcon` |
| `QuestionCircleOutlined` | `Question` | `QuestionIcon` |
| `LeftOutlined` | `CaretLeft` | `CaretLeftIcon` |
| `RightOutlined` | `CaretRight` | `CaretRightIcon` |
| `DownOutlined` | `CaretDown` | `CaretDownIcon` |
| `UpOutlined` | `CaretUp` | `CaretUpIcon` |
| `ArrowLeftOutlined` | `ArrowLeft` | `ArrowLeftIcon` |
| `ArrowRightOutlined` | `ArrowRight` | `ArrowRightIcon` |
| `LockOutlined` | `Lock` | `LockIcon` |
| `EyeOutlined` | `Eye` | `EyeIcon` |
| `EyeInvisibleOutlined` | `EyeSlash` | `EyeSlashIcon` |
| `BellOutlined` | `Bell` | `BellIcon` |
| `FileOutlined` | `File` | `FileIcon` |
| `FolderOutlined` | `Folder` | `FolderIcon` |
| `FilterOutlined` | `Funnel` | `FilterIcon` |
| `ClockCircleOutlined` | `Clock` | `ClockIcon` |
| `LoadingOutlined` | `SpinnerGap` | `SpinnerIcon` (use with CSS animation) |

### Usage with AntD Components

#### Buttons with Icons
```tsx
import { Button } from 'antd';
import { SearchIcon, PlusIcon } from './icons';

<Button type="primary" icon={<SearchIcon weight="bold" />}>Search</Button>
<Button icon={<PlusIcon weight="bold" />}>Add Item</Button>

// Icon-only button
<Button type="primary" shape="circle" icon={<SearchIcon weight="bold" />} />
```

#### Input with Icons
```tsx
import { Input } from 'antd';
import { UserIcon, LockIcon, CheckCircleIcon } from './icons';
import { theme } from 'antd';

const { token } = theme.useToken();

<Input prefix={<UserIcon weight="regular" />} placeholder="Username" />
<Input.Password prefix={<LockIcon weight="regular" />} placeholder="Password" />
<Input
  defaultValue="Valid content"
  suffix={<CheckCircleIcon color={token.colorSuccess} weight="fill" />}
/>
```

#### Menu with Icons
```tsx
import { Menu } from 'antd';
import { HouseIcon, GearIcon, UserIcon } from './icons';

const items = [
  { key: 'home', icon: <HouseIcon weight="regular" />, label: 'Home' },
  { key: 'settings', icon: <GearIcon weight="regular" />, label: 'Settings' },
  { key: 'profile', icon: <UserIcon weight="regular" />, label: 'Profile' },
];

<Menu items={items} />
```

#### Select with Custom Icons
```tsx
import { Select } from 'antd';
import { CaretDownIcon, XIcon, CheckIcon, XCircleIcon } from './icons';

<Select
  mode="multiple"
  options={[
    { value: 'a', label: 'Option A' },
    { value: 'b', label: 'Option B' },
  ]}
  suffixIcon={<CaretDownIcon weight="bold" />}
  removeIcon={<XIcon size={12} weight="bold" />}
  menuItemSelectedIcon={<CheckIcon weight="bold" />}
  allowClear={{ clearIcon: <XCircleIcon weight="fill" /> }}
/>
```

#### Alert with Icons
```tsx
import { Alert, theme } from 'antd';
import { CheckCircleIcon, XCircleIcon, WarningCircleIcon } from './icons';

const { token } = theme.useToken();

<Alert
  message="Success Tips"
  type="success"
  showIcon
  icon={<CheckCircleIcon size={20} weight="fill" />}
/>

<Alert
  message="Error"
  description="Error description."
  type="error"
  showIcon
  icon={<XCircleIcon size={24} weight="fill" />}
/>

<Alert
  message="Warning"
  type="warning"
  showIcon
  icon={<WarningCircleIcon size={20} weight="fill" />}
/>
```

#### Pagination with Custom Icons
```tsx
import { Pagination, Button } from 'antd';
import { CaretLeftIcon, CaretRightIcon } from './icons';

const itemRender = (_page: number, type: string, originalElement: React.ReactNode) => {
  if (type === 'prev')
    return <Button type="text" size="small" icon={<CaretLeftIcon weight="bold" />} />;
  if (type === 'next')
    return <Button type="text" size="small" icon={<CaretRightIcon weight="bold" />} />;
  return originalElement;
};

<Pagination defaultCurrent={1} total={50} itemRender={itemRender} />
```

#### Steps with Icons
```tsx
import { Steps } from 'antd';
import { CheckIcon, CircleIcon } from './icons';

<Steps
  current={1}
  items={[
    { title: 'Finished', icon: <CheckIcon weight="bold" /> },
    { title: 'In Progress' },
    { title: 'Waiting', icon: <CircleIcon weight="bold" /> },
  ]}
/>
```

#### Tag with Close Icon
```tsx
import { Tag } from 'antd';
import { XIcon } from './icons';

<Tag closeIcon={<XIcon size={12} weight="bold" />}>
  Closable Tag
</Tag>
```

#### Message and Notification
```tsx
import { App, theme } from 'antd';
import { CheckCircleIcon, XCircleIcon, WarningCircleIcon } from './icons';

const { message, notification } = App.useApp();
const { token } = theme.useToken();

// Message
message.open({
  type: 'success',
  content: 'Operation successful',
  icon: <CheckCircleIcon color={token.colorSuccess} size={20} weight="fill" />,
});

// Notification
notification.open({
  message: 'Notification Title',
  description: 'This is the content of the notification.',
  icon: <CheckCircleIcon color={token.colorSuccess} size={24} weight="fill" />,
});
```

#### Result with Icon
```tsx
import { Result, theme } from 'antd';
import { CheckCircleIcon, XCircleIcon, WarningIcon } from './icons';

const { token } = theme.useToken();

<Result
  status="success"
  icon={<CheckCircleIcon color={token.colorSuccess} size={72} weight="fill" />}
  title="Successfully Purchased!"
  subTitle="Order number: 2017182818828182881"
/>
```

### Icon Props Reference

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `weight` | Icon weight variant | `'regular' \| 'bold' \| 'fill' \| 'thin' \| 'light' \| 'duotone'` | `'regular'` |
| `color` | Icon color | `string` | inherits from parent |
| `size` | Icon size in pixels | `string \| number` | inherits from AntD context |
| `style` | Inline styles | `CSSProperties` | - |
| `className` | Class name | `string` | - |

### Weight Guidelines by Context

| Context | Recommended Weight | Rationale |
|---------|-------------------|-----------|
| Menu items | `regular` | Clean, readable navigation |
| Buttons | `bold` | Better visibility, emphasis |
| Status indicators (success/error/warning) | `fill` | Strong visual feedback |
| Input prefixes/suffixes | `regular` | Subtle, non-distracting |
| Alerts | `fill` | Clear status communication |
| Steps (completed) | `bold` | Emphasis on completion |
| Tags close button | `bold` | Clear interaction affordance |
| Pagination arrows | `bold` | Clear navigation |

### Best Practices

1. **Consistent weights**: Use the same weight across similar UI elements. `regular` for navigation, `bold` for actions, `fill` for status.

2. **Use design tokens for colors**: Always use AntD design tokens for semantic colors:
   ```tsx
   const { token } = theme.useToken();
   <CheckCircleIcon color={token.colorSuccess} weight="fill" />
   <XCircleIcon color={token.colorError} weight="fill" />
   <WarningCircleIcon color={token.colorWarning} weight="fill" />
   ```

3. **Size appropriately**: Match icon size to context:
   - Buttons: inherit from button (no size prop needed)
   - Small alerts: `size={20}`
   - Large alerts with description: `size={24}`
   - Result pages: `size={72}`
   - Tag close icons: `size={12}`

4. **Accessible labels**: Always provide accessible labels for icon-only buttons:
   ```tsx
   <Button
     type="primary"
     shape="circle"
     icon={<TrashIcon weight="bold" />}
     aria-label="Delete item"
   />
   ```

5. **Loading states**: For loading, use `SpinnerGap` with CSS animation:
   ```tsx
   import { SpinnerGap } from '@phosphor-icons/react';

   const SpinnerIcon = createPhosphorIcon(SpinnerGap);

   <SpinnerIcon weight="bold" className="animate-spin" />
   ```

   Or use AntD's `Spin` component for consistent loading UI.

### Phosphor Icon Explorer

Browse all available Phosphor icons at: https://phosphoricons.com/

The library includes 1,200+ icons across categories:
- Arrows & Navigation
- Commerce & Finance
- Communication
- Design & Development
- Files & Folders
- Health & Wellbeing
- Maps & Travel
- Media & Devices
- Nature & Weather
- Objects & Tools
- People & Body
- System & UI
