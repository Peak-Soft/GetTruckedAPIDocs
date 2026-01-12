# Authentication

Manage user access and session tokens.

## Sign Up

Register a new user account.

### Endpoint

`POST /signup`

### Request Body

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `name` | string | Yes | Full name of the user. |
| `email` | string | Yes | Valid email address. |
| `password` | string | Yes | Password for the account. |
| `type` | string | Yes | User type (e.g., `driver`, `shipper`). |
| `phone` | string | No | Contact number. |

### Example Request

```json
{
    "name": "John Doe",
    "email": "john@example.com",
    "password": "securepassword123",
    "type": "driver"
}
```

### Response

Returns the created user object and an access token.

```json
{
    "data": {
        "id": 1,
        "name": "John Doe",
        "email": "john@example.com",
        "type": "driver",
        "token": "1|laravel_sanctum_token_string..."
    },
    "message": "user created successfuly",
    "status": 201
}
```

---

## Login (Create Token)

Authenticate a user and retrieve a personal access token.

### Endpoint

`POST /tokens`

### Request Body

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `email` | string | Yes | Registered email address. |
| `password` | string | Yes | User password. |
| `device_name`| string | No | Optional device identifier. |

### Example Request

```json
{
    "email": "john@example.com",
    "password": "securepassword123",
    "device_name": "mobile_app"
}
```

### Response

```json
{
    "data": {
        "id": 1,
        "name": "John Doe",
        "email": "john@example.com",
        "token": "2|new_token_string..."
    },
    "message": "Token created successfully",
    "status": 200
}
```

---

## Logout

Invalidate the user's current token.

### Endpoint

`POST /logout`

!!! warning "Requires Authentication"
    You must provide a valid Bearer token in the header.

### Response

```json
{
    "data": null,
    "message": "Logged out successfully",
    "status": 200
}
```
