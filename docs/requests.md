# Request Schemas

This reference details the required and optional fields for `POST` (Creation) and `PUT/PATCH` (Update) operations.

## Common Validation Rules

- **required**: Field must be present and not empty.
- **sometimes**: Field is validated only if present.
- **exists:table,column**: Value must exist in the database.
- **unique:table,column**: Value must not already exist in the database.
- **in:foo,bar**: Value must be one of the listed options.

---

## Users

### Create User (`POST /signup`)
See [Authentication](authentication.md#sign-up).

### Update User (`PUT/PATCH /users/{id}`)
*No strict validation rules defined in middleware. Standard user fields are accepted.*

---

## Loads

### Create Load (`POST /loads`)

| Field | Rules | Description |
| :--- | :--- | :--- |
| `owner_id` | `required`, `exists:users,id` | ID of the shipper. |
| `vehicle_id` | `nullable` | Specific vehicle assignment. |
| `description` | `nullable`, `string` | Details about the cargo. |
| `pick_lat` | `float` | Pickup Latitude. |
| `pick_lng` | `float` | Pickup Longitude. |
| `drop_lat` | `float` | Drop-off Latitude. |
| `drop_lng` | `float` | Drop-off Longitude. |
| `weight` | `numeric` | Cargo weight (kg/tons). |
| `price` | `numeric` | Offered price. |

### Update Load (`PUT /loads/{id}`)
**Method: PUT (Replace)** - All fields required.
**Method: PATCH (Modify)** - All fields optional (`sometimes`).

| Field | Rules |
| :--- | :--- |
| `description` | `string`, `max:255` |
| `visible_hours` | `string` |
| `amount` | `string` |
| `weight` | `string` |
| `total_amount` | `string` |
| `vehicle_id` | `string` |
| `material_name` | `string` |
| `owner_id` | `string` |
| `status` | `in:pending,accepted,rejected,in_progress,completed,cancelled` |
| `pickup_point` | `string` |
| `pick_name` | `string` |
| `pick_mobile` | `string` |
| `pick_state_id` | `string` |
| `pick_lat` | `string` |
| `pick_lng` | `string` |
| `drop_point` | `string` |
| `drop_name` | `string` |
| `drop_mobile` | `string` |
| `drop_state_id` | `string` |
| `drop_lat` | `string` |
| `drop_lng` | `string` |

---

## Bids

### Create Bid (`POST /bids`)

| Field | Rules |
| :--- | :--- |
| `load_id` | `required`, `exists:loads,id` |
| `owner_id` | `required`, `exists:users,id` |
| `amount` | `required`, `numeric` |
| `available_date` | `required`, `date_format:d/m/Y` |
| `status` | `required`, `in:pending,accepted,rejected` |

### Update Bid (`PUT/PATCH /bids/{id}`)

| Field | Rules |
| :--- | :--- |
| `amount` | `sometimes`, `numeric` |
| `available_date` | `sometimes`, `date_format:d/m/Y` |
| `status` | `sometimes`, `in:pending,accepted,rejected` |

---

## Vehicles (Lorries)

### Create Lorry (`POST /lorries`)

| Field | Rules |
| :--- | :--- |
| `owner_id` | `required`, `exists:users,id` |
| `lorry_no` | `required`, `unique:lorries,lorry_no` |
| `vehicle_id` | `required` |
| `weight` | `required`, `numeric` |
| `size` | `required`, `numeric` |
| `curr_state_id` | `required`, `exists:states,id` |
| `description` | `nullable` |
| `routes` | `sometimes` |
| `curr_location` | `nullable` |
| `status` | `boolean` |

### Update Lorry (`PUT/PATCH /lorries/{id}`)

| Field | Rules |
| :--- | :--- |
| `owner_id` | `sometimes`, `exists:users,id` |
| `lorry_no` | `sometimes`, `unique:lorries,lorry_no` |
| `weight` | `sometimes`, `numeric` |
| `size` | `sometimes`, `numeric` |
| `curr_state_id` | `sometimes`, `exists:states,id` |
| `status` | `boolean` |

---

## Documents

### Create Document (`POST /documents`)

| Field | Rules |
| :--- | :--- |
| `user_id` | `required`, `exists:users,id` |
| `file` | `required`, `file`, `mimes:jpg,png,pdf,doc`, `max:2048` |
| `description` | `nullable` |

### Update Document (`PUT/PATCH /documents/{id}`)

| Field | Rules |
| :--- | :--- |
| `user_id` | `required`/`sometimes` |
| `description` | `nullable`/`sometimes` |
| `file_path` | `required`/`sometimes` |

---

## Load Movers

### Create/Update (`POST/PUT/PATCH`)

| Field | Rules |
| :--- | :--- |
| `user_id` | `required` (or `sometimes` on PATCH) |
| `load_id` | `required` (or `sometimes` on PATCH) |

---

## Wallets

### Create Wallet (`POST /wallet`)

| Field | Rules |
| :--- | :--- |
| `user_id` | `required`, `exists:users,id` |
| `balance` | `required`, `numeric`, `min:0` |

### Update Wallet (`PATCH /wallet_up` / `/wallet_down`)

| Field | Rules |
| :--- | :--- |
| `balance` | `required`, `numeric`, `min:0` |
| `method` | `required`, `string` |

---

## Locations

### Countries

| Field | Rules |
| :--- | :--- |
| `country_name` | `required` |
| `country_code` | `required`, `max:10` |
| `mobile_prefix` | `required`, `max:10` |
| `isActive` | `required`, `boolean` |

### Communes

| Field | Rules |
| :--- | :--- |
| `state_id` | `required`, `exists:states,id` |
| `commune_name` | `required` |
| `commune_code` | `required`, `unique:communes` |

### Points

| Field | Rules |
| :--- | :--- |
| `lat` | `required`, `numeric` |
| `lang` | `required`, `numeric` |
| `person_name` | `required` |
| `person_mobile` | `required` |

---

## System

### Notifications

| Field | Rules |
| :--- | :--- |
| `notification_type` | `required`, `in:fail,success,info,warning` |
| `description` | `required` |
| `user_id` | `required`, `exists:users,id` |
| `is_read` | `boolean` |

### Reviews

| Field | Rules |
| :--- | :--- |
| `rate_number` | `required` |
| `rate_text` | `nullable` |
