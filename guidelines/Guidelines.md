This project uses Ant Design (AntD) v6, a React UI component library, and **i18next** for internationalization. Files in the guidelines directory show how to use AntD components, design tokens, and translations.

**Requirements**: React 18 or higher is required. AntD v6 does not support React 17 or earlier.

Always read:
- All files with a name that starts with `overview-`
- All files in the `design-tokens` folder
- All files in the `i18n` folder

Read the files in the `guidelines/components` directory when you want to use the component with that name. For example, if you want to use Button, read `guidelines/components/button.md`.

## Internationalization (i18n) - CRITICAL

This project uses **i18next** with **react-i18next** for internationalization. **ALL user-facing text MUST use translation keys.**

**IMPORTANT**: Before writing any code with text content, read `i18n/overview.md` for the full i18n setup and translation patterns.

### Quick i18n Rules

1. **Never hardcode text** - Use `t('key')` from `useTranslation` hook
2. **Use namespaces** - Organize by feature: `common`, `forms`, `errors`, `components`
3. **Use interpolation** - For dynamic values: `t('greeting', { name: userName })`
4. **Translate everything** - Labels, placeholders, messages, errors, tooltips

### Quick i18n Example

```tsx
import { useTranslation } from 'react-i18next';
import { Button, Form, Input, message } from 'antd';

function LoginForm() {
  const { t } = useTranslation(['common', 'forms']);

  return (
    <Form>
      <Form.Item
        label={t('forms:labels.email')}
        rules={[{ required: true, message: t('forms:validation.required') }]}
      >
        <Input placeholder={t('forms:placeholders.email')} />
      </Form.Item>
      <Button type="primary">{t('common:actions.submit')}</Button>
    </Form>
  );
}
```

## Component Usage Guidelines - READ THIS FIRST

IMPORTANT: Always prefer to use components from Ant Design if they exist. For example, prefer to use a Button component from `antd`, rather than native HTML button elements.

IMPORTANT: Follow these steps IN ORDER before writing any code:

### Step 1: Read Overview Files (REQUIRED)
Read ALL files with a name that starts with "overview-" in the guidelines directory:
- `overview-components.md`
- `overview-icons.md`

### Step 2: Read i18n Guidelines (REQUIRED)
Read the `i18n/overview.md` file. This is CRITICAL for proper internationalization.

### Step 3: Read Design Tokens (REQUIRED)
Read ALL files in the `design-tokens/` folder. Do NOT skip this step. AntD v6 uses a three-layer token system (Seed, Map, Alias) for theming.

### Step 4: Plan What Components You Need (REQUIRED)
Identify which AntD components are needed for your task.

### Step 5: Read Component Guidelines BEFORE Using Components (REQUIRED)
BEFORE using ANY component, you MUST read its guidelines file first:
- Using Button? → Read `guidelines/components/button.md` FIRST
- Using Input? → Read `guidelines/components/input.md` FIRST
- Using Select? → Read `guidelines/components/select.md` FIRST
- Using Table? → Read `guidelines/components/table.md` FIRST
- Using Modal? → Read `guidelines/components/modal.md` FIRST
- Using Form? → Read `guidelines/components/form.md` FIRST

DO NOT write code using a component until you have read its specific guidelines.

### Step 6: Apply Design Tokens Correctly (REQUIRED)
When customizing styles, use the ConfigProvider with theme tokens instead of inline CSS. Reference the design-tokens documentation for available tokens.

### Step 7: Apply Translations (REQUIRED)
Replace ALL user-facing text with translation keys. Use the patterns from `i18n/overview.md`.

## Key Rules

1. **Import from 'antd'**: All components are imported from the `antd` package.
2. **Use i18n for all text**: Never hardcode user-facing strings. Always use `t('key')` from `useTranslation`.
3. **Use ConfigProvider for theming and locale**: Wrap your app with ConfigProvider to customize theme AND set AntD locale.
4. **Use Semantic DOM styling (v6)**: All components support `classNames` and `styles` props for fine-grained customization of internal DOM elements (e.g., `root`, `header`, `body`, `icon`, `content`). These can be objects or functions.
5. **Prefer controlled components**: Use `value` and `onChange` for form controls.
6. **Use Form for data collection**: Let Form handle form state, not individual component state.
7. **Use `variant` instead of `bordered`**: The `bordered` prop is deprecated in v6. Use `variant="borderless"` instead.
8. **Use `destroyOnHidden` instead of `destroyOnClose`**: The `destroyOnClose` prop is deprecated in v6 for Modal, Drawer, Tabs.

