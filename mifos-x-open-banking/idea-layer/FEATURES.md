# mifos-x-open-banking — Features

> Auto-generated from `idea-plan.yaml` §features + §requirements + §screens + §flows on 2026-05-20.
> Edit `idea-plan.yaml` and run `/idea sync` to regenerate.

| Feature | Priority | Maturity | Screens | Requirements |
|---|---|---|---|---|
| [home](#home) | must | production | TasksList · EditTask | FR-001…FR-005 |
| [profile](#profile) | should | stub | Profile | — |
| [settings](#settings) | should | partial | Settings · Notification | FR-006 |

---

## home

> 🟢 **production** — the core feature of the app, fully implemented.

TaskMinder core — displays task list with calendar-based date filtering (year/month/day pickers), task creation/editing, completion tracking, and priority visualization.

### Screens

#### `TasksList` (dashboard)
Primary entry point. Calendar pickers at the top let you slice tasks by year → month → day. Tasks render in a `LazyColumn` with checkbox + delete actions. FAB launches `EditTask` in create mode.

**State**: `TasksViewModel` (MVI) · 5 actions · 2 events · states `Loading | Empty | Success`
**Data**: `StorageService.{getTasksByDate, updateTask, deleteTask}`

#### `EditTask` (form)
Create or edit a single task. Fields: title, description, priority (`FilterChip` low/med/high), due date (`DatePickerDialog`), due time (`TimePicker`). Save persists via `StorageService`; cancel shows `AlertDialog` to confirm discard.

**State**: `EditTaskViewModel` (MVI) · 7 actions · 1 event · states `Loading | Empty | Success`
**Data**: `StorageService.{addTask, updateTask, getTaskById}`

### Requirements

| ID | Description | Source |
|---|---|---|
| **FR-001** | User can create a new task with title, description, priority, and due date/time via EditTask. | `task/EditTaskViewModel.kt:95-110` |
| **FR-002** | User can view all tasks for a selected calendar date in a filterable list. | `tasks/TasksViewModel.kt:75-88` |
| **FR-003** | User can toggle task completion via checkbox; state persists. | `tasks/TasksScreen.kt:125-140` |
| **FR-004** | User can delete a task. | `tasks/TasksViewModel.kt deleteTask` |
| **FR-005** | User can filter tasks by year/month/day via interactive picker UI. | `tasks/TasksViewModel.kt:100-125` |

### Flows

- **create_task_flow**: TasksList → tap FAB → EditTask form → Save → StorageService.addTask → back to TasksList with new task
- **filter_tasks_by_date_flow**: TasksList → pick year/month/day → TasksFlow filters → LazyColumn updates
- **mark_task_complete_flow**: TasksList → tap checkbox → flagTask → StorageService.updateTask → visual update

---

## profile

> ⚪ **stub** — placeholder scaffold, no ViewModel yet.

User profile dashboard. Currently a static Compose screen with no state. Designed to integrate with user account / preference data.

### Screens

#### `Profile` (profile archetype)
**Composition**: `KptScaffold` · `Column` · `Text`
**State**: stateless — no ViewModel
**Data**: none

### Next steps (recommended before /kmp-implement)

- [ ] Define profile data model + persistence
- [ ] Add `ProfileViewModel` with state for `{avatar, name, email, preferences}`
- [ ] Wire avatar upload + edit-profile flow
- [ ] Approve scope via `/idea approve profile`

---

## settings

> 🟡 **partial** — Settings screen functional (theme toggle), Notification subscreen is a stub.

App settings — theme customization, notification preferences (placeholder).

### Screens

#### `Settings` (settings archetype)
Stateless. Each setting category is an `OutlinedCard` with icon + label + chevron. The theme card opens an `AlertDialog` that updates app-scope theme via `AppViewModel.updateAppTheme`.

**State**: stateless-with-dialog (theme state lives in `AppViewModel`, app-scope)
**Data**: `AppViewModel.updateAppTheme`

#### `Notification` (settings archetype)
**Composition**: `KptScaffold` · `Column` · `Text`
**State**: stateless — stub
**Data**: none

### Requirements

| ID | Description | Source |
|---|---|---|
| **FR-006** | User can toggle application theme (light/dark) via SettingsDialog. | `SettingsScreen.kt:40-70` |

### Flows

- **settings_theme_toggle_flow**: Settings → tap ThemeCard → SettingsDialog → toggle → AppViewModel.updateAppTheme → handleThemeMode → app recomposes

### Next steps

- [ ] Implement `NotificationViewModel` + `UserNotificationPreferences`
- [ ] Add settings: language, account, privacy, about
- [ ] Consider moving theme to a dedicated `SettingsViewModel` for SoC

---

## Cross-cutting

### Splash (cmp-shared, not feature-bound)
Bootstrap screen — `RootNavViewModel.bootstrap` loads theme prefs, determines initial destination, then navigates to `TasksList`. Android uses the System SplashScreen API.

### Repositories observed

| Repository | Purpose |
|---|---|
| `StorageService` (+ `StorageServiceImpl`) | Task persistence — add / update / delete / query by date |
| `UserDataRepository` | User preferences and app configuration |
| `NetworkMonitor` | Connectivity status via `Flow<Boolean>` |

### Database (Room KMP)

| Entity | Key fields |
|---|---|
| `TaskEntity` | `id`, `title`, `priority`, `dueDate`, `dueTime`, `description`, `completed`, `alert`, `userId` |
| `SampleEntity` | `id`, `name` |
