# Utilities

Helper endpoints for public data and services.

## Geography

### Get Countries

List available countries for registration/service.

`GET /get_countries`

### Places Autocomplete

Search for addresses and coordinates (powered by OpenStreetMap).

`GET /places/autocomplete?query={search_term}`

**Example**:
`/places/autocomplete?query=Algiers`

**Response**:
```json
[
    {
        "name": "Algiers, Algeria",
        "lat": "36.7525",
        "lon": "3.04197",
        "type": "city",
        "address": { ... }
    }
]
```

---

## Payments

### Get Payment Methods

List supported payment gateways and methods.

`GET /payments`

**Response Example**:
```json
{
    "data": [
        {
            "id": "1",
            "title": "Paypal",
            "status": "1"
        },
        {
            "id": "5",
            "title": "Cash On Delivery",
            "status": "1"
        }
    ],
    "message": "Payments retrieved successfully",
    "status": 200
}
```

---

## Help

### FAQ

Retrieve Frequently Asked Questions.

`GET /help/faq`
