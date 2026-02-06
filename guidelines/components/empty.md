# Empty

**Purpose**: Display placeholder for empty states. Empty shows when there's no data or content to display.

## When to Use

- Empty tables, lists, or search results
- No data available
- First-time user states
- Filter results with no matches

## API Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `description` | Description text | `ReactNode` | `'No Data'` |
| `image` | Empty image | `ReactNode` | `Empty.PRESENTED_IMAGE_DEFAULT` |
| `imageStyle` | Image style | `CSSProperties` | - |

## Built-in Images

| Image | Description | Usage |
|-------|-------------|-------|
| `Empty.PRESENTED_IMAGE_DEFAULT` | Default illustration | General empty states |
| `Empty.PRESENTED_IMAGE_SIMPLE` | Simple illustration | Smaller spaces |

## Design Tokens Used

### Alias Tokens
- `colorTextDisabled` - Description text color
- `fontSize` - Description text size

## Examples

### Basic Empty
```tsx
import { Empty } from 'antd';

<Empty />
```

### Custom Description
```tsx
<Empty description="No results found" />

// JSX description
<Empty
  description={
    <span>
      No data. <a href="#">Create new</a>
    </span>
  }
/>
```

### No Description
```tsx
<Empty description={false} />
```

### Simple Image
```tsx
<Empty image={Empty.PRESENTED_IMAGE_SIMPLE} />
```

### Custom Image
```tsx
<Empty
  image="https://example.com/custom-empty.svg"
  imageStyle={{ height: 60 }}
  description="Custom empty state"
/>

// Or with component
<Empty
  image={<SmileOutlined style={{ fontSize: 60, color: '#ccc' }} />}
  description="No items yet"
/>
```

### With Action Button
```tsx
<Empty
  description="No data available"
>
  <Button type="primary">Create Now</Button>
</Empty>
```

### In Card
```tsx
<Card>
  <Empty description="No items in this category" />
</Card>
```

### In Table
```tsx
<Table
  dataSource={[]}
  columns={columns}
  locale={{
    emptyText: (
      <Empty
        image={Empty.PRESENTED_IMAGE_SIMPLE}
        description="No records found"
      >
        <Button type="primary">Add Record</Button>
      </Empty>
    ),
  }}
/>
```

### Conditional Rendering
```tsx
{data.length > 0 ? (
  <List dataSource={data} renderItem={renderItem} />
) : (
  <Empty description="No items yet">
    <Button type="primary" onClick={handleCreate}>
      Create First Item
    </Button>
  </Empty>
)}
```

### Search Empty State
```tsx
{searchResults.length === 0 && searchQuery && (
  <Empty
    image={Empty.PRESENTED_IMAGE_SIMPLE}
    description={`No results for "${searchQuery}"`}
  >
    <Button onClick={() => setSearchQuery('')}>
      Clear Search
    </Button>
  </Empty>
)}
```

### ConfigProvider Default Empty
```tsx
import { ConfigProvider, Empty, Table, List } from 'antd';

const customEmpty = () => (
  <Empty
    image={Empty.PRESENTED_IMAGE_SIMPLE}
    description="Nothing here"
  />
);

<ConfigProvider renderEmpty={customEmpty}>
  <Table dataSource={[]} /> {/* Uses custom empty */}
  <List dataSource={[]} /> {/* Uses custom empty */}
</ConfigProvider>
```

## Usage Guidelines

1. **Provide context**: Description should explain why empty and what to do.

2. **Include action**: Add a CTA button when user can take action.

3. **Use simple image for small spaces**: `PRESENTED_IMAGE_SIMPLE` for compact areas.

4. **Custom images for branding**: Replace default with branded illustrations.

5. **Differentiate empty states**:
   - No data yet → Encourage creation
   - No search results → Suggest clearing filters
   - Error loading → Show retry option
