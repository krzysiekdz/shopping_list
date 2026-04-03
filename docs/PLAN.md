# 📋 Application Development Plan: Shopping Lists (Draft)

*Draft document — the schedule and scope of stages may change.*

An intelligent mobile app for managing shopping lists and household inventory with usage prediction.

## 🛠 Tech Stack
- **Frontend:** Flutter + BLoC (State Management - strictly no Cubit)
- **Backend:** Firebase (Auth, Firestore, Storage)
- **Architecture:** Clean Architecture (Feature-driven: domain, data, presentation)
- **Helper libraries:** fpdart (Either), freezed, json_serializable, hydrated_bloc
- **Language:** UI entirely in Polish

---

## 🚀 Stage 1: Foundation (MVP)
*Goal: a working shopping list with cloud synchronization.*

- [ ] **Firebase setup:** Initialize the project, Firebase Auth, and Firestore.
- [ ] **Auth module:** Sign in with Google and Email/Password (Firebase Auth).
- [ ] **Shared lists:** Create, edit, and delete shopping lists (Firestore).
- [ ] **Product management:** Add items to the list and define quantities.
- [ ] **Shop mode (Tryb Sklepowy):** Mark bought items (flag `isBought`) and move them to the bottom.
- [ ] **Offline First:** Implement `hydrated_bloc` for shopping lists to reduce Firebase reads.

---

## 🏠 Stage 2: Home Management (Inventory - Zapasy)
*Goal: control the state of products across different parts of the home.*

- [ ] **Locations:** Allow defining custom locations (e.g. Fridge (Lodówka), Freezer (Zamrażarka), Pantry (Spiżarnia), Garage).
- [ ] **Inventory (Magazyn):** Automatically move products from the shopping list to inventory after they are marked as "bought".
- [ ] **Quantity statuses:** Visualize inventory states (Full, Half, Running low, Out).
- [ ] **Categorization:** Group products by location (e.g. Dairy (Nabiał), Meat (Mięso), Chemicals (Chemia)).

---

## 🧠 Stage 3: Intelligence & Usage Prediction
*Goal: automate inventory monitoring without requiring user input.*

- [ ] **Family profile:** Store household size as a base usage multiplier.
- [ ] **Usage Bar algorithm (Pasek zużycia):** Implement a visual bar (0-100%) that decreases daily based on:
    - Average usage rate for a given family type.
    - Historical data (time between purchases of the same product).
- [ ] **Smart notifications:** Suggest adding a product to the list when prediction indicates level < 20%.
- [ ] **Purchase history:** Archive prices and dates for spending analysis (year over year).

---

## 🤖 Stage 4: AI Extensions (vision / later scope)
*Goal: use AI to speed up data entry.*

- [ ] **Receipt scanning:** OCR (Google ML Kit/Gemini) extracting product names and prices directly into the database.
- [ ] **Voice assistant:** Quick dictation of the shopping list ("Add milk to the current list").
- [ ] **Promotions module:** (experimental) An offers aggregator from popular retailers tailored to missing inventory.

---

## ☕ Stage 5: UX & Community
*Goal: finalize the look and a support system.*

- [ ] **"Buy a Coffee" model (Kup Kawę):** Integrate a donate button for optional contributions (e.g. Buy Me a Coffee / Stripe).
- [ ] **Material 3:** Fully refine UI/UX according to the latest Google guidelines.
- [ ] **Dark Mode:** Support the dark theme.

---

## 🚩 Key Technical Challenges
1. **Firestore optimization:** Strict control of reads (50k/day limit), avoid excessive `snapshots()`.
2. **Sync Inventory (Zapasy) <-> List:** Automatically refill inventory after closing a shopping list.
3. **Privacy:** Secure Firestore (Rules) isolating data between different families.

---

## Related Documentation
- [FIRESTORE_SCHEMA.md](FIRESTORE_SCHEMA.md) — schema and Firestore path conventions
- [AGENTS.md](AGENTS.md) — AI agent roles for Cursor
