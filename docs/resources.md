# Resources

Access and manage the entities of the Smart Cargo platform.

## Common Parameters

Most `GET` endpoints invoke a list action and support the following query parameters:

- `page`: Page number for pagination (default: 1).
- `per_page`: Number of items per page (default: 15).
- `json`: Set to `true` or `1` to force a pure JSON response.

---

## Users

Manage user profiles.

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/users` | List all users. |
| `GET` | `/users/{id}` | Get user details. |
| `PUT` | `/users/{id}` | Update user profile. |
| `DELETE` | `/users/{id}` | Delete a user. |
| `POST` | `/profile_image_update/{id}` | Upload a new profile picture. |
| `POST` | `/users/fcm-token` | Update Firebase Cloud Messaging token. |

### Upload Profile Image

**Endpoint**: `POST /profile_image_update/{id}` (Multipart)

- `parts[]`: Array of image files.

---

## Loads

Manage cargo shipments.

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/loads` | List available loads. |
| `POST` | `/loads` | Post a new load. |
| `GET` | `/loads/{id}` | Get load details. |
| `PUT` | `/loads/{id}` | Update load. |
| `DELETE` | `/loads/{id}` | Delete load. |

**Create Body**:
```json
{
    "owner_id": 1,
    "pick_lat": 36.75, "pick_lng": 3.05,
    "drop_lat": 35.69, "drop_lng": -0.63,
    "weight": 1000,
    "price": 5000,
    "description": "Furniture"
}
```

---

## Bids

Manage bids placed on loads.

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/bids` | List bids. |
| `POST` | `/bids` | Place a bid. |
| `GET` | `/bids/{id}` | Get bid details. |
| `PUT` | `/bids/{id}` | Update bid. |
| `DELETE` | `/bids/{id}` | Withdraw bid. |

**Create Body**:
```json
{
    "load_id": 10,
    "owner_id": 2,
    "amount": 4500,
    "available_date": "15/01/2026",
    "status": "pending"
}
```

---

## Lorries (Vehicles)

Manage the detailed fleet of lorries/trucks.

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/lorries` | List lorries. |
| `POST` | `/lorries` | Register a new lorry. |
| `GET` | `/lorries/{id}` | Get details. |
| `PUT` | `/lorries/{id}` | Update details. |
| `DELETE` | `/lorries/{id}` | Delete lorry. |
| `GET` | `/lorries/getLorryList/{owner_id}/{load_id}` | Get available lorries for a specific load. |

**Create Body**:
```json
{
    "owner_id": 1,
    "lorry_no": "ABC-123-DZ",
    "vehicle_id": "truck_01",
    "weight": 5000,
    "size": 20,
    "curr_state_id": 5,
    "description": "Optional description"
}
```

---

## Wallet

Manage user balances and transactions.

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/wallet` | List wallets. |
| `POST` | `/wallet` | Create wallet. |
| `GET` | `/wallet/{id}` | Get wallet (includes transactions). |
| `PATCH` | `/wallet_up/{id}` | Add funds. |
| `PATCH` | `/wallet_down/{id}` | Deduct funds. |

**Modify Balance Body** (`PATCH`):
```json
{
    "balance": 1000,
    "method": "paypal"
}
```

---

## Locations

### Countries
Base endpoint: `/countries`

**Create Fields**:
- `country_name` (string)
- `country_code` (string, e.g., "DZ")
- `mobile_prefix` (string, e.g., "+213")
- `isActive` (boolean)

### States
Base endpoint: `/states`

**Custom**: `POST /states/getStatesId`
- Body: `{"drop_state_name": "Oran", "pick_state_name": "Algiers"}`
- Returns: IDs for the states.

### Communes
Base endpoint: `/communes`

**Create Fields**:
- `state_id` (exists in states)
- `commune_name`
- `commune_code` (unique)

### Points
Address points or landmarks.
Base endpoint: `/points`

**Create Body**:
```json
{
    "lat": 36.75,
    "lang": 3.05,
    "person_name": "Contact Name",
    "person_mobile": "0550000000"
}
```

---

## Reviews

Manage user ratings and reviews.
Base endpoint: `/reviews`

**Create Body**:
```json
{
    "rate_number": 5,
    "rate_text": "Great service!",
    "user_id": 2
}
```

---

## Notifications

System notifications for users.
Base endpoint: `/notifications`

**Create Body**:
```json
{
    "user_id": 1,
    "notification_type": "info",
    "description": "Your load has been delivered.",
    "is_read": false
}
```
**Types**: `fail`, `success`, `info`, `warning`
