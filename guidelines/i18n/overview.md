# Internationalization (i18n)

This project uses **i18next** with **react-i18next** for internationalization. All user-facing text must be translated using the translation system.

## Installation

```bash
npm install i18next react-i18next i18next-browser-languagedetector
```

## Project Structure

```
src/
├── i18n/
│   ├── index.ts              # i18n configuration
│   ├── locales/
│   │   ├── en/
│   │   │   ├── common.json   # Shared translations (actions, status, navigation)
│   │   │   ├── forms.json    # Form-related (labels, placeholders, validation)
│   │   │   ├── errors.json   # Error messages
│   │   │   ├── components.json # Component-specific (table, modal, upload)
│   │   │   ├── dashboard.json  # Feature: Dashboard page content
│   │   │   ├── settings.json   # Feature: Settings page content
│   │   │   └── [feature].json  # Feature: Add more as needed
│   │   ├── pl/
│   │   │   └── ... (same structure)
│   │   └── cs/
│   │       └── ... (same structure)
```

### Namespace Types

| Namespace | Purpose | Examples |
|-----------|---------|----------|
| `common` | Shared across entire app | Actions, status messages, navigation |
| `forms` | Form-related text | Labels, placeholders, validation messages |
| `errors` | Error messages | API errors, validation errors, generic errors |
| `components` | Reusable component text | Table empty states, modal confirmations, upload hints |
| `[feature]` | Feature/page-specific content | `dashboard`, `settings`, `profile`, `products` |

**Rule:** Create a new feature namespace when page/feature content doesn't fit into the core namespaces. This keeps translations organized and allows lazy-loading per feature.

## Configuration

### i18n Setup (src/i18n/index.ts)

```typescript
import i18n from 'i18next';
import { initReactI18next } from 'react-i18next';
import LanguageDetector from 'i18next-browser-languagedetector';

// Import translation resources
import enCommon from './locales/en/common.json';
import enForms from './locales/en/forms.json';
import enErrors from './locales/en/errors.json';
import enComponents from './locales/en/components.json';

import plCommon from './locales/pl/common.json';
import plForms from './locales/pl/forms.json';
import plErrors from './locales/pl/errors.json';
import plComponents from './locales/pl/components.json';

import csCommon from './locales/cs/common.json';
import csForms from './locales/cs/forms.json';
import csErrors from './locales/cs/errors.json';
import csComponents from './locales/cs/components.json';

// Feature-specific namespaces (add as needed)
import enDashboard from './locales/en/dashboard.json';
import enSettings from './locales/en/settings.json';
import plDashboard from './locales/pl/dashboard.json';
import plSettings from './locales/pl/settings.json';
import csDashboard from './locales/cs/dashboard.json';
import csSettings from './locales/cs/settings.json';

const resources = {
  en: {
    common: enCommon,
    forms: enForms,
    errors: enErrors,
    components: enComponents,
    // Feature namespaces
    dashboard: enDashboard,
    settings: enSettings,
  },
  pl: {
    common: plCommon,
    forms: plForms,
    errors: plErrors,
    components: plComponents,
    dashboard: plDashboard,
    settings: plSettings,
  },
  cs: {
    common: csCommon,
    forms: csForms,
    errors: csErrors,
    components: csComponents,
    dashboard: csDashboard,
    settings: csSettings,
  },
};

i18n
  .use(LanguageDetector)
  .use(initReactI18next)
  .init({
    resources,
    fallbackLng: 'en',
    supportedLngs: ['en', 'pl', 'cs'],

    // Namespaces (core + feature-specific)
    ns: ['common', 'forms', 'errors', 'components', 'dashboard', 'settings'],
    defaultNS: 'common',
    fallbackNS: 'common',

    // Interpolation
    interpolation: {
      escapeValue: false, // React already escapes
      formatSeparator: ',',
    },

    // Detection options
    detection: {
      order: ['localStorage', 'navigator', 'htmlTag'],
      caches: ['localStorage'],
    },

    // React-specific options
    react: {
      useSuspense: true,
      bindI18n: 'languageChanged loaded',
      transSupportBasicHtmlNodes: true,
      transKeepBasicHtmlNodesFor: ['br', 'strong', 'i', 'p', 'em', 'a'],
    },
  });

export default i18n;
```

