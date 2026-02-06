# Form

**Purpose**: Collect and validate user input. Forms handle data binding, validation, and submission in a structured way.

## When to Use

- Collecting user data (registration, settings, etc.)
- Data entry with validation requirements
- Multi-field submissions
- Complex forms with dependencies between fields

## Component States

| State | Description | Visual Appearance |
|-------|-------------|-------------------|
| **Default** | Empty form | Labels and empty inputs |
| **Filled** | Has values | Inputs show entered data |
| **Validating** | Checking input | Spinner on field |
| **Success** | Validation passed | Green checkmark (with hasFeedback) |
| **Error** | Validation failed | Red border, error message |
| **Warning** | Validation warning | Yellow border, warning message |
| **Disabled** | Not editable | Grayed inputs |
| **Submitting** | Form submitting | Submit button loading |

## API Props (Form)

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `form` | Form instance from useForm | `FormInstance` | - |
| `initialValues` | Initial field values | `object` | - |
| `onFinish` | Submit success handler | `(values) => void` | - |
| `onFinishFailed` | Submit fail handler | `(errorInfo) => void` | - |
| `onValuesChange` | Field value change handler | `(changedValues, allValues) => void` | - |
| `layout` | Form layout | `'horizontal' \| 'vertical' \| 'inline'` | `'horizontal'` |
| `labelCol` | Label column layout | `ColProps` | - |
| `wrapperCol` | Input column layout | `ColProps` | - |
| `labelAlign` | Label text align | `'left' \| 'right'` | `'right'` |
| `colon` | Show colon after labels | `boolean` | `true` |
| `requiredMark` | Required field marker | `boolean \| 'optional'` | `true` |
| `disabled` | Disable all fields | `boolean` | `false` |
| `size` | Field size | `'large' \| 'middle' \| 'small'` | - |
| `validateMessages` | Custom validation messages | `ValidateMessages` | - |
| `validateTrigger` | When to validate | `string \| string[]` | `'onChange'` |
| `preserve` | Preserve values when unmount | `boolean` | `true` |

## API Props (Form.Item)

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `name` | Field name (path) | `NamePath` | - |
| `label` | Field label | `ReactNode` | - |
| `rules` | Validation rules | `Rule[]` | - |
| `required` | Show required mark | `boolean` | `false` |
| `validateStatus` | Override validation status | `'success' \| 'warning' \| 'error' \| 'validating'` | - |
| `help` | Help message | `ReactNode` | - |
| `extra` | Extra hint below field | `ReactNode` | - |
| `hasFeedback` | Show validation icon | `boolean` | `false` |
| `dependencies` | Re-validate when dependencies change | `NamePath[]` | - |
| `valuePropName` | Child value prop name | `string` | `'value'` |
| `trigger` | Child change event name | `string` | `'onChange'` |
| `validateTrigger` | When to validate | `string \| string[]` | `'onChange'` |
| `initialValue` | Field initial value | `any` | - |
| `tooltip` | Tooltip for label | `ReactNode \| TooltipProps` | - |
| `hidden` | Hide field (still validate) | `boolean` | `false` |
| `noStyle` | No wrapper styling | `boolean` | `false` |

## Validation Rules

| Rule | Description | Example |
|------|-------------|---------|
| `required` | Field is required | `{ required: true, message: 'Required' }` |
| `type` | Data type validation | `{ type: 'email' }`, `{ type: 'url' }`, `{ type: 'number' }` |
| `min` / `max` | Length/value limits | `{ min: 3, max: 20 }` |
| `len` | Exact length | `{ len: 10 }` |
| `pattern` | Regex pattern | `{ pattern: /^[A-Z]+$/ }` |
| `validator` | Custom validation | `{ validator: (_, value) => Promise }` |
| `whitespace` | Reject whitespace-only | `{ whitespace: true }` |
| `enum` | Value must be in list | `{ enum: ['a', 'b', 'c'] }` |

## Design Tokens Used

### Alias Tokens
- `colorError` - Error state color
- `colorWarning` - Warning state color
- `colorSuccess` - Success state color
- `colorText` - Label text
- `colorTextSecondary` - Help/extra text
- `fontSize` - Label/input text size
- `marginSM` - Space between label and input
- `marginLG` - Space between form items

## Examples

### Basic Form
```tsx
import { Form, Input, Button } from 'antd';

const BasicForm = () => {
  const onFinish = (values) => {
    console.log('Success:', values);
  };

  return (
    <Form
      name="basic"
      labelCol={{ span: 8 }}
      wrapperCol={{ span: 16 }}
      onFinish={onFinish}
      autoComplete="off"
    >
      <Form.Item
        label="Username"
        name="username"
        rules={[{ required: true, message: 'Please input your username!' }]}
      >
        <Input />
      </Form.Item>

      <Form.Item
        label="Password"
        name="password"
        rules={[{ required: true, message: 'Please input your password!' }]}
      >
        <Input.Password />
      </Form.Item>

      <Form.Item wrapperCol={{ offset: 8, span: 16 }}>
        <Button type="primary" htmlType="submit">
          Submit
        </Button>
      </Form.Item>
    </Form>
  );
};
```

