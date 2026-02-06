# Result

**Purpose**: Display the result of an operation or important status. Result is used to give feedback on significant outcomes.

## When to Use

- Operation success/failure feedback
- Submission completion
- Permission denied pages
- 404/500 error pages

## Result Status Types

| Status | Description | Visual |
|--------|-------------|--------|
| **success** | Operation succeeded | Green checkmark |
| **error** | Operation failed | Red X mark |
| **info** | Information | Blue info icon |
| **warning** | Warning/caution | Yellow warning icon |
| **404** | Page not found | 404 illustration |
| **403** | Not authorized | 403 illustration |
| **500** | Server error | 500 illustration |

## API Props

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `status` | Result status | `'success' \| 'error' \| 'info' \| 'warning' \| '404' \| '403' \| '500'` | `'info'` |
| `title` | Main title | `ReactNode` | - |
| `subTitle` | Subtitle/description | `ReactNode` | - |
| `icon` | Custom icon | `ReactNode` | - |
| `extra` | Action area content | `ReactNode` | - |

## Design Tokens Used

### Alias Tokens
- `colorSuccess` - Success icon
- `colorError` - Error icon
- `colorWarning` - Warning icon
- `colorInfo` - Info icon
- `colorText` - Title text
- `colorTextSecondary` - Subtitle text
- `fontSize` - Text sizes

## Examples

### Success Result
```tsx
import { Result, Button } from 'antd';

<Result
  status="success"
  title="Successfully Purchased!"
  subTitle="Order number: 2017182818828182881. It may take 1-5 minutes to process."
  extra={[
    <Button type="primary" key="console">
      Go to Dashboard
    </Button>,
    <Button key="buy">Buy Again</Button>,
  ]}
/>
```

### Error Result
```tsx
import { XCircleIcon } from './icons';
import { theme } from 'antd';

const { token } = theme.useToken();

<Result
  status="error"
  title="Submission Failed"
  subTitle="Please check and modify the following information before resubmitting."
  extra={[
    <Button type="primary" key="retry">
      Try Again
    </Button>,
    <Button key="back">Go Back</Button>,
  ]}
>
  <div className="desc">
    <Paragraph>
      <Text strong>The content you submitted has the following error:</Text>
    </Paragraph>
    <Paragraph>
      <XCircleIcon color={token.colorError} weight="fill" /> Your account has been frozen.
    </Paragraph>
    <Paragraph>
      <XCircleIcon color={token.colorError} weight="fill" /> Your account is not eligible.
    </Paragraph>
  </div>
</Result>
```

### Info Result
```tsx
<Result
  title="Your operation has been completed"
  extra={
    <Button type="primary">Next Step</Button>
  }
/>
```

### Warning Result
```tsx
<Result
  status="warning"
  title="There are some problems with your operation"
  extra={
    <Button type="primary">Go Console</Button>
  }
/>
```

### 404 Page
```tsx
<Result
  status="404"
  title="404"
  subTitle="Sorry, the page you visited does not exist."
  extra={<Button type="primary">Back Home</Button>}
/>
```

### 403 Page
```tsx
<Result
  status="403"
  title="403"
  subTitle="Sorry, you are not authorized to access this page."
  extra={<Button type="primary">Back Home</Button>}
/>
```

### 500 Page
```tsx
<Result
  status="500"
  title="500"
  subTitle="Sorry, something went wrong."
  extra={<Button type="primary">Back Home</Button>}
/>
```

### Custom Icon
```tsx
import { SmileyIcon, CheckCircleIcon, XCircleIcon, WarningIcon } from './icons';
import { theme } from 'antd';

const { token } = theme.useToken();

<Result
  icon={<SmileyIcon size={72} weight="fill" />}
  title="Great, we have done all the operations!"
  extra={<Button type="primary">Next</Button>}
/>

// Success with Phosphor icon
<Result
  status="success"
  icon={<CheckCircleIcon color={token.colorSuccess} size={72} weight="fill" />}
  title="Successfully Purchased!"
  subTitle="Order number: 2017182818828182881"
/>

// Error with Phosphor icon
<Result
  status="error"
  icon={<XCircleIcon color={token.colorError} size={72} weight="fill" />}
  title="Submission Failed"
/>

// Warning with Phosphor icon
<Result
  status="warning"
  icon={<WarningIcon color={token.colorWarning} size={72} weight="fill" />}
  title="There are some problems with your operation"
/>
```

### In Modal
```tsx
<Modal open={showResult} footer={null}>
  <Result
    status="success"
    title="Payment Successful"
    subTitle="Your order has been placed."
    extra={
      <Button type="primary" onClick={() => setShowResult(false)}>
        Done
      </Button>
    }
  />
</Modal>
```

### Form Submission Result
```tsx
const [submitted, setSubmitted] = useState(false);

{submitted ? (
  <Result
    status="success"
    title="Form Submitted"
    subTitle="We'll get back to you within 24 hours."
    extra={
      <Button type="primary" onClick={() => setSubmitted(false)}>
        Submit Another
      </Button>
    }
  />
) : (
  <Form onFinish={() => setSubmitted(true)}>
    {/* form fields */}
  </Form>
)}
```

### With Additional Content
```tsx
<Result
  status="success"
  title="Order Placed"
  subTitle="Order #12345"
  extra={[
    <Button type="primary" key="track">Track Order</Button>,
    <Button key="home">Continue Shopping</Button>,
  ]}
>
  <Descriptions title="Order Info" column={1}>
    <Descriptions.Item label="Product">Cloud Database</Descriptions.Item>
    <Descriptions.Item label="Amount">$250.00</Descriptions.Item>
    <Descriptions.Item label="Discount">$20.00</Descriptions.Item>
    <Descriptions.Item label="Total">$230.00</Descriptions.Item>
  </Descriptions>
</Result>
```

## Usage Guidelines

1. **Use for significant outcomes**: Results are for important feedback, not routine actions.

2. **Provide clear next steps**: Always include action buttons in `extra`.

3. **Match status to outcome**: Use appropriate status for the situation.

4. **Keep title short**: Title should be scannable; put details in subtitle.

5. **Use for error pages**: 404, 403, 500 pages benefit from Result component.

6. **Full page or modal**: Result works well as full-page or in modal after operations.