### App Integration

```tsx
import { Suspense } from 'react';
import { ConfigProvider } from 'antd';
import { useTranslation } from 'react-i18next';

// AntD locales
import enUS from 'antd/locale/en_US';
import plPL from 'antd/locale/pl_PL';
import csCZ from 'antd/locale/cs_CZ';

import './i18n'; // Initialize i18n

const antdLocales = {
  en: enUS,
  pl: plPL,
  cs: csCZ,
};

function App() {
  const { i18n } = useTranslation();
  const currentLocale = antdLocales[i18n.language] || enUS;

  return (
    <ConfigProvider locale={currentLocale}>
      <Suspense fallback={<div>Loading...</div>}>
        <MainApp />
      </Suspense>
    </ConfigProvider>
  );
}
```

## Translation File Structure

### Namespace: common.json

```json
{
  "app": {
    "name": "My Application",
    "tagline": "Building great experiences"
  },
  "greeting": "Hello, {{name}}!",
  "actions": {
    "save": "Save",
    "cancel": "Cancel",
    "delete": "Delete",
    "edit": "Edit",
    "create": "Create",
    "submit": "Submit",
    "confirm": "Confirm",
    "close": "Close",
    "back": "Back",
    "next": "Next",
    "search": "Search",
    "filter": "Filter",
    "clear": "Clear",
    "reset": "Reset",
    "refresh": "Refresh",
    "loading": "Loading..."
  },
  "status": {
    "success": "Success",
    "error": "Error",
    "warning": "Warning",
    "info": "Information",
    "pending": "Pending",
    "active": "Active",
    "inactive": "Inactive"
  },
  "navigation": {
    "home": "Home",
    "dashboard": "Dashboard",
    "settings": "Settings",
    "profile": "Profile",
    "logout": "Log out"
  },
  "time": {
    "today": "Today",
    "yesterday": "Yesterday",
    "tomorrow": "Tomorrow",
    "now": "Now"
  },
  "a11y": {
    "deleteItem": "Delete item",
    "editItem": "Edit item",
    "closeModal": "Close modal",
    "openMenu": "Open menu",
    "loading": "Loading content"
  }
}
```

### Namespace: forms.json

```json
{
  "labels": {
    "email": "Email",
    "password": "Password",
    "confirmPassword": "Confirm Password",
    "username": "Username",
    "firstName": "First Name",
    "lastName": "Last Name",
    "phone": "Phone Number",
    "address": "Address",
    "city": "City",
    "country": "Country",
    "zipCode": "ZIP Code"
  },
  "placeholders": {
    "email": "Enter your email",
    "password": "Enter your password",
    "search": "Search...",
    "select": "Please select"
  },
  "validation": {
    "required": "This field is required",
    "email": "Please enter a valid email",
    "minLength": "Must be at least {{min}} characters",
    "maxLength": "Must be no more than {{max}} characters",
    "passwordMatch": "Passwords must match",
    "invalidFormat": "Invalid format"
  },
  "hints": {
    "passwordStrength": "Use at least 8 characters with numbers and symbols"
  }
}
```

### Namespace: errors.json

```json
{
  "generic": "Something went wrong. Please try again.",
  "network": "Network error. Check your connection.",
  "unauthorized": "You are not authorized to perform this action.",
  "notFound": "The requested resource was not found.",
  "serverError": "Server error. Please try again later.",
  "timeout": "Request timed out. Please try again.",
  "validation": "Please check the form for errors.",
  "api": {
    "400": "Bad request. Please check your input.",
    "401": "Session expired. Please log in again.",
    "403": "Access denied.",
    "404": "Not found.",
    "500": "Internal server error."
  }
}
```