### Form with useForm Hook
```tsx
const [form] = Form.useForm();

// Set values programmatically
form.setFieldsValue({
  username: 'john',
  email: 'john@example.com',
});

// Get values
const values = form.getFieldsValue();
const username = form.getFieldValue('username');

// Validate fields
const validateAndSubmit = async () => {
  try {
    const values = await form.validateFields();
    console.log('Valid:', values);
  } catch (error) {
    console.log('Invalid:', error.errorFields);
  }
};

// Reset form
form.resetFields();

<Form form={form} onFinish={handleSubmit}>
  ...
</Form>
```

### Vertical Layout
```tsx
<Form layout="vertical">
  <Form.Item label="Username" name="username">
    <Input />
  </Form.Item>
  <Form.Item label="Password" name="password">
    <Input.Password />
  </Form.Item>
</Form>
```

### Inline Layout
```tsx
<Form layout="inline" onFinish={handleSearch}>
  <Form.Item name="keyword">
    <Input placeholder="Search..." />
  </Form.Item>
  <Form.Item>
    <Button type="primary" htmlType="submit">
      Search
    </Button>
  </Form.Item>
</Form>
```

### Validation Rules
```tsx
<Form.Item
  name="email"
  label="Email"
  rules={[
    { required: true, message: 'Email is required' },
    { type: 'email', message: 'Invalid email format' },
  ]}
>
  <Input />
</Form.Item>

<Form.Item
  name="password"
  label="Password"
  rules={[
    { required: true, message: 'Password is required' },
    { min: 8, message: 'Password must be at least 8 characters' },
    {
      pattern: /^(?=.*[A-Za-z])(?=.*\d)/,
      message: 'Must contain letters and numbers',
    },
  ]}
  hasFeedback
>
  <Input.Password />
</Form.Item>

<Form.Item
  name="confirm"
  label="Confirm Password"
  dependencies={['password']}
  rules={[
    { required: true },
    ({ getFieldValue }) => ({
      validator(_, value) {
        if (!value || getFieldValue('password') === value) {
          return Promise.resolve();
        }
        return Promise.reject(new Error('Passwords do not match'));
      },
    }),
  ]}
  hasFeedback
>
  <Input.Password />
</Form.Item>
```

### Custom Validation Status
```tsx
<Form.Item
  label="Async Field"
  name="async"
  hasFeedback
  validateStatus={asyncStatus} // 'validating' | 'success' | 'error'
  help={asyncMessage}
>
  <Input />
</Form.Item>
```

### Form with Different Input Types
```tsx
<Form layout="vertical" initialValues={{ remember: true, gender: 'male' }}>
  <Form.Item name="username" label="Username">
    <Input />
  </Form.Item>

  <Form.Item name="gender" label="Gender">
    <Radio.Group>
      <Radio value="male">Male</Radio>
      <Radio value="female">Female</Radio>
    </Radio.Group>
  </Form.Item>

  <Form.Item name="remember" valuePropName="checked">
    <Checkbox>Remember me</Checkbox>
  </Form.Item>

  <Form.Item name="bio" label="Bio">
    <Input.TextArea rows={4} />
  </Form.Item>

  <Form.Item name="country" label="Country">
    <Select options={countryOptions} />
  </Form.Item>

  <Form.Item name="birthday" label="Birthday">
    <DatePicker />
  </Form.Item>

  <Form.Item name="rating" label="Rating">
    <Rate />
  </Form.Item>

  <Form.Item name="agree" valuePropName="checked">
    <Switch /> I agree to terms
  </Form.Item>
</Form>
```

### Dynamic Form Fields
```tsx
<Form.List name="users">
  {(fields, { add, remove }) => (
    <>
      {fields.map(({ key, name, ...restField }) => (
        <Space key={key} align="baseline">
          <Form.Item
            {...restField}
            name={[name, 'first']}
            rules={[{ required: true }]}
          >
            <Input placeholder="First Name" />
          </Form.Item>
          <Form.Item
            {...restField}
            name={[name, 'last']}
            rules={[{ required: true }]}
          >
            <Input placeholder="Last Name" />
          </Form.Item>
          <MinusCircleOutlined onClick={() => remove(name)} />
        </Space>
      ))}
      <Form.Item>
        <Button type="dashed" onClick={() => add()} block icon={<PlusOutlined />}>
          Add User
        </Button>
      </Form.Item>
    </>
  )}
</Form.List>
```

### Nested Fields
```tsx
<Form.Item name={['user', 'name']} label="Name">
  <Input />
</Form.Item>
<Form.Item name={['user', 'email']} label="Email">
  <Input />
</Form.Item>
// Results in: { user: { name: '...', email: '...' } }
```

## Usage Guidelines

1. **Use Form for all data collection**: Even single inputs benefit from Form's validation.

2. **Choose appropriate layout**:
   - `horizontal`: Label beside input (forms with many fields)
   - `vertical`: Label above input (simple forms, mobile)
   - `inline`: All in one row (search/filter forms)

3. **Provide clear validation messages**: Custom messages help users fix errors.

4. **Use `initialValues` for defaults**: Don't use `defaultValue` on inputs inside Form.

5. **Handle async validation**: Use `validator` returning Promise for async checks.

6. **Show feedback for important fields**: Use `hasFeedback` on password/email fields.

7. **Disable submit while validating**: Prevent double submission with loading state.

8. **Reset form after success**: Call `form.resetFields()` after successful submission.
