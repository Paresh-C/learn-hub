## 13. MV\* patterns (MVC, MVP, MVVM, Flux)

All of these separate **what the app knows** (model), **what the user sees** (view), and **the glue** between them.

| Pattern | Roles | Data flow | Typical use |
| --- | --- | --- | --- |
| MVC | Model holds data and rules; View renders; Controller handles input and updates the model | Input goes to Controller, then Model, then View reads Model | Server frameworks (Rails, Spring), classic web |
| MVP | Presenter holds all UI logic; View is passive and dumb | View calls Presenter, which updates Model and tells View what to show | Android, older desktop UIs; very testable |
| MVVM | ViewModel exposes state and commands; View binds to it | Two-way (or reactive) binding between View and ViewModel | Angular, Vue, WPF, SwiftUI |
| Flux / Redux | Actions, dispatcher/store, reducers, views | Strictly one-way: View, Action, Reducer, Store, View | React + Redux / RTK |
| MVU (Elm) | Model, Update, View | One-way; update is a pure function | Elm, some React reducer designs |
| MVI | Intent, Model, View | One-way, immutable state per intent | Android, reactive apps |

**How this maps to your React + RTK app**

- **View:** React components (as dumb and declarative as reasonable).
- **ViewModel-like layer:** custom hooks (`useCheckoutForm`, `useOrderList`) that expose the state and handlers a component needs.
- **Model:** types, pure domain functions (pricing, permissions, validation), and the cached server state in RTK Query.
- **Controller-like flow:** event handlers, thunks, listener middleware, and RTK Query mutations.
- **Flux idea:** data flows one way: user event, action or mutation, store update, re-render. This predictability is the main reason RTK works well.

**Take-aways:** React is one-way and view-focused, so you rarely need classic MVC. Keep the view thin, put logic in hooks and pure functions, keep server state in RTK Query, and keep side effects out of components.
