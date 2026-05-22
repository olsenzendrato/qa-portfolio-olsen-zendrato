# 03 — API Testing

API test documentation based on real REST API validation work performed using Postman at PT Indonesia Satu Tujuh. This folder covers endpoint testing for the Milov application, including authentication, core features, and data retrieval flows.

---

## Tools Used

| Tool | Purpose |
|---|---|
| **Postman** | API request execution, collection management, response validation |
| **Charles Proxy** | Network traffic inspection on mobile devices; monitoring actual API calls from app |
| **Fiddler** | HTTP/HTTPS traffic debugging on web platforms |

## What I Validate in API Testing

1. **HTTP Status Codes** — Correct response codes per scenario (200, 201, 400, 401, 403, 404, 500)
2. **Response Payload Structure** — All required fields present, correct data types, no unexpected null values
3. **Authentication** — Bearer token accepted for valid sessions; rejected with correct error for missing/expired tokens
4. **Error Handling** — Meaningful, structured error responses for invalid inputs
5. **Data Integrity** — Response data matches what was submitted and/or matches database state
6. **Pagination** — Correct page/limit behavior; no duplicate or missing items across pages
7. **Network Behavior** — API responses under throttled network conditions (via Charles Proxy)

---

# API Test Cases — Milov Application

**Project:** Milov — Fun Love Match Game App  
**Base URL:** `https://staging.milov.id/go` *(staging environment, anonymized)*  
**Testing Date:** February 26–27, 2024  
**Tester:** Olsen Yeremia Zendrato  
**Auth Type:** Bearer Token  

---

## Category 1: Authentication

### TC-API-AUTH-001 — User Login via Google

| Field | Detail |
|---|---|
| **Endpoint** | `POST /api/v1/auth/login/google` |
| **Method** | POST |
| **Body Type** | x-www-form-urlencoded |
| **Auth** | None (pre-login) |

**Request Body:**
```
access_token = [Google OAuth Token]
device_id    = [Device Build ID]
```

**Expected Response — 200 OK:**
```json
{
  "data": {
    "user_id": 282736154,
    "first_name": "string",
    "last_name": "string",
    "email": "string",
    "profile_picture_path": "https://...",
    "status": 3,
    "date_of_birth": "2024-01-24T00:00:00Z",
    "gender": "string",
    "coin": 0,
    "zodiac": "string",
    "love_language": "string",
    "is_active": false
  },
  "token": "string"
}
```

**Validation Checklist:**
- [x] Status code `200`
- [x] `data.user_id` is integer and not null
- [x] `token` is present and non-empty string
- [x] `data.email` matches the Google account used
- [x] `data.date_of_birth` is valid ISO 8601 format
- [x] Response time < 2000ms

**Status:** OK

---

### TC-API-AUTH-002 — Issue New Token

| Field | Detail |
|---|---|
| **Endpoint** | `GET /api/v1/auth/token/requestnew/{user_id}` |
| **Method** | GET |
| **Auth** | Bearer Token (existing valid token) |
| **Path Param** | `user_id` = valid integer |

**Expected Response — 200 OK:**
```json
{
  "token": "string"
}
```

**Validation Checklist:**
- [x] Status code `200`
- [x] New `token` returned, non-empty
- [x] New token is different from the one used in the request
- [x] Old token invalidated after new token issued

**Status:** OK

---

## Category 2: Hobby

### TC-API-HOBBY-001 — Get All Hobbies

| Field | Detail |
|---|---|
| **Endpoint** | `GET /api/v1/hobby` |
| **Method** | GET |
| **Auth** | Bearer Token |
| **Query Params** | `page=1`, `limit=10` |

**Expected Response — 200 OK:**
```json
{
  "data": [
    { "hobby_id": 1, "hobby_name": "memasak", "hobby_description": "" },
    { "hobby_id": 2, "hobby_name": "fotografi", "hobby_description": "" },
    { "hobby_id": 3, "hobby_name": "bersepeda", "hobby_description": "" }
  ]
}
```

**Validation Checklist:**
- [x] Status code `200`
- [x] `data` is an array
- [x] Each item contains `hobby_id` (integer), `hobby_name` (string), `hobby_description` (string)
- [x] Pagination: results ≤ `limit` value
- [x] No duplicate `hobby_id` values in response

**Status:** OK

---

## Category 3: User Profile

### TC-API-USER-001 — Get User Profile

| Field | Detail |
|---|---|
| **Endpoint** | `GET /api/v1/user/{user_id}` |
| **Method** | GET |
| **Auth** | Bearer Token |

