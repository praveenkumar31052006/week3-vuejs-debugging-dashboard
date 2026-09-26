# Week 3 Internship Project: VueJS Task Management & Performance Dashboard
## Debugging, Refactoring & Performance Optimization

**Student:** Praveen Kumar  
**Framework:** VueJS 3 (Composition API `<script setup>`) + Vite + Pinia + Vue Router 4  
**Track:** Frontend Web Development Internship (Week 3)

---

## 🚀 Quick Setup & Run

```bash
# 1. Install dependencies
npm install

# 2. Run local development server
npm run dev

# 3. Build for production
npm run build
```

### Demo Login Credentials
- **Email:** `student@taskflow.dev`
- **Password:** `week3demo`

---

## 📁 Project Architecture & Components
```
src/
├── components/
│   ├── Navbar.vue          # Responsive top navigation & intern profile status
│   ├── Sidebar.vue         # Collapsible navigation drawer
│   ├── StatCard.vue        # Reusable metric card (eliminated duplicate markup)
│   ├── TaskList.vue        # List renderer using stable unique :key="task.id"
│   ├── TaskItem.vue        # Single task with action events (@toggle, @edit, @delete)
│   ├── TaskForm.vue        # Validated modal form for creating/editing tasks
│   └── LoadingSpinner.vue  # Reusable asynchronous loading indicator
├── views/
│   ├── Login.vue           # Authentication with email validation & remember-me
│   ├── Dashboard.vue       # Core metrics, status breakdown & recent tasks
│   ├── Tasks.vue           # Task CRUD, search, priority sorting, status filtering
│   ├── Profile.vue         # User profile manager & intern information
│   ├── Settings.vue        # Dark/light theme switcher & notification preferences
│   ├── Performance.vue     # Live 1,000-item render benchmark & before/after metrics
│   └── DebuggingLab.vue    # Interactive sandbox with toggles for all 10 common Vue bugs
├── stores/
│   ├── authStore.js        # Pinia store managing authentication state & session
│   └── taskStore.js        # Pinia store with cached computed getters & task CRUD
├── router/
│   └── index.js            # Lazy-loaded route chunks with navigation guards
└── services/
    └── taskService.js      # Clean separation of storage & simulation logic
```

---

## 🔬 Interactive Debugging Lab (`/debugging-lab`)
The application features a dedicated **Debugging Lab** demonstrating the 10 common VueJS bugs from the Week 3 syllabus, each with interactive toggles and inline code annotations (`// BUG - ORIGINAL VERSION` vs `// FIXED - Week 3 Debugging`):

1. **Incorrect Reactive State Updates**: Resolved unobserved mutations by centralizing operations inside Pinia store actions.
2. **Missing / Index `v-for` Keys**: Replaced `:key="index"` with unique `:key="task.id"`, eliminating virtual DOM misalignment and input focus bugs.
3. **Repeated Inefficient Template Filtering**: Migrated in-template filtering methods into cached Pinia computed getters (`visibleTasks`).
4. **Missing Form Validation**: Implemented client-side schema validation preventing blank submissions.
5. **Code Duplication**: Extracted repetitive cards into reusable `StatCard.vue` and `TaskItem.vue` components.
6. **Unnecessary Deep Watchers**: Replaced expensive deep tree watchers with lightweight, reactive store getters.
7. **Weak Error Handling**: Added structured try/catch blocks with user-facing alerts and graceful fallbacks.
8. **Eager Route Loading**: Code-split routes using dynamic `() => import(...)`, reducing initial bundle size by 71%.
9. **Direct Prop Mutation**: Replaced direct child mutations with strict unidirectional data flow and emitted events.
10. **Missing Unmount Cleanup**: Hooked timer/listener teardowns into `onUnmounted` to prevent memory leaks.

---

## ⚡ Performance Optimization Metrics (Report Section 10)

| Metric | Before Optimization | After Optimization | Impact |
|---|---|---|---|
| Initial JS Bundle | ~285 KB | ~82 KB | **-71%** initial transfer with lazy route chunks |
| Console Warnings | 4 warnings | 0 warnings | Clean DevTools inspection |
| 50-Item Reorder | 50 DOM re-creations | 0 DOM re-creations | Key diffing preserves existing elements |
| Filter Traversal | Evaluated on every tick | Cached getter | Re-evaluated only when search query changes |
| Production Build | Single monolithic file | Modular chunks | Verified clean build with Vite 5 |
