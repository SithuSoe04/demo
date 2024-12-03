# Recruitment Management API Documentation

This module provides functions to manage recruitment posts for a club using an SQLite database and Express.js. The endpoints allow creating, deleting, and retrieving recruitment posts.

---

## Function: `createRecruitment`

### Description
Creates a new recruitment post for a club. The post includes details like the club's ID, title, posting date, deadline, and application link.

### Parameters
- `req: Request` - The HTTP request object containing the recruitment details in the body.
- `res: Response` - The HTTP response object.
- `db: Database` - The SQLite database instance.

### Expected Request Body
```
{
  "club_id": number,       // ID of the club creating the recruitment post
  "title": string,         // Title of the recruitment post
  "date_posted": string?,  // (Optional) Date the post was created; defaults to current timestamp
  "deadline": string,      // Deadline for applications
  "application_link": string // URL link to the application form
}
```

### Responses
-  201 Created: Recruitment post successfully created.
```{
  "club_id": number,
  "title": string,
  "date_posted": string,
  "deadline": string,
  "application_link": string
}
```
-  400 Bad Request: Missing required fields.
```
{ "error": "Missing required fields" }
```
- 500 Internal Server Error: Database or server error.
```
{ "error": "Recruitment could not be created: <error message>" }
```


