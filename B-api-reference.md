# Part B: API Reference Entry

## Create a task

Creates a new task inside a project for an authenticated user. The user must have permission to add tasks to the project and assign the task to the selected user.

### Endpoint

- **HTTP method:** `POST`
- **Path:** `/v1/projects/{projectId}/tasks`
- **Content type:** `application/json`
- **Authentication:** Bearer access token
- **Success status:** `201 Created`

### Path parameters

| Name | Type | Required? | Description |
|---|---|---|---|
| `projectId` | string (UUID) | Yes | Unique identifier of the project in which the task will be created. |

### Query parameters

This endpoint has no query parameters.

### Request headers

| Header | Required? | Example | Description |
|---|---|---|---|
| `Authorization` | Yes | `Bearer <access_token>` | Supplies the authenticated user's access token. |
| `Content-Type` | Yes | `application/json` | Declares that the request body is JSON. |
| `Accept` | Recommended | `application/json` | Requests a JSON response. |

Do not send a real access token in public documentation, screenshots, or source control.

### Request body

The request body must be a JSON object.

| Field | Type | Required? | Description |
|---|---|---|---|
| `title` | string | Yes | Task title. Must contain 1–120 characters after trimming whitespace. |
| `description` | string | No | Additional task details. May be omitted or set to an empty string. Maximum 2,000 characters. |
| `assigneeId` | string (UUID) | Yes | Identifier of the user who will be assigned the task. The user must exist and be eligible for assignment to the project. |
| `dueDate` | string (date, `YYYY-MM-DD`) | Yes | Date the task is due, expressed as a calendar date. Example: `2026-11-15`. |
| `priority` | string (enum) | Yes | Task priority. Allowed values: `low`, `medium`, `high`. |

Unknown fields should be rejected with a validation error so clients can detect misspelled field names.

### Example request

```http
POST /v1/projects/8d5c2d9e-7f21-4a82-9b11-15f46f0d9a31/tasks HTTP/1.1
Host: api.example.com
Authorization: Bearer <access_token>
Content-Type: application/json
Accept: application/json
```

```json
{
  "title": "Prepare monthly delivery report",
  "description": "Collect delivery figures from the regional teams.",
  "assigneeId": "2b1a4c7e-8d32-4f65-a120-9c6d7e8f9012",
  "dueDate": "2026-11-15",
  "priority": "high"
}
```

### Successful response: `201 Created`

The server creates the task and returns the new task resource.

```json
{
  "id": "7a6b5c4d-3e2f-4a10-9b8c-1d2e3f4a5b6c",
  "projectId": "8d5c2d9e-7f21-4a82-9b11-15f46f0d9a31",
  "title": "Prepare monthly delivery report",
  "description": "Collect delivery figures from the regional teams.",
  "assigneeId": "2b1a4c7e-8d32-4f65-a120-9c6d7e8f9012",
  "dueDate": "2026-11-15",
  "priority": "high",
  "status": "open",
  "createdAt": "2026-10-21T07:30:00Z"
}
```

### Response codes

| HTTP status | Name | When it occurs |
|---|---|---|
| `201` | Created | The task was created successfully. The response contains the new task. |
| `400` | Bad Request | The request body is malformed JSON or the request cannot be parsed. |
| `401` | Unauthorized | The access token is missing, invalid, or expired. |
| `403` | Forbidden | The authenticated user does not have permission to create tasks in the project or assign the selected user. |
| `404` | Not Found | The project or specified assignee does not exist, or is not visible to the caller. |
| `405` | Method Not Allowed | The path exists but does not support the HTTP method used. |
| `406` | Not Acceptable | The client requests a response format the endpoint does not support. |
| `409` | Conflict | The project is in a state that prevents new tasks from being created, such as being archived. |
| `415` | Unsupported Media Type | The request does not use `Content-Type: application/json`. |
| `422` | Unprocessable Content | The JSON is valid, but one or more fields fail validation—for example, a missing title, invalid priority, or incorrectly formatted date. |
| `429` | Too Many Requests | The client has exceeded the allowed request rate. |
| `500` | Internal Server Error | An unexpected server-side error prevents task creation. |
| `503` | Service Unavailable | The service is temporarily unavailable, for example during maintenance. |

### Validation notes

- `projectId` and `assigneeId` must be valid UUIDs.
- `title` cannot be blank and cannot exceed 120 characters.
- `priority` must be exactly `low`, `medium`, or `high`.
- `dueDate` must be a valid date in `YYYY-MM-DD` format.
- The server must verify authentication and authorization before creating the task.
- The example uses `api.example.com` and sample identifiers. Replace them with the real service host and valid IDs when implementing an actual API client.

### Example validation error: `422 Unprocessable Content`

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "One or more fields are invalid.",
    "details": [
      {
        "field": "priority",
        "issue": "Must be one of: low, medium, high."
      }
    ]
  }
}
```

### Design note

This is a hypothetical API design created for the assignment. The response codes above describe the behavior this proposed endpoint should implement; they do not describe a real deployed service.
