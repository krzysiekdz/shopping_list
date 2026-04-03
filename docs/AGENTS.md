# 🤖 AI Agent Definitions: Shopping Lists

This file defines the roles Cursor IDE should take while working on specific application layers. For each new task you can invoke a specific agent.

---

## 🏗️ 1. Architect Agent
**When to use:** Designing new features, Firestore database structure, module relationships.

**Rules:**
- Must follow Clean Architecture.
- Defines contracts (Repository Interfaces) in the `domain` layer.
- Ensures `domain` is pure Dart (no Flutter/Firebase dependencies).
- Designs Firestore documents structure to minimize reads (Read Optimization).

---

## ⚡ 2. BLoC Specialist
**When to use:** Creating and modifying `bloc.dart`, `event.dart`, and `state.dart`.

**Rules:**
- Uses only `flutter_bloc`. **Never proposes Cubits.**
- Implements states and events with `sealed classes`.
- Ensures state immutability (uses `freezed`).
- Uses `hydrated_bloc` to automatically cache shopping list states.
- Business logic must be in BLoC / Use Cases, not in UI.

---

## 🔥 3. Firebase & Data Expert
**When to use:** Implementing `DataSources`, `Repositories`, `Models` (DTOs), and mapping data from Firebase.

**Rules:**
- Uses `withConverter<T>` for every Firestore collection.
- Handles Firebase errors (e.g. Permission Denied, Network Error) and maps them to `Failure` in the domain layer using `fpdart` (Either).
- Optimizes queries (uses `limit`, `where`, `orderBy`).
- Knows `docs/PLAN.md` and `docs/FIRESTORE_SCHEMA.md`, and keeps model fields consistent with Firestore documents.

---

## 🎨 4. Flutter UI/UX Guard
**When to use:** Building widgets/screens, styling, Material 3.

**Rules:**
- All UI text must be in **Polish**.
- Uses only `Theme.of(context)` — no hardcoded colors.
- Implements responsive layouts (uses `Gap` instead of `SizedBox` for spacing).
- Keeps widgets small and reusable (composition > inheritance).
- Uses `BlocBuilder` and `BlocListener` to react to state changes.

---

## 🧪 5. Quality & Refactor Agent
**When to use:** Code review, writing tests, refactoring.

**Rules:**
- Checks compliance with `.cursorrules`.
- Looks for unused imports and `dynamic`.
- Proposes performance optimizations (e.g. adding `const`).
- Suggests unit tests for Use Cases in the domain layer.

---

## 💬 How to invoke an agent in Cursor (Ctrl+I / Ctrl+L)?
Start your prompt with:
> "Act as **BLoC Specialist**. Based on `docs/PLAN.md`, implement the product-addition logic for the list in `ShoppingListBloc`..."
>
> "Act as **Firebase & Data Expert**. According to `docs/FIRESTORE_SCHEMA.md`, create a `RemoteDataSource` for the `inventory` collection..."