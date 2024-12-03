# Recruitment Management API Documentation

This module provides functions to manage recruitment posts for a club using an SQLite database and Express.js. The endpoints allow creating, deleting, and retrieving recruitment posts.

# Recruitment
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

## Function: `deleteRecruitment`

### Description
Deletes an existing recruitment post by its unique ID.

### Parameters
- `req: Request` - The HTTP request object with recruitment_id as a route parameter.
- `res: Response` - The HTTP response object.
- `db: Database` - The SQLite database instance.

### Route Parameters
- recruitment_id (string): Unique ID of the recruitment post to delete.

### Responses
-  200 OK: Recruitment post successfully deleted.
```
{ "message": "Recruitment deleted successfully" }
```
-  400 Bad Request: Missing required recruitment_id parameter.
```
{ "error": "Missing required field: recruitment_id" }
```
- 404 Not Found: Recruitment post not found.
```
{ "error": "Recruitment not found" }
```
- 500 Internal Server Error: Database or server error.
```
{ "error": "Error deleting recruitment: <error message>" }
```

## Function: `getUserRecruitment`

### Description
Retrieves all recruitment posts for a user, filtered by the clubs they have marked as favorites.

### Parameters
- `req: Request` - The HTTP request object with user_id in the query string.
- `res: Response` - The HTTP response object.
- `db: Database` - The SQLite database instance.

### Route Parameters
- user_id (string): Unique ID of the user to filter recruitment posts.

### Responses
-  200 OK: Successfully retrieved recruitment posts.
```
{
  "data": [
    {
      "recruitment_id": number,
      "club_id": number,
      "title": string,
      "date_posted": string,
      "deadline": string,
      "application_link": string,
      "club_name": string
    },
    ...
  ]
}
```
-  500 Internal Server Error: Database or server error.
```
{ "error": "Error getting recruitment posts: <error message>" }
```

# Events
---

## Function: `createEvent`

### Description
Creates a new event for a club. The event includes details such as the club's ID, title, date, room, and optional incentives.

### Parameters
- `req: Request` - The HTTP request object containing the event details in the body.
- `res: Response` - The HTTP response object.
- `db: Database` - The SQLite database instance.

### Expected Request Body
```
{
  "club_id": number,         // ID of the club hosting the event
  "title": string,           // Title of the event
  "date": string,            // Date of the event
  "room": string,            // Location of the event
  "incentives": string?      // (Optional) Incentives for attending the event
}
```

### Responses
-  201 Created: Event successfully created
```
{
  "club_id": number,
  "title": string,
  "date": string,
  "room": string,
  "incentives": string | null
}
```
- 400 Bad Request: Missing required fields.
```
{ "error": "Missing required fields" }
```
- 500 Internal Server Error: Database or server error.
```
{ "error": "Event could not be created, + <error message>" }
```

## Function: `deleteEvent`

### Description
Creates a new event for a club. The event includes details such as the club's ID, title, date, room, and optional incentives.

### Parameters
- `req: Request` - The HTTP request object with event_id as a route parameter.
- `res: Response` - The HTTP response object.
- `db: Database` - The SQLite database instance.

### Route Parameters
- `event_id: string` - Unique ID of the event to delete.

### Responses
-  200 OK: Event successfully deleted.
```
{ "message": "Event deleted successfully" }
```
- 400 Bad Request: Missing event_id parameter.
```
{ "error": "Missing required field: event_id" }
```
- 404 Not Found: Event not found.
```
{ "error": "Event not found" }
```
- 500 Internal Server Error: Database or server error.
```
{ "error": "Error deleting event: <error message>" }
```

## Function: `getAllClubEvents`

### Description
Fetches all events for all clubs.

### Parameters
- `req: Request` - The HTTP request object.
- `res: Response` - The HTTP response object.
- `db: Database` - The SQLite database instance.

### Route Parameters
- `event_id: string` - Unique ID of the event to delete.

