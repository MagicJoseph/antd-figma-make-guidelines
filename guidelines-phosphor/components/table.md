# Table

**Purpose**: Display and organize data in rows and columns. Tables support sorting, filtering, pagination, selection, and more.

## When to Use

- Display structured data with multiple attributes
- Need sorting, filtering, or searching capabilities
- Row selection for bulk actions
- Expandable rows for additional detail

## Component States

| State | Description | Visual Appearance |
|-------|-------------|-------------------|
| **Default** | Normal display | Standard table rows |
| **Hover** | Mouse over row | Row background highlight |
| **Selected** | Row selected | Primary background tint |
| **Loading** | Data loading | Spinner overlay, skeleton rows |
| **Empty** | No data | Empty state placeholder |
| **Sorted** | Column sorted | Sort indicator icon |
| **Filtered** | Column filtered | Filter indicator |

## API Props (Table)

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `columns` | Column configuration | `ColumnType[]` | - |
| `dataSource` | Data array | `object[]` | - |
| `rowKey` | Row key field | `string \| (record) => string` | `'key'` |
| `loading` | Loading state | `boolean \| SpinProps` | `false` |
| `pagination` | Pagination config | `false \| PaginationProps` | - |
| `size` | Table density | `'large' \| 'middle' \| 'small'` | `'large'` |
| `bordered` | Show borders | `boolean` | `false` |
| `scroll` | Scroll config | `{ x, y, scrollToFirstRowOnChange }` | - |
| `rowSelection` | Row selection config | `RowSelectionType` | - |
| `expandable` | Expandable row config | `ExpandableConfig` | - |
| `sticky` | Sticky header | `boolean \| { offsetHeader, offsetScroll }` | - |
| `showHeader` | Show table header | `boolean` | `true` |
| `showSorterTooltip` | Show sort tooltip | `boolean \| TooltipProps` | `true` |
| `onChange` | Pagination/filter/sort change | `(pagination, filters, sorter, extra) => void` | - |
| `onRow` | Row event handlers | `(record, index) => HTMLAttributes` | - |

## Column Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `title` | Column header | `ReactNode` | - |
| `dataIndex` | Data field path | `string \| string[]` | - |
| `key` | Unique key | `string` | - |
| `render` | Custom cell render | `(value, record, index) => ReactNode` | - |
| `width` | Column width | `string \| number` | - |
| `fixed` | Fixed column | `'left' \| 'right'` | - |
| `align` | Text alignment | `'left' \| 'center' \| 'right'` | `'left'` |
| `ellipsis` | Truncate with ellipsis | `boolean \| { showTitle }` | `false` |
| `sorter` | Sort function or config | `boolean \| (a, b) => number \| { compare, multiple }` | - |
| `sortOrder` | Controlled sort order | `'ascend' \| 'descend' \| null` | - |
| `defaultSortOrder` | Default sort order | `'ascend' \| 'descend'` | - |
| `sortDirections` | Available sort orders | `('ascend' \| 'descend')[]` | `['ascend', 'descend']` |
| `filters` | Filter options | `{ text, value }[]` | - |
| `filterMode` | Filter UI | `'menu' \| 'tree'` | `'menu'` |
| `filterSearch` | Enable filter search | `boolean \| (input, filter) => boolean` | `false` |
| `onFilter` | Filter function | `(value, record) => boolean` | - |
| `filteredValue` | Controlled filter value | `string[]` | - |
| `defaultFilteredValue` | Default filter value | `string[]` | - |
| `hidden` | Hide column | `boolean` | `false` |

## Design Tokens Used

### Alias Tokens
- `colorBgContainer` - Table background
- `colorBgElevated` - Header background (bordered)
- `colorBorder` - Border color
- `colorBorderSecondary` - Row divider
- `colorText` - Cell text
- `colorTextHeading` - Header text
- `colorPrimaryBg` - Selected row background
- `colorPrimaryBgHover` - Hover row background
- `padding` - Cell padding
- `fontSize` - Cell text size

## Examples

### Basic Table
```tsx
import { Table } from 'antd';

const columns = [
  {
    title: 'Name',
    dataIndex: 'name',
    key: 'name',
  },
  {
    title: 'Age',
    dataIndex: 'age',
    key: 'age',
  },
  {
    title: 'Address',
    dataIndex: 'address',
    key: 'address',
  },
];

const dataSource = [
  { key: '1', name: 'John', age: 32, address: 'New York' },
  { key: '2', name: 'Jane', age: 28, address: 'London' },
];

<Table columns={columns} dataSource={dataSource} />
```

