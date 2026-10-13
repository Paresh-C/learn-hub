## 12. Design patterns for React

| Pattern | Use when | Notes |
| --- | --- | --- |
| Custom hook | Reusing stateful logic | The default way to share logic today; also acts as a view-model |
| Composition (children / slots) | Flexible layout without many props | Prefer over config props and inheritance |
| Compound components | A set of parts that share implicit state (Tabs, Accordion, Select) | Implemented with context; clean consumer API |
| Controlled / uncontrolled | Inputs and widgets | Controlled = parent owns state; uncontrolled = internal state with optional initial value |
| Provider / Context | Low-frequency, widely needed data (theme, auth, locale) | Split contexts; avoid for fast-changing state |
| Container / Presentational | Separating data from UI | Mostly replaced by hooks, still a useful mental model |
| Render props | Passing render control to a consumer | Largely replaced by hooks; still useful for headless components |
| Higher-order component | Cross-cutting concerns in legacy code | Prefer hooks; know HOCs because legacy code uses them |
| State reducer | Letting consumers customize state transitions | Powerful for reusable widgets |
| Props getters | Headless UI that returns props to spread | Used by libraries like Downshift |
| Headless component | Behavior and accessibility without styling | Radix, React Aria, Headless UI |
| Polymorphic `as` prop | One component rendered as different elements | Type it carefully |
| Portal | Modals, tooltips, dropdowns | Escapes overflow and stacking issues |
| Error boundary | Isolating render failures | See section 14 |
| Lazy + Suspense | Code splitting and loading states | Routes and heavy widgets |
| Optimistic UI | Making mutations feel instant | RTK Query `onQueryStarted` |
| Observer | Subscribing to external stores | `useSyncExternalStore`; Redux does this internally |
| Adapter | Old API shape to new shape | `transformResponse`, legacy shims (section 22) |
| Facade | Hiding a complex subsystem behind one simple API | Your typed API layer or a feature hook |
| Strategy | Swapping behavior by prop or config | Validators, formatters, sort functions |
| Factory | Producing components or variants | `cva` variants, form field factories |
| Command | Actions as data (undo/redo, queues) | Redux actions are commands |
| Mediator | Decoupling parts through a hub | Store, event bus (use sparingly) |
| Chain of responsibility | Middleware | Redux middleware, `baseQuery` wrappers |
| State machine | Complex flows with defined states and transitions | XState or a reducer with a status field |
| Repository | Hiding data access behind an interface | Your API layer; easy to mock in tests |
| Dependency injection | Testability | Pass services via props or context |
| Singleton | One shared instance | Store, query client; avoid hidden global state |
| Memoization / Flyweight | Avoiding repeated work | `memo`, selectors, virtualization |

**Compound component example**

```tsx
const TabsContext = createContext<{ active: string; setActive: (id: string) => void } | null>(null);

function Tabs({ defaultTab, children }: { defaultTab: string; children: ReactNode }) {
  const [active, setActive] = useState(defaultTab);
  return <TabsContext.Provider value={{ active, setActive }}>{children}</TabsContext.Provider>;
}

function Tab({ id, children }: { id: string; children: ReactNode }) {
  const ctx = useContext(TabsContext);
  if (!ctx) throw new Error('Tab must be used inside Tabs');
  return <button role='tab' aria-selected={ctx.active === id} onClick={() => ctx.setActive(id)}>{children}</button>;
}

Tabs.Tab = Tab;
```

**Anti-patterns**

- Prop drilling through many layers; one giant context that re-renders everything; derived state in `useState`; index keys on dynamic lists; boolean-prop explosion (`isPrimary isLarge isRounded isOutlined`); premature abstraction; components defined inside components; effects used to sync state that could be derived; copying server data into Redux.