## Quick i18n Reference

| Content Type | Namespace | Key Pattern | Example |
|--------------|-----------|-------------|---------|
| Buttons/Actions | `common` | `actions.*` | `t('common:actions.save')` |
| Navigation | `common` | `navigation.*` | `t('common:navigation.home')` |
| Status messages | `common` | `status.*` | `t('common:status.success')` |
| Accessibility | `common` | `a11y.*` | `t('common:a11y.deleteItem')` |
| Form labels | `forms` | `labels.*` | `t('forms:labels.email')` |
| Placeholders | `forms` | `placeholders.*` | `t('forms:placeholders.email')` |
| Validation | `forms` | `validation.*` | `t('forms:validation.required')` |
| Error messages | `errors` | `*` | `t('errors:network')` |
| Component text | `components` | `[component].*` | `t('components:table.empty')` |
| **Page content** | `[feature]` | `*` | `t('dashboard:welcomeMessage')` |

**Feature namespaces** (`dashboard`, `settings`, etc.) are for page-specific content like titles, descriptions, and unique UI text. See `i18n/overview.md` for details.

## i18n Code Generation Rules

**CORE PRINCIPLE: NEVER generate hardcoded user-facing text.** Every visible string in the UI must use a translation key.

### Text-to-Key Mapping Tables

#### Button Labels

| Figma Text | Translation Key |
|------------|-----------------|
| Submit | `common:actions.submit` |
| Cancel | `common:actions.cancel` |
| Save | `common:actions.save` |
| Delete | `common:actions.delete` |
| Edit | `common:actions.edit` |
| Create | `common:actions.create` |
| Confirm | `common:actions.confirm` |
| Close | `common:actions.close` |
| Back | `common:actions.back` |
| Next | `common:actions.next` |
| Search | `common:actions.search` |
| Filter | `common:actions.filter` |
| Clear | `common:actions.clear` |
| Reset | `common:actions.reset` |
| Refresh | `common:actions.refresh` |

#### Form Labels

| Figma Text | Translation Key |
|------------|-----------------|
| Email | `forms:labels.email` |
| Password | `forms:labels.password` |
| Username | `forms:labels.username` |
| First Name | `forms:labels.firstName` |
| Last Name | `forms:labels.lastName` |
| Phone | `forms:labels.phone` |
| Address | `forms:labels.address` |
| City | `forms:labels.city` |
| Country | `forms:labels.country` |
| ZIP Code | `forms:labels.zipCode` |

#### Placeholders

| Figma Placeholder | Translation Key |
|-------------------|-----------------|
| Enter your email | `forms:placeholders.email` |
| Enter your password | `forms:placeholders.password` |
| Search... | `forms:placeholders.search` |
| Please select | `forms:placeholders.select` |

#### Validation Messages

| Validation Type | Translation Key |
|-----------------|-----------------|
| Required field | `forms:validation.required` |
| Invalid email | `forms:validation.email` |
| Min length | `forms:validation.minLength` (use `{ min: X }`) |
| Max length | `forms:validation.maxLength` (use `{ max: X }`) |
| Passwords don't match | `forms:validation.passwordMatch` |

#### Navigation Items

| Figma Text | Translation Key |
|------------|-----------------|
| Home | `common:navigation.home` |
| Dashboard | `common:navigation.dashboard` |
| Settings | `common:navigation.settings` |
| Profile | `common:navigation.profile` |
| Log out | `common:navigation.logout` |

### i18n Anti-Patterns - NEVER DO THIS

#### 1. String Concatenation

```tsx
// WRONG
t('hello') + ' ' + t('world')

// CORRECT - Use single key with interpolation
t('helloWorld')
```

#### 2. Split Sentences

```tsx
// WRONG
<p>{t('youHave')} {count} {t('items')}</p>

// CORRECT - Keep sentence together
<p>{t('youHaveItems', { count })}</p>
```

