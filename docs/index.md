# Smart Cargo API Documentation

Welcome to the **Smart Cargo API** documentation. This API allows you to manage users, shipments (`loads`), vehicles (`lorries`), and more for the Smart Cargo platform.

**Project Repository:** [Peak-Soft/Smart-Cargo-BackOffice](https://github.com/Peak-Soft/Smart-Cargo-BackOffice)

## Base URL

All endpoints are prefixed with `/v1`.

```
http://api.smartcargo.com/v1
```

*(Replace `api.smartcargo.com` with your actual domain)*

## Authentication

The API uses **Laravel Sanctum** for authentication.

### sending the Token

To access protected endpoints, you must include the `Authorization` header with a valid Bearer token.

```http
Authorization: Bearer <your_token>
Accept: application/json
```

### Getting a Token

You can obtain a token by logging in via the [`/tokens`](authentication.md#login) endpoint.

## Response Format

The API generally uses a standard unified response format:

```json
{
  "data": { ... },
  "message": "Operation successful",
  "status": 200
}
```

- **data**: The requested resource or result object.
- **message**: A human-readable message describing the result.
- **status**: The HTTP status code (mirrored).
