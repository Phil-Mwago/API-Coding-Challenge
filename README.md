# API Design Challenge

## 1. API Specification Overview

I have designed a RESTful API that prioritizes developer experience and data transparency.

* **`GET /v1/facilities`**: Returns a paginated list. Supports region and category filters via query parameters (e.g., `?region=nairobi`).


* **`GET /v1/facilities/{id}`**: Returns full details, including contact info, operating hours, and Geo-coordinates.


* **`GET /v1/facilities/filters`**: A helper endpoint that provides valid filter values to help developers build dynamic UI dropdowns.


* *Note:* While useful, this approach requires constant maintenance if or when the database structure changes.





## 2. Why this structure?

* **Developer-Centric**: I used a wrapper to separate pagination details from the actual data array, keeping the payload clean.


* **Civic Readiness**: Every response includes a timestamp and coordinates to prevent data miscommunication with other apps. This ensures it is easy to integrate with other maps.



## 3. Versioning & Breaking Changes

* **Explicit Versioning**: I advocate for URL versioning (`/v1/`) because it is the most transparent for external partners who may have limited technical resources or knowledge.


* **The "Sunset" Rule**:
  * **Non-breaking changes** (adding fields) occur in the current version.


  * **Breaking changes** (removing fields) trigger a `v2`.


  * We would provide a **6-month "sunset" period** where both versions run in parallel.





## 4. Engineering Clarifications (The PM Checklist)

Before moving to production, I would check with developers on the following:

* **Rate Limiting**: How do we distinguish between a single citizen and a high-traffic partner? 


* **Data Freshness**: Is the data a "live" view of the database or a cached snapshot? What if the client wanted visualized data?


* **Auth Requirements**: While the API is public, do we need API keys for partners to track impact and prevent abuse? 



## 5. Supporting Transparency & Reuse

* **Standardized Formats**: By using standard JSON and ISO-8601 timestamps/timezones, the data can be easily ingested by standard data science tools.


* **Scalability**: While standardizing at the onset may require more work, it makes the system easier to scale regarding integration vs. interoperability.


* **Open Documentation**: Using a Postman collection or OpenAPI spec ensures the community can "self-serve" without needing 1-on-1 support from our team.



---