### Namespace: components.json

```json
{
  "table": {
    "empty": "No data available",
    "loading": "Loading data...",
    "total": "Total {{count}} items",
    "selected": "{{count}} item selected",
    "selected_other": "{{count}} items selected"
  },
  "modal": {
    "confirmDelete": "Are you sure you want to delete this item?",
    "confirmDeleteTitle": "Confirm Deletion",
    "unsavedChanges": "You have unsaved changes. Discard them?",
    "unsavedChangesTitle": "Unsaved Changes"
  },
  "upload": {
    "dragHere": "Drag files here or click to upload",
    "maxSize": "Maximum file size: {{size}}MB",
    "allowedTypes": "Allowed types: {{types}}",
    "uploading": "Uploading...",
    "uploadSuccess": "File uploaded successfully",
    "uploadError": "Upload failed"
  },
  "pagination": {
    "page": "Page",
    "of": "of",
    "items": "items",
    "perPage": "per page"
  },
  "datePicker": {
    "selectDate": "Select date",
    "selectTime": "Select time",
    "startDate": "Start date",
    "endDate": "End date"
  }
}
```

### Feature Namespace: dashboard.json

Feature namespaces contain page/feature-specific content that doesn't belong in core namespaces.

```json
{
  "pageTitle": "Dashboard",
  "welcomeMessage": "Welcome back, {{name}}!",
  "lastLogin": "Last login: {{date}}",
  "stats": {
    "totalUsers": "Total Users",
    "activeUsers": "Active Users",
    "newOrders": "New Orders",
    "revenue": "Revenue"
  },
  "widgets": {
    "recentActivity": "Recent Activity",
    "quickActions": "Quick Actions",
    "notifications": "Notifications"
  },
  "emptyState": {
    "noActivity": "No recent activity",
    "noNotifications": "You're all caught up!"
  }
}
```

### Feature Namespace: settings.json

```json
{
  "pageTitle": "Settings",
  "sections": {
    "general": "General",
    "security": "Security",
    "notifications": "Notifications",
    "appearance": "Appearance",
    "privacy": "Privacy"
  },
  "general": {
    "language": "Language",
    "timezone": "Timezone",
    "dateFormat": "Date Format"
  },
  "security": {
    "changePassword": "Change Password",
    "twoFactor": "Two-Factor Authentication",
    "sessions": "Active Sessions"
  },
  "notifications": {
    "email": "Email Notifications",
    "push": "Push Notifications",
    "frequency": "Notification Frequency"
  },
  "messages": {
    "saveSuccess": "Settings saved successfully",
    "saveError": "Failed to save settings"
  }
}
```

### When to Create a Feature Namespace

Create a new `[feature].json` namespace when:
- Content is specific to one page/feature (not reused elsewhere)
- The feature has multiple unique text elements (titles, descriptions, labels)
- You want to lazy-load translations for that feature

**Do NOT create** a feature namespace for:
- Generic buttons/actions → use `common:actions.*`
- Form field labels → use `forms:labels.*`
- Error messages → use `errors:*`
- Reusable component text → use `components:*`

## Using Translations

### useTranslation Hook

```tsx
import { useTranslation } from 'react-i18next';

function MyComponent() {
  // Basic usage - uses default namespace (common)
  const { t } = useTranslation();

  // With specific namespace
  const { t: tForms } = useTranslation('forms');

  // With multiple namespaces
  const { t: tMulti } = useTranslation(['common', 'forms']);

  // With key prefix for nested keys
  const { t: tActions } = useTranslation('common', { keyPrefix: 'actions' });

  return (
    <div>
      {/* Simple translation */}
      <h1>{t('app.name')}</h1>

      {/* From specific namespace */}
      <label>{tForms('labels.email')}</label>

      {/* With key prefix - 'save' becomes 'actions.save' */}
      <Button>{tActions('save')}</Button>

      {/* Explicit namespace syntax */}
      <p>{t('forms:validation.required')}</p>
    </div>
  );
}
```

