# Typography Design Tokens

## Font Scale System

Ant Design uses a modular scale based on a 14px base font size. The scale follows natural proportions for clear visual hierarchy.

## Font Family Tokens

| Token | Value | Usage |
|-------|-------|-------|
| `fontFamily` | `-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif` | Default UI font |
| `fontFamilyCode` | `'SFMono-Regular', Consolas, 'Liberation Mono', Menlo, Courier, monospace` | Code and monospace text |

## Font Size Tokens

| Token | Default Value | Usage |
|-------|--------------|-------|
| `fontSize` | 14px | Base/default text |
| `fontSizeSM` | 12px | Small text, captions |
| `fontSizeLG` | 16px | Large text, emphasis |
| `fontSizeXL` | 20px | Extra large text |
| `fontSizeHeading1` | 38px | H1 headings |
| `fontSizeHeading2` | 30px | H2 headings |
| `fontSizeHeading3` | 24px | H3 headings |
| `fontSizeHeading4` | 20px | H4 headings |
| `fontSizeHeading5` | 16px | H5 headings |

## Line Height Tokens

| Token | Default Value | Usage |
|-------|--------------|-------|
| `lineHeight` | 1.5714 | Default line height |
| `lineHeightSM` | 1.6667 | Small text |
| `lineHeightLG` | 1.5 | Large text |
| `lineHeightHeading1` | 1.2105 | H1 |
| `lineHeightHeading2` | 1.2667 | H2 |
| `lineHeightHeading3` | 1.3333 | H3 |
| `lineHeightHeading4` | 1.4 | H4 |
| `lineHeightHeading5` | 1.5 | H5 |

## Font Weight Tokens

| Token | Value | Usage |
|-------|-------|-------|
| `fontWeightStrong` | 600 | Bold/strong text, headings |

## Typography Component

AntD provides a Typography component for consistent text styling:

```tsx
import { Typography } from 'antd';

const { Title, Text, Paragraph, Link } = Typography;

// Headings
<Title>h1. Ant Design</Title>
<Title level={2}>h2. Ant Design</Title>
<Title level={3}>h3. Ant Design</Title>
<Title level={4}>h4. Ant Design</Title>
<Title level={5}>h5. Ant Design</Title>

// Text variants
<Text>Default text</Text>
<Text type="secondary">Secondary text</Text>
<Text type="success">Success text</Text>
<Text type="warning">Warning text</Text>
<Text type="danger">Danger text</Text>
<Text disabled>Disabled text</Text>
<Text strong>Bold text</Text>
<Text italic>Italic text</Text>
<Text underline>Underlined text</Text>
<Text delete>Strikethrough text</Text>
<Text code>Code text</Text>
<Text keyboard>Keyboard text</Text>
<Text mark>Highlighted text</Text>

// Paragraph
<Paragraph>
  A paragraph of text with proper spacing.
</Paragraph>

// Links
<Link href="https://ant.design">Link text</Link>
```

## Using Typography Tokens Directly

```tsx
import { theme } from 'antd';

const { useToken } = theme;

const CustomText = () => {
  const { token } = useToken();

  return (
    <div>
      <h1
        style={{
          fontSize: token.fontSizeHeading1,
          lineHeight: token.lineHeightHeading1,
          fontWeight: token.fontWeightStrong,
          color: token.colorTextHeading,
        }}
      >
        Main Heading
      </h1>

      <p
        style={{
          fontSize: token.fontSize,
          lineHeight: token.lineHeight,
          color: token.colorText,
        }}
      >
        Body text using default tokens.
      </p>

      <span
        style={{
          fontSize: token.fontSizeSM,
          lineHeight: token.lineHeightSM,
          color: token.colorTextSecondary,
        }}
      >
        Small secondary text
      </span>
    </div>
  );
};
```

## Typography Guidelines

### Hierarchy
- Use heading sizes to establish clear visual hierarchy
- H1 for page titles (use sparingly, typically once per page)
- H2-H4 for section headings
- Default text for body content
- Small text for captions, metadata, helper text

### Readability
- Prefer `fontSize` (14px) for body text - optimized for UI density
- Use `fontSizeLG` (16px) for longer-form content
- Avoid using `fontSizeSM` (12px) for anything except captions and metadata

### Text Colors
- `colorText` - Primary content
- `colorTextSecondary` - Descriptions, less important info
- `colorTextTertiary` - Placeholder text, hints
- `colorTextDisabled` - Disabled states

### Customizing Font Size Scale

```tsx
<ConfigProvider
  theme={{
    token: {
      fontSize: 14,        // Base size
      fontSizeSM: 12,      // Small
      fontSizeLG: 16,      // Large
      fontSizeXL: 20,      // Extra large
      fontSizeHeading1: 38,
      fontSizeHeading2: 30,
      fontSizeHeading3: 24,
      fontSizeHeading4: 20,
      fontSizeHeading5: 16,
    },
  }}
>
  <App />
</ConfigProvider>
```

## Text Truncation

Typography component supports automatic truncation:

```tsx
// Single line ellipsis
<Paragraph ellipsis>
  Very long text that will be truncated with ellipsis...
</Paragraph>

// Multi-line ellipsis (3 lines)
<Paragraph ellipsis={{ rows: 3 }}>
  Very long text that spans multiple lines...
</Paragraph>

// Expandable
<Paragraph ellipsis={{ rows: 2, expandable: true, symbol: 'more' }}>
  Expandable text content...
</Paragraph>
```

## Copyable Text

```tsx
<Paragraph copyable>Click to copy this text.</Paragraph>
<Paragraph copyable={{ text: 'Custom copy text' }}>Display text</Paragraph>
```

## Editable Text

```tsx
<Paragraph editable={{ onChange: setEditedText }}>
  Click to edit this text
</Paragraph>
```
