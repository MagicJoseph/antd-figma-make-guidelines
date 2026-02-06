# Ant Design v6 – Figma Make Guidelines

Guidelines for [Figma Make](https://www.figma.com/make/) to generate code using **Ant Design v6** components, design tokens, and best practices.

## What is this?

This repository contains structured guidelines that teach AI code generators (like Figma Make) how to correctly use Ant Design v6. It includes:

- **Component guidelines** – usage patterns, API reference, and examples for 26 AntD components
- **Design tokens** – color system, typography, spacing, and the three-layer token system (Seed, Map, Alias)
- **Phosphor Icons variant** – alternative guidelines using Phosphor Icons instead of default AntD icons

## Structure

```
├── guidelines/                  # AntD v6 with default @ant-design/icons
│   ├── Guidelines.md            # Main entry point
│   ├── overview-components.md   # Component categories and best practices
│   ├── overview-icons.md        # Icon usage guide
│   ├── components/              # Per-component guidelines (26 files)
│   └── design-tokens/           # Colors, typography, spacing, overview
│
├── guidelines-phosphor/         # AntD v6 with Phosphor Icons
│   ├── Guidelines.md            # Entry point (includes Phosphor setup)
│   ├── components/              # Component guidelines with Phosphor examples
│   └── design-tokens/           # Same token system
│
├── examples/                    # Example guidelines for reference
└── VALIDATION_REPORT.md         # v6 API validation status
```

## Covered Components

| Category | Components |
|----------|------------|
| **General** | Button, Typography |
| **Navigation** | Menu, Tabs |
| **Data Entry** | Checkbox, DatePicker, Form, Input, Radio, Select, Switch |
| **Data Display** | Avatar, Badge, Card, Empty, Progress, Table, Tag, Tooltip |
| **Feedback** | Alert, Drawer, Message, Modal, Notification, Popconfirm, Result, Spin |

## Key AntD v6 Rules

- **React 18+** required
- Use `variant` instead of deprecated `bordered` prop
- Use `destroyOnHidden` instead of deprecated `destroyOnClose`
- Use `classNames` / `styles` props for Semantic DOM styling
- Theme via `ConfigProvider` with the three-layer token system

## How to Use

### With Figma Make
Upload the `guidelines/` or `guidelines-phosphor/` folder as guidelines in your Figma Make project. The AI will follow the component patterns and design token system when generating code.

### With Other AI Tools
Point your AI assistant to `guidelines/Guidelines.md` as the entry point. It contains step-by-step instructions for reading the documentation in the correct order.

## License

MIT
