# 03 — API Testing

Documentation and test cases for API validation using Postman, covering functional, negative, and performance testing of REST API endpoints.

---

## Tools Used

| Tool | Purpose |
|---|---|
| **Postman** | API request execution, response validation, collection management |
| **Charles Proxy** | Network traffic inspection, request/response monitoring on mobile |
| **Fiddler** | HTTP/HTTPS traffic debugging on web platforms |

## What I Test in APIs

1. **Status Code Validation** — Correct HTTP status codes for each scenario (200, 201, 400, 401, 403, 404, 500)
2. **Response Payload Structure** — Required fields present, correct data types, no null values where unexpected
3. **Authentication** — Valid token accepted, expired/missing token rejected with correct error
4. **Error Handling** — Meaningful error messages returned for invalid inputs
5. **Data Integrity** — Response data matches what was submitted / matches database state
6. **Performance Under Throttling** — API behavior under slow network conditions (Slow 3G simulation)

---

# API Test Cases

## Endpoint Group 1: Miniapp Launch API

**Base URL:** `https://api.[platform].id/v1` *(anonymized)*  
**Authentication:** Bearer Token (passed from host app)

---

### TC-API-001 — Successful Miniapp Launch

| Field | Detail |
|---|---|
| **Endpoint** | `POST /miniapp/launch` |
| **Auth** | Bearer Token (valid) |
| **Scenario** | Launch Miniapp with valid user token |

**Request Body:**
```json
{
  "miniapp_id": "ayolari",
  "user_id": "USR-12345",
  "platform": "android",
  "app_version": "3.4.2"
}
```

**Expected Response — 200 OK:**
```json
{
  "status": "success",
  "data": {
    "miniapp_url": "https://miniapp.ayolari.id/launch?token=...",
    "session_id": "SES-abc123",
    "expires_at": "2026-04-30T12:30:00Z",
    "user_context": {
      "user_id": "USR-12345",
      "name": "Olsen Test",
      "tier": "premium"
    }
  }
}
```

**Validation Checklist:**
- [x] Status code is `200`
- [x] `miniapp_url` is present and is a valid URL
- [x] `session_id` is present and non-empty
- [x] `expires_at` is a valid ISO 8601 timestamp
- [x] `user_context.user_id` matches the request `user_id`
- [x] Response time < 2000ms

---

### TC-API-002 — Launch Without Auth Token

| Field | Detail |
|---|---|
| **Endpoint** | `POST /miniapp/launch` |
| **Auth** | No token (header omitted) |
| **Scenario** | Verify unauthorized access is rejected |

**Expected Response — 401 Unauthorized:**
```json
{
  "status": "error",
  "error": {
    "code": "UNAUTHORIZED",
    "message": "Authentication token is missing or invalid."
  }
}
```

**Validation Checklist:**
- [x] Status code is `401`
- [x] Response body contains `error.code` = `"UNAUTHORIZED"`
- [x] No `miniapp_url` or user data exposed in error response

---

### TC-API-003 — Launch With Expired Token

| Field | Detail |
|---|---|
| **Endpoint** | `POST /miniapp/launch` |
| **Auth** | Bearer Token (expired) |
| **Scenario** | Verify expired token is rejected with correct message |

**Expected Response — 401 Unauthorized:**
```json
{
  "status": "error",
  "error": {
    "code": "TOKEN_EXPIRED",
    "message": "Your session has expired. Please log in again."
  }
}
```

**Validation Checklist:**
- [x] Status code is `401`
- [x] Error code is specifically `TOKEN_EXPIRED` (distinguishable from missing token)
- [x] No sensitive data leaked in error response

---

### TC-API-004 — Launch With Invalid Miniapp ID

| Field | Detail |
|---|---|
| **Endpoint** | `POST /miniapp/launch` |
| **Auth** | Bearer Token (valid) |
| **Scenario** | Verify non-existent miniapp returns 404 |

**Request Body:**
```json
{
  "miniapp_id": "nonexistent_app",
  "user_id": "USR-12345",
  "platform": "android"
}
```

**Expected Response — 404 Not Found:**
```json
{
  "status": "error",
  "error": {
    "code": "MINIAPP_NOT_FOUND",
    "message": "The requested miniapp does not exist."
  }
}
```

---

## Endpoint Group 2: Content Fetch API

---

### TC-API-010 — Fetch Homepage Content (Success)

| Field | Detail |
|---|---|
| **Endpoint** | `GET /miniapp/content?miniapp_id=ayolari&section=home` |
| **Auth** | Bearer Token (valid) |
| **Scenario** | Fetch homepage content sections |

**Expected Response — 200 OK:**
```json
{
  "status": "success",
  "data": {
    "sections": [
      {
        "id": "banner",
        "type": "carousel",
        "items": [
          {
            "id": "item-001",
            "title": "Promo Title",
            "thumbnail_url": "https://cdn.example.com/img.jpg",
            "deeplink": "ayolari://promo/001"
          }
        ]
      }
    ],
    "total_sections": 3
  }
}
```

**Validation Checklist:**
- [x] Status code is `200`
- [x] `sections` is an array with at least 1 item
- [x] Each item contains `id`, `title`, `thumbnail_url`, `deeplink`
- [x] `thumbnail_url` is a valid HTTPS URL
- [x] Response time < 1500ms on standard connection

---

### TC-API-011 — Fetch Content Under Slow Network

| Field | Detail |
|---|---|
| **Endpoint** | `GET /miniapp/content` |
| **Network** | Throttled to Slow 3G via Charles Proxy |
| **Scenario** | Verify API behaves gracefully under poor network |

**Expected Behavior:**
- Response still returns `200` (may take longer)
- No timeout error before 10 seconds
- App displays loading state while waiting
- Content renders correctly once received

---

## API Testing Notes

- All API tests executed via **Postman** with environment variables for base URL and auth tokens
- Network throttling simulated via **Charles Proxy** to test slow-connection behavior
- Response validation includes both structure (keys present) and data type checks
- Error response messages validated verbatim to ensure developer-friendly error communication

---

> **Note:** All endpoints, URLs, and data shown are anonymized/simulated versions based on real API testing work.
