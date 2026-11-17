# Account Deletion API

A small REST API built with **Node.js** and **Express.js** that deletes a user account by email. It validates the request, returns clear HTTP status codes, and ships with a Dockerfile and a Postman collection for testing.

## Features

- `DELETE /delete-account` endpoint that removes a user by email
- Input validation with meaningful error messages
- Correct HTTP status codes (`200`, `400`, `404`)
- Dockerized for portable deployment
- Ready-to-import Postman collection (`test.json`)

## Tech Stack

- Node.js (ES modules)
- Express.js
- Docker
- Postman

## Getting Started

### Run locally

```bash
git clone https://github.com/elshemy44/Account-Deletion-Api.git
cd Account-Deletion-Api
npm install
node app.js
```

The server starts on `http://localhost:3000`.

### Run with Docker

```bash
docker build -t account-deletion-api .
docker run -p 3000:3000 account-deletion-api
```

## API Reference

### Delete an account

```
DELETE /delete-account
Content-Type: application/json
```

**Request body**

```json
{
  "email": "user1@example.com"
}
```

**Responses**

| Status | Meaning | Body |
| ------ | ------- | ---- |
| `200 OK` | Account deleted | `{ "message": "Account deleted successfully" }` |
| `400 Bad Request` | `email` missing from the body | `{ "message": "Email is required" }` |
| `404 Not Found` | No user with that email | `{ "message": "User not found" }` |

**Example**

```bash
curl -X DELETE http://localhost:3000/delete-account \
  -H "Content-Type: application/json" \
  -d '{"email": "user1@example.com"}'
```

## Testing with Postman

1. Open Postman and click **Import**.
2. Select `test.json` from this repository.
3. Run the **Delete Account** request against `http://localhost:3000`.

To test the error cases, send the same request with an empty body (`400`), or with an email that does not exist (`404`).

## Sample Data

The API uses a small in-memory list of users, so you can try it right away:

| id | email | name |
| -- | ----- | ---- |
| 1 | user1@example.com | User One |
| 2 | user2@example.com | User Two |

> Data is stored in memory, so it resets every time the server restarts.

## Possible Improvements

- Connect a real database (MongoDB or MySQL) instead of the in-memory list
- Add authentication (e.g. JWT) so users can only delete their own account
- Add automated tests (Jest and Supertest)
- Add register, login, and update endpoints for a full CRUD flow

## Author

**Ahmed Morsi** — [GitHub](https://github.com/elshemy44)