#### 3. Dynamic Keys

```tsx
// WRONG - Variable in translation key
t(`status.${status}`)

// CORRECT - Map explicitly
const statusMessages = {
  active: t('status.active'),
  inactive: t('status.inactive'),
};
statusMessages[status]
```

#### 4. Hardcoded Aria Labels

```tsx
// WRONG
<Button aria-label="Delete item" icon={<DeleteOutlined />} />

// CORRECT
<Button aria-label={t('common:a11y.deleteItem')} icon={<DeleteOutlined />} />
```

### Modal & Confirmation Dialogs

```tsx
// WRONG
Modal.confirm({
  title: 'Are you sure?',
  content: 'This action cannot be undone.',
});

// CORRECT
Modal.confirm({
  title: t('components:modal.confirmDeleteTitle'),
  content: t('components:modal.confirmDelete'),
  okText: t('common:actions.confirm'),
  cancelText: t('common:actions.cancel'),
});
```

### Table Content

```tsx
// Column title
{
  title: t('forms:labels.email'),
  dataIndex: 'email',
}

// Empty state
<Table
  locale={{
    emptyText: t('components:table.empty'),
  }}
/>

// Pagination total
pagination={{
  showTotal: (total) => t('components:table.total', { count: total }),
}}
```

### i18n Generation Checklist

Before generating code, verify:
- [ ] All button labels use `t('common:actions.*')`
- [ ] All form labels use `t('forms:labels.*')`
- [ ] All placeholders use `t('forms:placeholders.*')`
- [ ] All validation messages use `t('forms:validation.*')`
- [ ] All status messages use `t('common:status.*')` or `t('errors:*')`
- [ ] All navigation items use `t('common:navigation.*')`
- [ ] All table content uses `t('components:table.*')`
- [ ] All modal content uses `t('components:modal.*')`
- [ ] All aria-labels use `t('common:a11y.*')`
- [ ] Dynamic content uses interpolation `t('key', { variable })`
- [ ] Component includes `useTranslation` hook with correct namespaces
- [ ] No hardcoded strings remain in JSX

### Component Template with i18n

```tsx
import { useTranslation } from 'react-i18next';
import { Button, Form, Input, message, theme } from 'antd';
import { SearchOutlined, CheckCircleFilled } from '@ant-design/icons';

interface ComponentNameProps {
  // Define props based on Figma design
}

export function ComponentName({ ...props }: ComponentNameProps) {
  // 1. Always include useTranslation with relevant namespaces
  const { t } = useTranslation(['common', 'forms', 'components', 'errors']);

  // 2. Get design tokens if needed
  const { token } = theme.useToken();

  // 3. Event handlers with translated messages
  const handleSuccess = () => {
    message.success(t('common:status.success'));
  };

  const handleError = () => {
    message.error(t('errors:generic'));
  };

  return (
    // 4. Use translations for ALL visible text
    <Form>
      <Form.Item
        label={t('forms:labels.fieldName')}
        rules={[
          { required: true, message: t('forms:validation.required') }
        ]}
      >
        <Input placeholder={t('forms:placeholders.fieldName')} />
      </Form.Item>

      <Button
        type="primary"
        icon={<SearchOutlined />}
      >
        {t('common:actions.search')}
      </Button>
    </Form>
  );
}
```

## App Setup Template

```tsx
import { Suspense } from 'react';
import { ConfigProvider, App } from 'antd';
import { useTranslation } from 'react-i18next';
import enUS from 'antd/locale/en_US';
import plPL from 'antd/locale/pl_PL';
import csCZ from 'antd/locale/cs_CZ';
import './i18n';

const antdLocales = { en: enUS, pl: plPL, cs: csCZ };

function AppRoot() {
  const { i18n } = useTranslation();
  const locale = antdLocales[i18n.language] || enUS;

  return (
    <ConfigProvider
      locale={locale}
      theme={{
        token: { colorPrimary: '#1890ff' },
      }}
    >
      <App>
        <Suspense fallback={<div>Loading...</div>}>
          <MainApp />
        </Suspense>
      </App>
    </ConfigProvider>
  );
}
```
