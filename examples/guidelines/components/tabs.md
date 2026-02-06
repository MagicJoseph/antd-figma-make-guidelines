### Tabs

**Purpose**: Organize content into multiple panels accessed via tabs.

**Structure**: Use `Tabs.useTabs()` or `Tabs.useManagedTabs()` hook, then render `Tabs.TabStrip` with `Tabs.Tab` children and `Tabs.TabPanel` components. Prefer `Tabs.useTabs()`, as it is simpler.

**Usage Notes**:
- Add a container with padding around the TabStrip component. It does not have its own padding and does not usually look good without padding.
- If a TabStrip has a border above or below, you MUST add vertical padding around the TabStrip.
- Do not add icons inside Tabs.

**Tabs.useTabs Hook**:
- Args: Object where keys are tab IDs and values are `true`
- Returns: `[tabProps, manager]`
- Each tabProps[key] has props to spread onto corresponding Tab and TabPanel

**Tabs.useManagedTabs Hook**:
- Args: Three args here: tabIds (object where keys are tab IDs and values are `true`), activeTab (string represent the ID of the active tab), and setActiveTab (function that will be called to set the active tab)
- Returns: `[tabProps, manager, { selectedTab, setSelectedTab }]`

**Tabs.TabStrip Props**:
- `manager`: Manager from hook
- `children`: `<Tabs.Tab>` components

**Tabs.Tab Props**:
- Spread props from `tabProps.keyName`
- `children`: ReactNode (tab label)
- `disabled`: Boolean

**Tabs.TabPanel Props**:
- Spread props from `tabProps.keyName`
- `children`: ReactNode (panel content)

**Example**:
```typescript
function TabsExample() {
  const [tabProps, manager] = Tabs.useTabs({
    design: true,
    prototype: true,
    inspect: true,
  })

  return (
    <>
      <Tabs.TabStrip manager={manager}>
        <Tabs.Tab {...tabProps.design}>Design</Tabs.Tab>
        <Tabs.Tab {...tabProps.prototype}>Prototype</Tabs.Tab>
        <Tabs.Tab {...tabProps.inspect}>Inspect</Tabs.Tab>
      </Tabs.TabStrip>

      <Tabs.TabPanel {...tabProps.design}>
        Design content
      </Tabs.TabPanel>
      <Tabs.TabPanel {...tabProps.prototype}>
        Prototype content
      </Tabs.TabPanel>
      <Tabs.TabPanel {...tabProps.inspect}>
        Inspect content
      </Tabs.TabPanel>
    </>
  )
}
```