### Interpolation

```tsx
const { t } = useTranslation();

// Simple interpolation
// JSON: "welcome": "Hello, {{name}}!"
<p>{t('welcome', { name: 'John' })}</p>
// Output: "Hello, John!"

// Multiple values
// JSON: "greeting": "Hello {{firstName}} {{lastName}}, welcome to {{app}}!"
<p>{t('greeting', { firstName: 'John', lastName: 'Doe', app: 'MyApp' })}</p>

// With formatting
// JSON: "price": "Price: {{value, number}}"
<p>{t('price', { value: 1234.56 })}</p>
// Output: "Price: 1,234.56"

// Currency formatting
// JSON: "total": "Total: {{amount, currency(USD)}}"
<p>{t('total', { amount: 99.99 })}</p>
// Output: "Total: $99.99"

// Date formatting
// JSON: "createdAt": "Created: {{date, datetime}}"
<p>{t('createdAt', { date: new Date() })}</p>
```

### Pluralization

```tsx
const { t } = useTranslation();

// JSON structure for plurals:
// "items_one": "{{count}} item"
// "items_other": "{{count}} items"

<p>{t('items', { count: 1 })}</p>  // "1 item"
<p>{t('items', { count: 5 })}</p>  // "5 items"
<p>{t('items', { count: 0 })}</p>  // "0 items"

// Complex plurals (e.g., Polish)
// "files_one": "{{count}} plik"
// "files_few": "{{count}} pliki"      // 2-4
// "files_many": "{{count}} plików"    // 5+, 0
// "files_other": "{{count}} pliku"    // fractions
```

### Trans Component for Rich Text

```tsx
import { Trans } from 'react-i18next';
import { Link } from 'react-router-dom';

function RichTextExample() {
  const name = 'John';
  const count = 5;

  return (
    <div>
      {/* With embedded components */}
      {/* JSON: "terms": "By continuing, you agree to our <link>Terms of Service</link>." */}
      <Trans
        i18nKey="terms"
        components={{ link: <Link to="/terms" /> }}
      />

      {/* With interpolation and components */}
      {/* JSON: "welcome": "Hello <bold>{{name}}</bold>, you have <bold>{{count}}</bold> messages." */}
      <Trans
        i18nKey="welcome"
        values={{ name, count }}
        components={{ bold: <strong /> }}
      />

      {/* With array-based components */}
      {/* JSON: "info": "Read our <0>documentation</0> or <1>contact us</1>." */}
      <Trans
        i18nKey="info"
        components={[
          <a href="/docs" />,
          <a href="/contact" />
        ]}
      />
    </div>
  );
}
```

### Language Switching

```tsx
import { useTranslation } from 'react-i18next';
import { Select } from 'antd';

function LanguageSwitcher() {
  const { i18n, t } = useTranslation();

  const languages = [
    { value: 'en', label: 'English' },
    { value: 'pl', label: 'Polski' },
    { value: 'cs', label: 'Ceština' },
  ];

  const handleChange = (lng: string) => {
    i18n.changeLanguage(lng);
  };

  return (
    <Select
      value={i18n.language}
      onChange={handleChange}
      options={languages}
      style={{ width: 120 }}
    />
  );
}
```

## Integration with AntD Components

### Form with Translations

