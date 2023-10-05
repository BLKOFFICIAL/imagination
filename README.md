# API Plan

## Introduction
This API provides two primary routes: `/register` for user registration and authentication and `/incident` for managing incidents. It also includes a status page for displaying incidents associated with a specific user.

## `/register` Route
### Authentication
- **Endpoint**: `/register`
- **Method**: POST
- **Request**:
  ```json
  {
    "username": "exampleuser",
    "password": "securepassword"
  }

# Response
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

# /incident Route
## POST Incident
### Endpoint: /incident
### Method: POST


# Request:

```json
{
  "title": "Server Outage",
  "description": "Our server is currently down.",
  "ETA": "2023-10-10T12:00:00Z",
  "id": 1
}
```


# Response

```json
{
  "message": "Incident saved successfully."
}
```

# GET Incidents by User ID
## Endpoint: /incident/:id
### Method: GET
#### Request:
- Example request: /incident/1


#### Response:

```json
[
  {
    "id": 1,
    "title": "Server Outage",
    "description": "Our server is currently down.",
    "ETA": "2023-10-10T12:00:00Z"
  },
  {
    "id": 1,
    "title": "Network Issues",
    "description": "We are experiencing network problems.",
    "ETA": "2023-10-12T15:30:00Z"
  }
]
```

# Status Page API
## Create Status Page

- Create an HTML status page template that includes placeholders for incident data.
- When creating the status page, replace placeholders with the user's incidents.

```html
<!DOCTYPE html>
<html>
<head>
    <title>Status Page</title>
</head>
<body>
    <h1>Status Page</h1>
    <div id="incidents">
        <!-- Incidents will be dynamically inserted here -->
    </div>
    <script>
        // JavaScript code to fetch and display incidents dynamically
        fetch('/incident/1') // Replace 1 with the user's ID
            .then(response => response.json())
            .then(data => {
                const incidentsDiv = document.getElementById('incidents');
                data.forEach(incident => {
                    const incidentDiv = document.createElement('div');
                    incidentDiv.innerHTML = `
                        <h2>${incident.title}</h2>
                        <p>${incident.description}</p>
                        <p>ETA: ${incident.ETA}</p>
                    `;
                    incidentsDiv.appendChild(incidentDiv);
                });
            })
            .catch(error => console.error('Error fetching incidents:', error));
    </script>
</body>
</html>
```

# Additional Notes

- Implement proper authentication mechanisms for user registration, such as hashing passwords.
- Use a secure method to store and manage user authentication tokens (e.g., JSON Web Tokens or sessions).
- The /incident route should associate incidents with user IDs for proper separation.
- Implement error handling and validation for API requests, including input validation and error responses.
- The status page template is a  exambasic HTMLple; you can expand it and style it as needed for your application.
- Consider adding authentication and authorization checks to ensure users can only access their own incidents.


