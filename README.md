# API documentation - Deploy email verification in seconds
Real-Time Email Verification API by [BounceStrike](https://bouncestrike.com/)

## How to Call the API

Make a **GET request** to the following endpoint:

```bash
curl -X GET \
"https://api.bouncestrike.com?apikey=YOUR_API_KEY&email=test@example.com"
```

Replace `YOUR_API_KEY` with your personal API key.

---

## Request Parameters

| Parameter | Type   | Description                  | Required |
|-----------|--------|-----------------------------|----------|
| `apikey`  | string | Your personal API key       | Yes      |
| `email`   | string | The email address to verify | Yes      |

---

## Example Response

```json
{
  "status": "Success",
  "message": "Email verification completed successfully.",
  "verification": {
    "address": "test@example.com",
    "local_part": "test",
    "domain": "example.com",
    "accept_all_policy": false,
    "is_role_account": false,
    "is_free_provider": true,
    "is_disposable": false,
    "is_spamtrap": false,
    "deliverable": false
  },
  "credits_used": 12,
  "credits_left": 88,
  "next_reset": "2025-08-31"
}
```

---

## Response Parameters

| Parameter                               | Type              | Description                                      |
|----------------------------------------|-------------------|--------------------------------------------------|
| `status`                               | string            | "Success" or "Error"                            |
| `message`                              | string            | Description of the result                       |
| `verification`                         | object            | Details of the email verification               |
| `verification.address`                 | string            | The email address checked                       |
| `verification.local_part`              | string            | Local part of the email                         |
| `verification.domain`                  | string            | Domain of the email                             |
| `verification.accept_all_policy`       | boolean           | True if the remote host accepts any address     |
| `verification.is_role_account`         | boolean           | True if it's a role account (info@, sales@)    |
| `verification.is_free_provider`        | boolean           | True if it's a free email provider             |
| `verification.is_disposable`           | boolean           | True if disposable email                       |
| `verification.is_spamtrap`             | boolean           | True if it's a spamtrap or blacklist address   |
| `verification.deliverable`             | boolean           | True if email is deliverable                   |
| `credits_used`                         | integer           | Number of credits used so far                  |
| `credits_left`                         | integer           | Remaining monthly credits                      |
| `next_reset`                           | string (YYYY-MM-DD)| Date when credits reset                        |

---

## Error Codes

| HTTP Code | Error                                      | Description                                      |
|-----------|-------------------------------------------|--------------------------------------------------|
| `400`     | Invalid email address                    | The email parameter is missing or invalid       |
| `401`     | Missing API key                          | No API key provided in request                  |
| `403`     | Invalid API key / Inactive subscription  | The API key is wrong or subscription inactive   |
| `429`     | Quota exceeded                           | Your monthly credits are exhausted              |
| `429`     | Too many requests                        | You exceeded the rate limit (per second)        |
| `500/503` | Service temporarily unavailable          | BounceStrike service or connection error        |

---

## Notes
- Ensure your API key remains private and secure.
- Requests without a valid API key will be rejected.