```tsx
import { Form, Input, Button, message } from 'antd';
import { useTranslation } from 'react-i18next';

function LoginForm() {
  const { t } = useTranslation(['forms', 'common', 'errors']);
  const [form] = Form.useForm();

  const onFinish = async (values) => {
    try {
      await login(values);
      message.success(t('common:status.success'));
    } catch (error) {
      message.error(t('errors:generic'));
    }
  };

  return (
    <Form form={form} onFinish={onFinish}>
      <Form.Item
        name="email"
        label={t('forms:labels.email')}
        rules={[
          { required: true, message: t('forms:validation.required') },
          { type: 'email', message: t('forms:validation.email') }
        ]}
      >
        <Input placeholder={t('forms:placeholders.email')} />
      </Form.Item>

      <Form.Item
        name="password"
        label={t('forms:labels.password')}
        rules={[
          { required: true, message: t('forms:validation.required') },
          { min: 8, message: t('forms:validation.minLength', { min: 8 }) }
        ]}
      >
        <Input.Password placeholder={t('forms:placeholders.password')} />
      </Form.Item>

      <Form.Item>
        <Button type="primary" htmlType="submit">
          {t('common:actions.submit')}
        </Button>
      </Form.Item>
    </Form>
  );
}
```

### Table with Translations

```tsx
import { Table, Button, Popconfirm, Space, message } from 'antd';
import { useTranslation } from 'react-i18next';
import { DeleteOutlined, EditOutlined } from '@ant-design/icons';

function UsersTable({ data, onDelete, onEdit }) {
  const { t } = useTranslation(['common', 'forms', 'components']);

  const columns = [
    {
      title: t('forms:labels.username'),
      dataIndex: 'username',
      key: 'username',
    },
    {
      title: t('forms:labels.email'),
      dataIndex: 'email',
      key: 'email',
    },
    {
      title: t('common:actions.edit'),
      key: 'actions',
      render: (_, record) => (
        <Space>
          <Button
            type="text"
            icon={<EditOutlined />}
            onClick={() => onEdit(record)}
          >
            {t('common:actions.edit')}
          </Button>
          <Popconfirm
            title={t('components:modal.confirmDeleteTitle')}
            description={t('components:modal.confirmDelete')}
            onConfirm={() => onDelete(record.id)}
            okText={t('common:actions.confirm')}
            cancelText={t('common:actions.cancel')}
          >
            <Button
              type="text"
              danger
              icon={<DeleteOutlined />}
            >
              {t('common:actions.delete')}
            </Button>
          </Popconfirm>
        </Space>
      ),
    },
  ];

  return (
    <Table
      dataSource={data}
      columns={columns}
      locale={{
        emptyText: t('components:table.empty'),
      }}
      pagination={{
        showTotal: (total) => t('components:table.total', { count: total }),
      }}
    />
  );
}
```

### Modal with Translations

```tsx
import { Modal, App } from 'antd';
import { useTranslation } from 'react-i18next';
import { ExclamationCircleFilled } from '@ant-design/icons';

function useConfirmDelete() {
  const { t } = useTranslation(['common', 'components']);
  const { modal } = App.useApp();

  const confirmDelete = (onConfirm: () => void) => {
    modal.confirm({
      title: t('components:modal.confirmDeleteTitle'),
      icon: <ExclamationCircleFilled />,
      content: t('components:modal.confirmDelete'),
      okText: t('common:actions.delete'),
      okType: 'danger',
      cancelText: t('common:actions.cancel'),
      onOk: onConfirm,
    });
  };

  return { confirmDelete };
}
```

## Translation Key Naming Conventions

### Structure Rules

1. **Use nested keys for organization**:
   ```json
   {
     "user": {
       "profile": {
         "title": "User Profile",
         "edit": "Edit Profile"
       }
     }
   }
   ```

2. **Use camelCase for key names**:
   ```json
   {
     "firstName": "First Name",
     "lastName": "Last Name",
     "emailAddress": "Email Address"
   }
   ```

3. **Group by feature/domain**:
   - `common` - Shared across app
   - `forms` - Form labels, placeholders, validation
   - `errors` - Error messages
   - `components` - Component-specific text
   - `[feature]` - Feature-specific (e.g., `dashboard`, `settings`)

