#Resource Log Manager API

A Java Spring Boot API to manage exclusive resource logs with timeout and process-level tracking.

Features
Acquire Lock with Timeout:
Take over expired locks on resources if the timeout is exceeded.

List Active Locks:
View all currently locked resources.

View Locks by Process:
Retrieve all resources locked by a specific process.

Release Lock:
Safely release resource locks when a process is done.

Tech Stack
Java 17+

Spring Boot 3+

Spring Data JPA

H2 In-Memory Database

API Endpoints

1️⃣ List All Active (Locked) Resources
pgsql

GET /log/locked

[
  {
    "resourceName": "ResourceA",
    "processId": "Proc1",
    "timestamp": "2025-07-20T12:00:00",
    "isActive": true
  }
]

2️⃣ Acquire Lock with Timeout
pgsql

POST /log/request-with-timeout
Request Body:

json

{
  "resourceName": "ResourceA",
  "processId": "Proc123",
  "timeoutInSeconds": 300
}
Responses:
200 OK – Lock acquired or taken over

409 CONFLICT – Resource is still locked (timeout not exceeded)

3️⃣ List Locks by Process
pgsql

GET /log/process/{processId}
Example:

pgsql

GET /log/process/Proc123

4️⃣ Release Lock
pgsql

POST /log/release
Request Body:
json
Copy
Edit
{
  "resourceName": "ResourceA",
  "processId": "Proc123"
}
Run Locally
Clone the Repository

git clone <your-repo-link>
cd <your-repo-folder>
Run the Application




Author
Chittaluri Rekha
