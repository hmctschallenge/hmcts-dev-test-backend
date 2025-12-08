# HMCTS Dev Test Backend

This will be the backend for the brand new HMCTS case management system. As a potential candidate we are leaving
this in your hands. Please refer to the brief for the complete list of tasks! Complete as much as you can and be
as creative as you want.

You should be able to run `./gradlew build` to start with to ensure it builds successfully. Then from that you
can run the service in IntelliJ (or your IDE of choice) or however you normally would.

There is an example endpoint provided to retrieve an example of a case. You are free to add/remove fields as you
wish.

To run the backend, first run `docker compose up -d` to create the postgres database defined in docker-compose.yml,
then run `./gradlew bootrun` to start the main spring boot application.

The application runs on http://localhost:4000

### Endpoints

| Path     | Method | Description                               | Returns                                                 |
| -------- | ------ | ----------------------------------------- | ------------------------------------------------------- |
| `/cases` | POST   | Create a new case and add to the database | Success - 200 (Case) OK, Error - 400 Bad Request (null) |

### Case Entity Structure

The Case class contains the following fields, including auto-generated id and createdDate fields.

```json
{
  "id": 5,
  "caseNumber": "AIDJ123",
  "title": "Title",
  "description": "description",
  "status": "First Hearing",
  "dueDate": "2026-01-31",
  "createdDate": "2025-12-01"
}
```

### Example Request Body

A new Case can be created by sending a POST request with the following body:

```json
{
  "caseNumber": "AIDJ123",
  "title": "Title",
  "description": "Optional description",
  "status": "First Hearing",
  "dueDate": "2026-01-12"
}
```

The description field is optional so can be left empty, all other fields must not be null, and the dueDate must be in the future. If any of these constraints are not met the case will not be created and the request will result in a bad request response.