### Responses
-  200 OK: Successfully retrieved all events.
```
{
"data": [
  {
  "club_id": number,
  "title": string,
  "date": string,
  "room": string,
  "incentives": string | null
  },
  ...
  ]
}
```
## Function: `getAllClubEvents`

### Description
Fetches all events for all clubs.

### Parameters
- `req: Request` - The HTTP request object.
- `res: Response` - The HTTP response object.
- `db: Database` - The SQLite database instance.

### Route Parameters
- `event_id: string` - Unique ID of the event to delete.

### Responses
-  200 OK: Successfully retrieved all events.
```
{
"data": [
  {
  "club_id": number,
  "title": string,
  "date": string,
  "room": string,
  "incentives": string | null
  },
  ...
  ]
}
```
- 500 Internal Server Error: Database or server error.
```
{ "error": "Error getting events: <error message>" }
```
## Function: `deleteEvent`

### Description
Creates a new event for a club. The event includes details such as the club's ID, title, date, room, and optional incentives.

### Parameters
- `req: Request` - The HTTP request object with event_id as a route parameter.
- `res: Response` - The HTTP response object.
- `db: Database` - The SQLite database instance.

### Route Parameters
- `event_id: string` - Unique ID of the event to delete.

### Responses
-  200 OK: Event successfully deleted.
```
{ "message": "Event deleted successfully" }
```
- 400 Bad Request: Missing event_id parameter.
```
{ "error": "Missing required field: event_id" }
```
- 404 Not Found: Event not found.
```
{ "error": "Event not found" }
```
- 500 Internal Server Error: Database or server error.
```
{ "error": "Error deleting event: <error message>" }
```

## Function: `getUserUpcomingEvents`

### Description
Fetches all upcoming events for a specific user based on their club preferences.

### Parameters
- `req: Request` - The HTTP request object containing user_id in the query.
- `res: Response` - The HTTP response object.
- `db: Database` - The SQLite database instance.

### Route Parameters
-  `user_id: string - ID` of the user whose upcoming events are to be retrieved.

### Responses
-  200 OK: Successfully retrieved all events.
```
{
"data": [
  {
  "club_id": number,
  "title": string,
  "date": string,
  "room": string,
  "incentives": string | null
  },
  ...
  ]
}
```
-  500 Internal Server Error: Database or server error during fetching.
```
{ "error": "Error getting user upcoming events: <error message>" }
```

## Function: `getUserNonFavoriteEvents`

### Description
Fetches all non-favorite events for a user based on their club preferences.

### Parameters
- `req: Request` - The HTTP request object containing user_id in the query.
- `res: Response` - The HTTP response object.
- `db: Database` - The SQLite database instance.

### Route Parameters
-  `user_id: string - ID` of the user whose non-favorite events are to be retrieved.

### Responses
-  200 OK: Successfully retrieved all events.
```
{
"data": [
  {
  "club_id": number,
  "title": string,
  "date": string,
  "room": string,
  "incentives": string | null
  },
  ...
  ]
}
```
-  500 Internal Server Error: Database or server error during fetching.
```
{ "error": "Error getting user upcoming non-favorite events: <error message>" }
```

## Function: `getUserFavoriteEvents`

### Description
Fetches all favorite events for a user based on their club preferences.

### Parameters
- `req: Request` - The HTTP request object containing user_id in the query.
- `res: Response` - The HTTP response object.
- `db: Database` - The SQLite database instance.

### Route Parameters
-  `user_id: string - ID` of the user whose non-favorite events are to be retrieved.

### Responses
-  200 OK: Successfully retrieved all events.
```
{
"data": [
  {
  "club_id": number,
  "title": string,
  "date": string,
  "room": string,
  "incentives": string | null
  },
  ...
  ]
}
```
-  500 Internal Server Error: Database or server error during fetching.
```
{ "error": "Error getting user favorite events: <error message>" }
```

# User
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