**Expected Response — 200 OK:**
```json
{
  "data": {
    "user_id": "integer",
    "first_name": "string",
    "last_name": "string",
    "email": "string",
    "profile_picture_path": "string",
    "date_of_birth": "datetime",
    "gender": "string",
    "coin": "integer",
    "zodiac": "string",
    "shio": "string",
    "love_language": "string",
    "is_active": "boolean"
  }
}
```

**Validation Checklist:**
- [x] Status code `200`
- [x] `user_id` matches path parameter
- [x] All required fields present and non-null
- [x] `coin` is non-negative integer
- [x] `profile_picture_path` is valid HTTPS URL

**Status:** OK

---

### TC-API-USER-002 — Get Profile with Invalid Token

| Field | Detail |
|---|---|
| **Endpoint** | `GET /api/v1/user/{user_id}` |
| **Auth** | Invalid / expired Bearer Token |

**Expected Response — 401 Unauthorized:**
```json
{
  "error": "Unauthorized",
  "message": "Token is invalid or expired"
}
```

**Validation Checklist:**
- [x] Status code `401`
- [x] Error message present and descriptive
- [x] No user data exposed in error response

**Status:** OK

---

## Category 4: Match / Scan Feature

### TC-API-MATCH-001 — Scan Friend Match

| Field | Detail |
|---|---|
| **Endpoint** | `POST /api/v1/match/scan` |
| **Method** | POST |
| **Auth** | Bearer Token |

**Request Body:**
```json
{
  "target_user_id": "integer",
  "name": "string",
  "date_of_birth": "date",
  "gender": "string"
}
```

**Expected Response — 200 OK:**
```json
{
  "data": {
    "match_percentage": "integer",
    "coin_deducted": 1,
    "remaining_coin": "integer"
  }
}
```

**Validation Checklist:**
- [x] Status code `200`
- [x] `match_percentage` is integer between 0–100
- [x] `coin_deducted` = 1 (each scan costs 1 coin)
- [x] `remaining_coin` = previous coin - 1
- [x] Match result appears in Friends → Match tab after scan

**Status:** OK with Note — Match result intermittently not appearing in Friends tab (see Bug Report BUG-2024-007)

---

### TC-API-MATCH-002 — Invite Friend

| Field | Detail |
|---|---|
| **Endpoint** | `POST /api/v1/friend/invite` |
| **Method** | POST |
| **Auth** | Bearer Token |

**Expected Response — 200 OK:**
```json
{
  "status": "invited",
  "coin_deducted": 2,
  "remaining_coin": "integer"
}
```

**Validation Checklist:**
- [x] Status code `200`
- [x] `coin_deducted` = 2 (each invite costs 2 coins)
- [x] "Undang" button changes to "Diundang" state on UI
- [x] Friend appears in invitation list on recipient's device

**Status:** OK with Note — "Undang" button reactivates when user scrolls and encounters same profile again in Explore, allowing unintended re-invitation and double coin deduction

---

## Category 5: Subscribe & Purchase

### TC-API-SUB-001 — Subscribe Premium

| Field | Detail |
|---|---|
| **Endpoint** | `POST /api/v1/subscription/subscribe` |
| **Method** | POST |
| **Auth** | Bearer Token |

**Expected Response — 200 OK:**
```json
{
  "status": "subscribed",
  "pulsa_deducted": true,
  "coin_added": 15
}
```

**Validation Checklist:**
- [x] Status code `200`
- [x] User's phone credit (pulsa) deducted
- [x] User's coin balance increased by 15
- [x] Premium features unlocked after subscription

**Status:** OK

---

### TC-API-SUB-002 — Buy Coins

| Field | Detail |
|---|---|
| **Endpoint** | `POST /api/v1/coins/purchase` |
| **Method** | POST |
| **Auth** | Bearer Token |

**Expected Response — 200 OK:**
```json
{
  "status": "purchased",
  "pulsa_deducted": true,
  "coin_added": 30
}
```

**Validation Checklist:**
- [x] Status code `200`
- [x] User's pulsa deducted
- [x] Coin balance increased by 30
- [x] New coin balance reflected immediately in UI

**Status:** OK

---

## API Testing Notes

- All API tests executed via **Postman** with environment variables for base URL and Bearer tokens
- Network traffic monitored via **Charles Proxy** on physical test devices to verify actual request/response in mobile context
- Bearer token stored as Postman environment variable; automatically included in all authenticated request headers
- Response body validation includes: field presence, data types, value ranges, and business logic correctness — not just HTTP status codes
- Pagination tested by varying `page` and `limit` parameters and verifying no duplicate or missing items

---

> **Note:** Base URL, actual API endpoints, token values, and user identifiers have been anonymized. API structure based on real Milov backend testing at PT Indonesia Satu Tujuh.
