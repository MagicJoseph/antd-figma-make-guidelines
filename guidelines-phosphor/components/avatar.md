# Avatar

**Purpose**: Represent a user or entity. Avatars display images, icons, or letters to identify users.

## When to Use

- User profile pictures
- User lists and mentions
- Comments and activity feeds
- Identification in any user-related context

## Avatar Variants

| Variant | Description | Visual Appearance |
|---------|-------------|-------------------|
| **Image** | Photo/picture | Circular/square image |
| **Icon** | Icon representation | Icon in colored circle |
| **Letter** | Initial(s) | Letter(s) in colored circle |

## API Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `src` | Image URL | `string` | - |
| `srcSet` | Responsive image sources | `string` | - |
| `alt` | Alt text for image | `string` | - |
| `icon` | Icon to display | `ReactNode` | - |
| `shape` | Avatar shape | `'circle' \| 'square'` | `'circle'` |
| `size` | Avatar size | `number \| 'large' \| 'small' \| 'default' \| { xs, sm, md, lg, xl, xxl }` | `'default'` |
| `gap` | Letter spacing from sides | `number` | `4` |
| `draggable` | Allow drag | `boolean` | - |
| `onError` | Image load error handler | `() => boolean` | - |

## Avatar.Group Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `maxCount` | Max avatars to show | `number` | - |
| `maxPopoverPlacement` | Overflow popover position | `'top' \| 'bottom'` | `'top'` |
| `maxPopoverTrigger` | Overflow trigger | `'hover' \| 'focus' \| 'click'` | `'hover'` |
| `maxStyle` | Overflow avatar style | `CSSProperties` | - |
| `size` | Group avatar size | Same as Avatar | `'default'` |
| `shape` | Group avatar shape | `'circle' \| 'square'` | `'circle'` |

## Design Tokens Used

### Seed Tokens
- `colorPrimary` - Default background color
- `fontSize` - Letter text size

### Alias Tokens
- `colorBgContainer` - Background when no color set
- `colorTextLightSolid` - Letter/icon color on colored background

## Examples

### Basic Avatar
```tsx
import { Avatar } from 'antd';
import { UserIcon } from './icons';

// Image
<Avatar src="https://example.com/avatar.jpg" />

// Icon
<Avatar icon={<UserIcon weight="regular" />} />

// Letter
<Avatar>U</Avatar>
<Avatar>USER</Avatar>
```

### Shapes
```tsx
import { UserIcon } from './icons';

<Avatar shape="circle" icon={<UserIcon weight="regular" />} />
<Avatar shape="square" icon={<UserIcon weight="regular" />} />
```

### Sizes
```tsx
import { UserIcon } from './icons';

<Avatar size={64} icon={<UserIcon weight="regular" />} />
<Avatar size="large" icon={<UserIcon weight="regular" />} />
<Avatar icon={<UserIcon weight="regular" />} />
<Avatar size="small" icon={<UserIcon weight="regular" />} />

// Responsive size
<Avatar
  size={{ xs: 24, sm: 32, md: 40, lg: 64, xl: 80, xxl: 100 }}
  icon={<UserIcon weight="regular" />}
/>
```

### With Badge
```tsx
import { Avatar, Badge } from 'antd';
import { UserIcon } from './icons';

<Badge count={5}>
  <Avatar shape="square" icon={<UserIcon weight="regular" />} />
</Badge>

<Badge dot>
  <Avatar shape="square" icon={<UserOutlined />} />
</Badge>

// Online status
<Badge status="success" dot offset={[-5, 40]}>
  <Avatar src="avatar.jpg" />
</Badge>
```

### Avatar Group
```tsx
<Avatar.Group>
  <Avatar src="user1.jpg" />
  <Avatar style={{ backgroundColor: '#f56a00' }}>K</Avatar>
  <Avatar style={{ backgroundColor: '#87d068' }} icon={<UserOutlined />} />
  <Avatar style={{ backgroundColor: '#1890ff' }}>U</Avatar>
</Avatar.Group>
```

### Avatar Group with Max Count
```tsx
<Avatar.Group
  maxCount={3}
  maxStyle={{ color: '#f56a00', backgroundColor: '#fde3cf' }}
>
  <Avatar src="user1.jpg" />
  <Avatar src="user2.jpg" />
  <Avatar src="user3.jpg" />
  <Avatar src="user4.jpg" />
  <Avatar src="user5.jpg" />
</Avatar.Group>
```

### Colored Avatars
```tsx
<Avatar style={{ backgroundColor: '#f56a00' }}>U</Avatar>
<Avatar style={{ backgroundColor: '#7265e6' }}>S</Avatar>
<Avatar style={{ backgroundColor: '#ffbf00' }}>A</Avatar>
<Avatar style={{ backgroundColor: '#00a2ae' }}>M</Avatar>
```

### Fallback on Error
```tsx
<Avatar
  src="broken-image.jpg"
  onError={() => {
    // Return false to show fallback
    return false;
  }}
>
  U
</Avatar>

// Or with icon fallback
<Avatar
  src="broken-image.jpg"
  icon={<UserOutlined />}
/>
```

### In Lists
```tsx
import { List, Avatar } from 'antd';

<List
  itemLayout="horizontal"
  dataSource={users}
  renderItem={user => (
    <List.Item>
      <List.Item.Meta
        avatar={<Avatar src={user.avatar} />}
        title={user.name}
        description={user.email}
      />
    </List.Item>
  )}
/>
```

### With Tooltip
```tsx
import { Avatar, Tooltip } from 'antd';

<Avatar.Group>
  <Tooltip title="User 1" placement="top">
    <Avatar src="user1.jpg" />
  </Tooltip>
  <Tooltip title="User 2" placement="top">
    <Avatar src="user2.jpg" />
  </Tooltip>
</Avatar.Group>
```

### Letter Auto-Scale
```tsx
// Long text auto-scales to fit
<Avatar size={40}>User</Avatar>
<Avatar size={40}>AB</Avatar>

// Adjust gap from edges
<Avatar gap={2}>User</Avatar>
```

## Usage Guidelines

1. **Fallback hierarchy**: Image → Icon → Letter(s).

2. **Consistent sizing**: Use same size for avatars in a group or list.

3. **Use Avatar.Group for multiple**: Shows overlap effect and handles overflow.

4. **Badge for status**: Combine with Badge for online/notification status.

5. **Alt text for accessibility**: Always provide `alt` for image avatars.

6. **Letter avatars**: Use 1-2 characters (initials) for letter avatars.

7. **Color for letter avatars**: Assign consistent colors based on user ID/name.