4. **Use descriptive suffixes**:
   - `*Title` - Page/section titles
   - `*Description` - Longer descriptions
   - `*Hint` - Helper text
   - `*Error` - Error messages
   - `*Success` - Success messages
   - `*Placeholder` - Input placeholders

### Examples

```json
{
  "dashboard": {
    "pageTitle": "Dashboard",
    "welcomeMessage": "Welcome back, {{name}}!",
    "stats": {
      "totalUsers": "Total Users",
      "activeUsers": "Active Users",
      "revenue": "Revenue"
    }
  },
  "settings": {
    "pageTitle": "Settings",
    "sections": {
      "general": "General",
      "security": "Security",
      "notifications": "Notifications"
    },
    "saveSuccess": "Settings saved successfully",
    "saveError": "Failed to save settings"
  }
}
```

## Best Practices

### DO:

1. **Always use translation keys** - Never hardcode user-facing text
2. **Use namespaces** - Organize translations by feature/domain
3. **Include context in keys** - Make keys self-documenting
4. **Provide default values** - For graceful degradation
5. **Use interpolation** - For dynamic content
6. **Test all languages** - Ensure layouts work with longer text

### DON'T:

1. **Don't concatenate translations** - Use interpolation instead
   ```tsx
   // BAD
   t('hello') + ' ' + t('world')

   // GOOD
   t('helloWorld') // or t('greeting', { name: 'World' })
   ```

2. **Don't split sentences** - Keep full sentences together
   ```tsx
   // BAD
   t('youHave') + count + t('items')

   // GOOD
   t('youHaveItems', { count })
   ```

3. **Don't use variables in keys**
   ```tsx
   // BAD
   t(`status.${status}`)

   // GOOD - use context or explicit mapping
   const statusMap = {
     active: t('status.active'),
     inactive: t('status.inactive'),
   };
   ```

4. **Don't forget RTL languages** - Design layouts to be RTL-compatible

## Figma Make Integration

When generating code from Figma designs, follow these rules:

### For Static Text

Replace all visible text with translation keys:

```tsx
// Instead of:
<Button>Submit</Button>

// Generate:
<Button>{t('common:actions.submit')}</Button>
```

### For Form Labels

```tsx
// Instead of:
<Form.Item label="Email">

// Generate:
<Form.Item label={t('forms:labels.email')}>
```

### For Placeholders

```tsx
// Instead of:
<Input placeholder="Enter your email" />

// Generate:
<Input placeholder={t('forms:placeholders.email')} />
```

### For Validation Messages

```tsx
// Instead of:
rules={[{ required: true, message: 'This field is required' }]}

// Generate:
rules={[{ required: true, message: t('forms:validation.required') }]}
```

### For Dynamic Content

```tsx
// Instead of:
<span>Hello, John!</span>

// Generate:
<span>{t('common:greeting', { name: userName })}</span>
```

### For Status Messages

```tsx
// Instead of:
message.success('Operation completed successfully');

// Generate:
message.success(t('common:status.success'));
```

### Component Template with i18n

```tsx
import { useTranslation } from 'react-i18next';
import { Button, Form, Input, message } from 'antd';

interface ComponentNameProps {
  // props
}

export function ComponentName({ ...props }: ComponentNameProps) {
  const { t } = useTranslation(['common', 'forms']);

  return (
    <Form>
      <Form.Item
        name="fieldName"
        label={t('forms:labels.fieldName')}
        rules={[
          { required: true, message: t('forms:validation.required') }
        ]}
      >
        <Input placeholder={t('forms:placeholders.fieldName')} />
      </Form.Item>

      <Button type="primary">
        {t('common:actions.submit')}
      </Button>
    </Form>
  );
}
```

## Adding New Languages

1. Create new locale folder: `src/i18n/locales/[lang]/`
2. Copy all JSON files from `en/` folder
3. Translate all values
4. Add import in `src/i18n/index.ts`
5. Add to `supportedLngs` array
6. Import corresponding AntD locale
7. Add to `antdLocales` map