### With Custom Render
```tsx
const columns = [
  {
    title: 'Name',
    dataIndex: 'name',
    render: (text) => <a>{text}</a>,
  },
  {
    title: 'Status',
    dataIndex: 'status',
    render: (status) => (
      <Tag color={status === 'active' ? 'green' : 'red'}>
        {status.toUpperCase()}
      </Tag>
    ),
  },
  {
    title: 'Action',
    key: 'action',
    render: (_, record) => (
      <Space>
        <Button type="link" onClick={() => handleEdit(record)}>Edit</Button>
        <Button type="link" danger onClick={() => handleDelete(record)}>Delete</Button>
      </Space>
    ),
  },
];
```

### Sorting
```tsx
const columns = [
  {
    title: 'Name',
    dataIndex: 'name',
    sorter: (a, b) => a.name.localeCompare(b.name),
  },
  {
    title: 'Age',
    dataIndex: 'age',
    sorter: (a, b) => a.age - b.age,
    defaultSortOrder: 'descend',
  },
];

<Table columns={columns} dataSource={dataSource} />
```

### Filtering
```tsx
const columns = [
  {
    title: 'Name',
    dataIndex: 'name',
    filters: [
      { text: 'John', value: 'John' },
      { text: 'Jane', value: 'Jane' },
    ],
    onFilter: (value, record) => record.name === value,
    filterSearch: true,
  },
  {
    title: 'Status',
    dataIndex: 'status',
    filters: [
      { text: 'Active', value: 'active' },
      { text: 'Inactive', value: 'inactive' },
    ],
    onFilter: (value, record) => record.status === value,
  },
];
```

### Row Selection
```tsx
const [selectedRowKeys, setSelectedRowKeys] = useState([]);

const rowSelection = {
  selectedRowKeys,
  onChange: (newSelectedRowKeys) => {
    setSelectedRowKeys(newSelectedRowKeys);
  },
};

<Table
  rowSelection={rowSelection}
  columns={columns}
  dataSource={dataSource}
/>
```

### Pagination
```tsx
<Table
  columns={columns}
  dataSource={dataSource}
  pagination={{
    pageSize: 10,
    showSizeChanger: true,
    showQuickJumper: true,
    showTotal: (total) => `Total ${total} items`,
  }}
/>

// Disable pagination
<Table pagination={false} />
```

### Loading State
```tsx
<Table
  loading={isLoading}
  columns={columns}
  dataSource={dataSource}
/>
```

### Fixed Columns and Scroll
```tsx
<Table
  columns={columns}
  dataSource={dataSource}
  scroll={{ x: 1500, y: 400 }}
  // First column fixed left, last fixed right
/>

const columns = [
  { title: 'Name', dataIndex: 'name', fixed: 'left', width: 100 },
  { title: 'Col 1', dataIndex: 'col1' },
  { title: 'Col 2', dataIndex: 'col2' },
  // ... more columns
  { title: 'Action', key: 'action', fixed: 'right', width: 100 },
];
```

### Expandable Rows
```tsx
<Table
  columns={columns}
  dataSource={dataSource}
  expandable={{
    expandedRowRender: (record) => (
      <p style={{ margin: 0 }}>{record.description}</p>
    ),
    rowExpandable: (record) => record.name !== 'Not Expandable',
  }}
/>
```

### Bordered and Sizes
```tsx
<Table bordered columns={columns} dataSource={dataSource} />

<Table size="middle" columns={columns} dataSource={dataSource} />
<Table size="small" columns={columns} dataSource={dataSource} />
```

### Server-side Data
```tsx
const [data, setData] = useState([]);
const [loading, setLoading] = useState(false);
const [pagination, setPagination] = useState({ current: 1, pageSize: 10 });

const fetchData = async (params) => {
  setLoading(true);
  const response = await api.getUsers(params);
  setData(response.data);
  setPagination({
    ...params.pagination,
    total: response.total,
  });
  setLoading(false);
};

const handleTableChange = (pagination, filters, sorter) => {
  fetchData({
    pagination,
    sortField: sorter.field,
    sortOrder: sorter.order,
    ...filters,
  });
};

<Table
  columns={columns}
  dataSource={data}
  pagination={pagination}
  loading={loading}
  onChange={handleTableChange}
/>
```

## Usage Guidelines

1. **Always set `rowKey`**: Provide a unique key for each row to ensure proper rendering.

2. **Use `dataIndex` for simple fields**: Only use `render` when custom rendering is needed.

3. **Set column widths for fixed columns**: Fixed columns require explicit width.

4. **Enable virtual scroll for large datasets**: Use `virtual` prop when rendering 1000+ rows.

5. **Handle loading states**: Show loading indicator during data fetches.

6. **Provide empty state**: Customize `locale.emptyText` for empty tables.

7. **Use pagination for large datasets**: Avoid rendering all rows at once.
