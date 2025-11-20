## 4. Security PoC: PostgreSQL UUID Parsing Error – Internal Server Crash

### Overview
A critical vulnerability was identified where supplying malformed UUIDs to an API endpoint expecting UUID input leads to a PostgreSQL parsing error. This error, in turn, causes an internal server crash, making the service unavailable.

### Impact
This vulnerability creates a **Denial of Service (DoS) opportunity**. An attacker can trigger a server crash by repeatedly sending malformed UUIDs, effectively rendering the service or specific functionalities unavailable to legitimate users.

### Affected System
•   **System Type:** Backend system interacting with PostgreSQL, processing UUID inputs.
•   **Sample Endpoint/URL:** `https://[anonymized-corporate-website.com]/api/resource/{uuid_id}`

### Steps to Reproduce
1.  Identify an API endpoint that expects a UUID as part of its parameters (e.g., a path parameter like `.../items/{item_uuid}`).
2.  Send an HTTP request (e.g., GET, PUT, DELETE) to this endpoint, providing a malformed string instead of a valid UUID (e.g., `.../items/invalid-uuid-string` or `.../items/123`).
3.  Observe the server response: a `500 Internal Server Error` indicating a database parsing issue, or potentially a complete server crash.
4.  Repeat the process with mass requests to trigger a full Denial of Service.

### Proof of Concept
<img width="1013" height="592" alt="chrome_Bgg0p0TmhU2025" src="https://github.com/user-attachments/assets/04d3fb19-ca05-4c17-b83c-a4bf0f2aa7c9" />

### Tools Used
•   Postman
