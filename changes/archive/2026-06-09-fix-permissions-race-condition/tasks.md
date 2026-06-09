## 1. Context Update

- [x] 1.1 Remove `permissions` state variable (`useState`) and `useEffect` hook from `PermissionsContext.jsx`.
- [x] 1.2 Derive `permissions` directly from `user?.permissions || {}` inside `PermissionsProvider`.
