# Tag

**Purpose**: Categorize or label content with keywords. Tags are used for marking and categorizing.

## When to Use

- Categorization labels
- Status indicators
- Filtering options (as filter chips)
- Keywords or attributes

## Tag Variants

| Variant | Description | Visual Appearance |
|---------|-------------|-------------------|
| **Default** | Basic tag | Light background, border |
| **Bordered** | With visible border | Outlined appearance |
| **Borderless** | No border | Solid background only |
| **Closable** | Can be removed | X button visible |
| **Checkable** | Toggle selection | Changes on click |
| **Colored** | Preset or custom color | Colored background |

## API Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `color` | Tag color | `PresetColors \| string` | - |
| `closable` | Show close button | `boolean` | `false` |
| `closeIcon` | Custom close icon | `ReactNode` | - |
| `onClose` | Close callback | `(e) => void` | - |
| `icon` | Tag icon | `ReactNode` | - |
| `bordered` | Show border | `boolean` | `true` |

## Tag.CheckableTag Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `checked` | Checked state | `boolean` | `false` |
| `onChange` | Change handler | `(checked: boolean) => void` | - |

## Preset Colors

```tsx
// Status colors
'success' | 'processing' | 'error' | 'warning' | 'default'

// Palette colors
'magenta' | 'red' | 'volcano' | 'orange' | 'gold' |
'lime' | 'green' | 'cyan' | 'blue' | 'geekblue' | 'purple'
```

## Design Tokens Used

### Seed Tokens
- `colorPrimary` - Checkable tag when checked
- `fontSize` - Tag text size (fontSizeSM)
- `borderRadius` - Tag corner radius (borderRadiusSM)

### Alias Tokens
- `colorBgContainer` - Default tag background
- `colorBorder` - Default tag border
- `colorText` - Tag text
- `colorSuccessBg`, `colorSuccessBorder` - Success tag
- `colorErrorBg`, `colorErrorBorder` - Error tag
- `colorWarningBg`, `colorWarningBorder` - Warning tag

## Examples

### Basic Tags
```tsx
import { Tag } from 'antd';

<Tag>Default</Tag>
<Tag color="success">Success</Tag>
<Tag color="processing">Processing</Tag>
<Tag color="error">Error</Tag>
<Tag color="warning">Warning</Tag>
```

### Colored Tags
```tsx
// Preset colors
<Tag color="magenta">magenta</Tag>
<Tag color="red">red</Tag>
<Tag color="volcano">volcano</Tag>
<Tag color="orange">orange</Tag>
<Tag color="gold">gold</Tag>
<Tag color="lime">lime</Tag>
<Tag color="green">green</Tag>
<Tag color="cyan">cyan</Tag>
<Tag color="blue">blue</Tag>
<Tag color="geekblue">geekblue</Tag>
<Tag color="purple">purple</Tag>

// Custom color
<Tag color="#f50">#f50</Tag>
<Tag color="#2db7f5">#2db7f5</Tag>
<Tag color="rgb(87, 52, 211)">rgb</Tag>
```

### Closable Tags
```tsx
const [tags, setTags] = useState(['Tag 1', 'Tag 2', 'Tag 3']);

const handleClose = (removedTag) => {
  setTags(tags.filter(tag => tag !== removedTag));
};

{tags.map(tag => (
  <Tag
    key={tag}
    closable
    onClose={() => handleClose(tag)}
  >
    {tag}
  </Tag>
))}
```

### With Icons
```tsx
import { TwitterOutlined, YoutubeOutlined, FacebookOutlined } from '@ant-design/icons';

<Tag icon={<TwitterOutlined />} color="#55acee">Twitter</Tag>
<Tag icon={<YoutubeOutlined />} color="#cd201f">Youtube</Tag>
<Tag icon={<FacebookOutlined />} color="#3b5999">Facebook</Tag>
```

### Borderless
```tsx
<Tag bordered={false}>Borderless</Tag>
<Tag bordered={false} color="success">Success</Tag>
<Tag bordered={false} color="error">Error</Tag>
```

### Checkable Tags (Filter Chips)
```tsx
const [selectedTags, setSelectedTags] = useState(['Books']);

const tagsData = ['Movies', 'Books', 'Music', 'Sports'];

const handleChange = (tag, checked) => {
  const nextSelectedTags = checked
    ? [...selectedTags, tag]
    : selectedTags.filter(t => t !== tag);
  setSelectedTags(nextSelectedTags);
};

{tagsData.map(tag => (
  <Tag.CheckableTag
    key={tag}
    checked={selectedTags.includes(tag)}
    onChange={checked => handleChange(tag, checked)}
  >
    {tag}
  </Tag.CheckableTag>
))}
```

### Editable Tags (Add New)
```tsx
const [tags, setTags] = useState(['Tag 1', 'Tag 2']);
const [inputVisible, setInputVisible] = useState(false);
const [inputValue, setInputValue] = useState('');

const handleInputConfirm = () => {
  if (inputValue && !tags.includes(inputValue)) {
    setTags([...tags, inputValue]);
  }
  setInputVisible(false);
  setInputValue('');
};

{tags.map(tag => (
  <Tag
    key={tag}
    closable
    onClose={() => setTags(tags.filter(t => t !== tag))}
  >
    {tag}
  </Tag>
))}

{inputVisible ? (
  <Input
    size="small"
    style={{ width: 78 }}
    value={inputValue}
    onChange={e => setInputValue(e.target.value)}
    onBlur={handleInputConfirm}
    onPressEnter={handleInputConfirm}
    autoFocus
  />
) : (
  <Tag onClick={() => setInputVisible(true)} style={{ borderStyle: 'dashed' }}>
    <PlusOutlined /> New Tag
  </Tag>
)}
```

### Status Tags
```tsx
<Tag color="success">Approved</Tag>
<Tag color="processing">Pending</Tag>
<Tag color="error">Rejected</Tag>
<Tag color="warning">Review</Tag>
<Tag color="default">Draft</Tag>
```

## Usage Guidelines

1. **Use semantic colors for status**: `success`, `error`, `warning`, `processing`.

2. **Keep tag text short**: 1-2 words maximum.

3. **Use CheckableTag for filters**: Better UX than regular tags for selection.

4. **Consistent styling**: Use same color scheme across your app.

5. **Closable for user-added tags**: Allow removal when tags are user-generated.

6. **Icons for social/brand tags**: Add recognizable icons for platforms.
