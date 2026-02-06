## Icons

Ant Design provides a comprehensive icon library through the `@ant-design/icons` package. All icons are React components that can be imported and used directly.

### Installation

Icons are in a separate package:
```bash
npm install @ant-design/icons
```

### Icon Categories

| Category | Description | Examples |
|----------|-------------|----------|
| **Outlined** | Default style, line icons | `UserOutlined`, `HomeOutlined`, `SettingOutlined` |
| **Filled** | Solid filled icons | `UserFilled`, `HomeFilled`, `SettingFilled` |
| **TwoTone** | Two-color icons | `UserTwoTone`, `HomeTwoTone`, `SettingTwoTone` |

### Import Pattern

```tsx
import {
  UserOutlined,
  SearchOutlined,
  PlusOutlined,
  DeleteOutlined,
  EditOutlined,
  CheckOutlined,
  CloseOutlined,
  LoadingOutlined,
  SettingOutlined,
  MenuOutlined,
} from '@ant-design/icons';
```

### Usage with Components

#### Buttons with Icons
```tsx
import { Button } from 'antd';
import { SearchOutlined, PlusOutlined } from '@ant-design/icons';

<Button type="primary" icon={<SearchOutlined />}>Search</Button>
<Button icon={<PlusOutlined />}>Add Item</Button>

// Icon-only button
<Button type="primary" shape="circle" icon={<SearchOutlined />} />
```

#### Input with Icons
```tsx
import { Input } from 'antd';
import { UserOutlined, LockOutlined } from '@ant-design/icons';

<Input prefix={<UserOutlined />} placeholder="Username" />
<Input.Password prefix={<LockOutlined />} placeholder="Password" />
```

#### Menu with Icons
```tsx
import { Menu } from 'antd';
import { HomeOutlined, SettingOutlined, UserOutlined } from '@ant-design/icons';

const items = [
  { key: 'home', icon: <HomeOutlined />, label: 'Home' },
  { key: 'settings', icon: <SettingOutlined />, label: 'Settings' },
  { key: 'profile', icon: <UserOutlined />, label: 'Profile' },
];

<Menu items={items} />
```

### Icon Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `className` | Class name | `string` | - |
| `style` | Inline styles | `CSSProperties` | - |
| `spin` | Rotate icon with animation | `boolean` | `false` |
| `rotate` | Rotate icon by degrees | `number` | - |
| `twoToneColor` | Color for TwoTone icons | `string` | - |

### Styling Icons

```tsx
// Custom size via font-size
<UserOutlined style={{ fontSize: '24px' }} />

// Custom color
<UserOutlined style={{ color: '#1890ff' }} />

// Spinning animation (for loading states)
<LoadingOutlined spin />

// Rotation
<ArrowUpOutlined rotate={90} />

// Two-tone color
<CheckCircleTwoTone twoToneColor="#52c41a" />
```

### Common Icon Names Reference

#### Navigation
- `HomeOutlined`, `MenuOutlined`, `MenuFoldOutlined`, `MenuUnfoldOutlined`
- `ArrowLeftOutlined`, `ArrowRightOutlined`, `ArrowUpOutlined`, `ArrowDownOutlined`
- `LeftOutlined`, `RightOutlined`, `UpOutlined`, `DownOutlined`

#### Actions
- `PlusOutlined`, `MinusOutlined`, `CloseOutlined`, `CheckOutlined`
- `EditOutlined`, `DeleteOutlined`, `CopyOutlined`, `SaveOutlined`
- `SearchOutlined`, `FilterOutlined`, `SortAscendingOutlined`
- `DownloadOutlined`, `UploadOutlined`, `ShareAltOutlined`
- `SyncOutlined`, `ReloadOutlined`, `UndoOutlined`, `RedoOutlined`

#### Status
- `CheckCircleOutlined`, `CloseCircleOutlined`, `ExclamationCircleOutlined`
- `InfoCircleOutlined`, `QuestionCircleOutlined`, `WarningOutlined`
- `LoadingOutlined` (use with `spin` prop)

#### User & Account
- `UserOutlined`, `TeamOutlined`, `UserAddOutlined`, `UserDeleteOutlined`
- `LockOutlined`, `UnlockOutlined`, `LoginOutlined`, `LogoutOutlined`

#### Communication
- `MailOutlined`, `MessageOutlined`, `CommentOutlined`, `NotificationOutlined`
- `BellOutlined`, `PhoneOutlined`, `SendOutlined`

#### Files & Data
- `FileOutlined`, `FolderOutlined`, `FileAddOutlined`, `FolderAddOutlined`
- `CloudOutlined`, `CloudUploadOutlined`, `CloudDownloadOutlined`
- `DatabaseOutlined`, `TableOutlined`, `BarChartOutlined`

#### Settings & Tools
- `SettingOutlined`, `ToolOutlined`, `ControlOutlined`, `SlidersOutlined`
- `EyeOutlined`, `EyeInvisibleOutlined`

### Best Practices

1. **Consistent style**: Use the same icon style (Outlined, Filled, or TwoTone) throughout your application.

2. **Meaningful icons**: Choose icons that clearly represent their action or meaning.

3. **Accessible labels**: Always provide accessible labels for icon-only buttons:
   ```tsx
   <Button
     type="primary"
     shape="circle"
     icon={<DeleteOutlined />}
     aria-label="Delete item"
   />
   ```

4. **Loading states**: Use `LoadingOutlined` with `spin` for loading indicators:
   ```tsx
   {isLoading ? <LoadingOutlined spin /> : <CheckOutlined />}
   ```

5. **Size consistency**: Match icon sizes to their context (buttons, menus, standalone).
