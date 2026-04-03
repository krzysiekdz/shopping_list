# Firestore Database Schema: Shopping Lists

## Path conventions
- **`users/{userId}`** — document ID **equal** to the Firebase Auth UID. If your model has an `id` field, it should match `userId` (avoid mismatches with Security Rules).
- **`shopping_lists/{listId}`** — list document; items live in the subcollection below.
- **`shopping_lists/{listId}/items/{itemId}`** — shopping list items subcollection.
- **`inventory/{docId}`**, **`locations/{docId}`** — documents with a `userId` field (or an ownership relation) according to security rules.

## Collection: `users`
- `id`: String (Firebase Auth UID; typically the same as the document ID)
- `email`: String
- `familySize`: Int (default 1)
- `createdAt`: Timestamp

## Collection: `shopping_lists`
- `id`: String
- `name`: String
- `ownerId`: String (relation to `users`)
- `sharedWith`: Array<String> (list of collaborator UIDs)
- `createdAt`: Timestamp

### Subcollection: `items` (inside a list document)
- `id`: String
- `name`: String
- `category`: String
- `amount`: Double
- `unit`: String (szt, kg, l)
- `isBought`: Boolean
- `addedAt`: Timestamp

## Collection: `inventory`
- `id`: String
- `userId`: String
- `locationId`: String
- `productName`: String
- `currentQuantity`: Double **from 0.0 to 1.0** — **normalized inventory level** (e.g. 1.0 = full, 0.0 = out), not an absolute amount in unit terms (kg, pcs). The usage bar and statuses from `docs/PLAN.md` (Stages 2–3) operate on this scale. If the UI needs a “physical” amount, convert from other fields or from a baseline unit defined for the product.
- `dailyUsageRate`: Double (e.g. 0.05)
- `lastUpdatedAt`: Timestamp

## Collection: `locations`
- `id`: String
- `userId`: String
- `name`: String (e.g. Fridge (Lodówka))
- `icon`: String