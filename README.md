# REST API Best Practices & Naming Conventions

> A practical, developer-focused guide to designing robust, secure, and maintainable REST APIs — covering resource naming, URI structure, HTTP methods, error handling, rate limiting, versioning, and more.

> Consistent API design improves the usability, scalability, and maintainability of your services, making them easier to adopt and integrate with. Always tailor these conventions to your target audience and the overarching goals of your API.

## Table of Contents

- [1. What is REST API?](#1-what-is-rest-api)
- [2. Breakdown of the Parts of a URL](#2-breakdown-of-the-parts-of-a-url)
- [3. Use HTTP Methods to Communicate Intent](#3-use-http-methods-to-communicate-intent)
- [4. Use an Appropriate Data Structure](#4-use-an-appropriate-data-structure)
- [5. Choose a Consistent JSON Field Naming Convention](#5-choose-a-consistent-json-field-naming-convention)
- [6. Use Consistent Error Messages](#6-use-consistent-error-messages)
- [7. Use Status Codes in Error Handling](#7-use-status-codes-in-error-handling)
- [8. Apply Rate Limiting to API Calls](#8-apply-rate-limiting-to-api-calls)
- [9. Avoid Verbs in URIs](#9-avoid-verbs-in-uris)
- [10. Use Plural Nouns](#10-use-plural-nouns)
- [11. Use Lowercase Letters](#11-use-lowercase-letters)
- [12. Use Hyphens to Separate Words in URI Paths](#12-use-hyphens-to-separate-words-in-uri-paths)
- [13. Use Underscores in Query String Parameters](#13-use-underscores-in-query-string-parameters)
- [14. Use Nesting to Show Resource Relationships](#14-use-nesting-to-show-resource-relationships)
- [15. Limit Nesting with Top-Level Resources](#15-limit-nesting-with-top-level-resources)
- [16. Use Forward Slashes for Hierarchy, No Trailing Slash](#16-use-forward-slashes-for-hierarchy-no-trailing-slash)
- [17. Use Query Parameters for Filtering, Sorting, Pagination, and Field Selection](#17-use-query-parameters-for-filtering-sorting-pagination-and-field-selection)
- [18. Version Your APIs](#18-version-your-apis)

## Support the Project :star:

> If you find this guide helpful, please consider giving it a **star** on GitHub. Your support is greatly appreciated!

> Connect with the author on [LinkedIn](https://www.linkedin.com/in/saif-aust-cse/).

## 1. What is REST API?

REST (Representational State Transfer) is an architectural style for designing web APIs that allows different systems and applications to communicate with each other over the internet.

REST treats the resources of a web application as objects in a data model. Clients perform operations on these resources using standard HTTP methods such as GET, POST, PUT, PATCH, and DELETE. Each resource is uniquely identified by a URL.

<div style="text-align: center;">
        <img src="https://github.com/saifaustcse/rest-api-best-practices/blob/main/images/rest-api-model.png?raw=true" width="700" height="300">
</div>

**Key Characteristics and Principles of REST:**

1. **Statelessness:** Each request from a client to the server must contain all the information needed to understand and process it. The server keeps no client-session state between requests, making it scalable and easy to manage.

2. **Resource-Based:** REST APIs are built around resources, which represent objects or entities in the system. Each resource is identified by a unique URL, and clients interact with these resources using standard HTTP methods.

3. **Uniform Interface:** REST APIs use a uniform set of well-defined and standardized methods (HTTP verbs) to perform actions on resources. This uniformity makes it easier for clients to understand and interact with the API.

4. **Client-Server Architecture:** The client and server are separate entities that can evolve independently. Clients are not concerned with the storage of data or the implementation of business logic, while servers are not concerned with the user interface.

5. **Layered System:** REST APIs can be built on top of multiple layers, allowing for a separation of concerns and modularity. Each layer provides specific functionality without affecting the other layers.

6. **Cacheability:** Responses from a REST API can be cached, improving performance and reducing the load on the server.

7. **Hypermedia as the Engine of Application State (HATEOAS):** REST APIs can include hyperlinks in responses, allowing clients to discover and navigate available resources and actions dynamically.

## 2. Breakdown of the Parts of a URL

A URL (Uniform Resource Locator) is a reference or address used to locate resources on the internet. It typically consists of several parts, each serving a specific purpose:

```
   protocol://hostname:port/path?query_string#fragment
```

1. **Protocol:** The protocol defines the rules used to access the resource. The most common are "http" (Hypertext Transfer Protocol) and "https" (its secure version).

2. **Hostname:** The hostname (domain name) is the address of the server hosting the resource. In "www.example.com," "www" is the subdomain and "example.com" the main domain.

3. **Port:** The port specifies the communication endpoint on the server. It is optional; the default is 80 for "http" and 443 for "https".

4. **Path:** The path points to a specific location on the server, representing the directory hierarchy leading to the resource. In "https://www.example.com/products/shoes," "/products/shoes" is the path.

5. **Query String:** The query string passes additional parameters to the server. It starts with "?" and contains key-value pairs separated by "&." In "https://www.example.com/search?query=shoes&size=10," "query" and "size" are the query parameters.

6. **Fragment:** The fragment identifies a section within a resource, such as an anchor in an HTML document. Indicated by "#", it is never sent to the server; the client uses it to navigate the retrieved resource.

Note: A URL may omit some of these parts depending on the resource and use case.

## 3. Use HTTP Methods to Communicate Intent

One of the key principles of REST APIs is the use of standard HTTP methods to communicate the intent of the request.

The following table summarizes the HTTP methods used in REST APIs:

| REST Verb | Action                                                                                       |
| --------- | -------------------------------------------------------------------------------------------- |
| GET       | Fetches a record or set of resources from the server                                         |
| OPTIONS   | Describes the communication options available for the target resource (e.g., CORS preflight) |
| POST      | Creates a new resource or a collection of resources                                          |
| PUT       | Replaces the target resource with the request payload                                        |
| PATCH     | Modifies the given record                                                                    |
| DELETE    | Deletes the given resource                                                                   |

Resources:

- [PATCH vs PUT in REST API](https://josipmisko.com/posts/patch-vs-put-rest-api) — Differences between PATCH and PUT

## 4. Use an Appropriate Data Structure

A common misconception is that a REST API must use JSON. In reality, REST is resource-oriented: a resource can be a JPEG image, an HTML document, or any other data structure.

Choose what works best for your use case. Many organizations standardize on JSON in their API guidelines. When using JSON, follow these best practices:

- Use valid JSON Schema for both request and response bodies to ensure consistency and data validation.
- Set the "Content-Type" header to "application/json" in all API requests and responses involving JSON data.
- Utilize JSON even for error messages, avoiding plain text or HTML responses.

**Example API Endpoint: `/users` Method: `POST`**

**Description:** This API allows clients to create a new user by sending a JSON payload in the request. The API will then return a JSON response containing the details of the newly created user.

**Request Payload:**

```json
{
  "name": "John Doe",
  "email": "john.doe@example.com",
  "age": 30
}
```

**Response:**

```json
{
  "id": "123456789",
  "name": "John Doe",
  "email": "john.doe@example.com",
  "age": 30,
  "createdAt": "2023-07-19T12:34:56Z"
}
```

Using JSON for both requests and responses ensures a standardized data format and efficient data exchange.

## 5. Choose a Consistent JSON Field Naming Convention

When working with JSON data, it's important to establish a consistent field naming convention for better readability and maintainability. While JSON doesn't enforce any specific naming convention, following a standard practice can greatly improve code consistency. Here are some common conventions along with their descriptions and examples:

1. **snake_case:**
   - Lowercase letters with underscores separating words.
   - Example: "user_name"

2. **camelCase:**
   - Lowercase first letter of the first word, capitalizing the first letter of subsequent words.
   - Example: "userName"

3. **PascalCase:**
   - Capitalizing the first letter of each word.
   - Example: "UserName"

4. **kebab-case:**
   - Lowercase letters with hyphens separating words.
   - Example: "user-name"

**camelCase** and **snake_case** are the most widely used and recommended. Pick one and apply it consistently across all your JSON structures.

## 6. Use Consistent Error Messages

HTTP status codes alone are often not enough to convey error details. Include structured JSON error messages in responses to better support API consumers.

A well-formed error message should consist of the following components:

- **Error Code:** A machine-readable code that uniquely identifies the error condition, allowing developers to handle errors programmatically.

- **Error Message:** A human-readable message that clearly explains the error to API consumers.

- **Error Context:** Additional details — such as the request ID, request parameters, or the field(s) that caused the issue — to aid debugging and troubleshooting.

- **Error Links:** URLs to documentation or support resources that help consumers resolve the issue.

- **Timestamp:** The exact time the error occurred, for tracing and logging.

**Example:**

```json
{
  "errorCode": "40001",
  "errorMessage": "Invalid input: Missing 'email' field in the request.",
  "errorContext": {
    "requestId": "123456789",
    "requestParameters": {
      "name": "John Doe",
      "age": 30
    }
  },
  "errorLinks": [
    "https://example.com/docs/errors/40001",
    "https://example.com/support/contact"
  ],
  "timestamp": "2023-07-19T15:30:45Z"
}
```

Consistently using structured error messages like this significantly improves the error-handling experience for API consumers.

## 7. Use Status Codes in Error Handling

HTTP status codes communicate the outcome of a request — whether it succeeded, failed, or requires redirection. Below are the status code ranges and their meanings:

- **1XX (Informational):** The server has received the request and is still processing it (e.g., 102 Processing).

- **3XX (Redirects):** Further action is required to complete the request (e.g., 301 Moved Permanently).

- **4XX (Client Errors):** The request itself was invalid (e.g., 400 Bad Request, 404 Not Found).

- **5XX (Server Errors):** The server failed to process the request (e.g., 500 Internal Server Error).

**Example:**

For example, a request for a nonexistent user ID might return a 404 with a message like this:

```json
{
  "statusCode": 404,
  "message": "User not found. Please provide a valid user ID."
}
```

Consistent status codes clarify API responses and ensure effective error handling and communication.

Resources:

- [API Best Practices: Response Handling](http://blogs.mulesoft.com/api-best-practices-response-handling/)
- [Error handling considerations and best practices](http://soabits.blogspot.ru/2013/05/error-handling-considerations-and-best.html)

## 8. Apply Rate Limiting to API Calls

Rate limiting controls how many requests a client can make within a given time frame, ensuring fair usage and protecting your API from abuse or overload. Key considerations:

1. **Set Rate Limit Information in API Response:**

   Include rate limit information in API responses: the total requests allowed per window, the remaining requests, and when the limit resets.

2. **Use "429 Too Many Requests" Status Code:**

   Return "429 Too Many Requests" when a client exceeds its rate limit.

3. **Utilize "Retry-After" Header:**

   Include a "Retry-After" header telling the client how long to wait before retrying.

4. **Expose Rate Limit Headers:**

   Optionally, expose the remaining calls in standard rate-limit headers such as `RateLimit-Remaining` so clients can track their usage.

Rate limiting ensures fair resource distribution and maintains API stability, reliability, and performance.

## 9. Avoid Verbs in URIs

Avoid verbs in endpoint paths and instead structure paths around the resources they represent.

Examples:

| Do's            | Don'ts               |
| --------------- | -------------------- |
| POST /users     | POST /createUser     |
| GET /users      | GET /getAllUsers     |
| GET /users/1    | GET /getUserById/1   |
| PUT /users/1    | PUT /updateUser/1    |
| PATCH /users/1  | PATCH /modifyUser/1  |
| DELETE /users/1 | DELETE /deleteUser/1 |

## 10. Use Plural Nouns

Use plural nouns unless the resource is a singleton.

Examples:

| Do's                        | Don'ts            |
| --------------------------- | ----------------- |
| POST /users                 | POST /user        |
| GET /users                  | GET /user         |
| GET /users/123              | GET /user/123     |
| PUT /users/123              | PUT /user/123     |
| PATCH /users/123            | PATCH /user/123   |
| DELETE /users/123           | DELETE /user/123  |

## 11. Use Lowercase Letters

Use only lowercase letters in URIs.

Examples:

| Do's       | Don'ts           |
| ---------- | ---------------- |
| GET /users | GET /getAllUsers |
| GET /users | GET /GetAllUsers |
| GET /users | GET /USERS       |

## 12. Use Hyphens to Separate Words in URI Paths

Avoid underscores, camelCase, PascalCase, spaces, and special characters in URIs. Instead, use hyphens (-) to separate words in the URI path. This improves readability and ensures compatibility across systems and platforms.

Examples:

| Do's            | Don'ts            |
| --------------- | ----------------- |
| /user-roles     | /user_roles       |
| /user-roles     | /User_Roles       |
| /user-roles     | /userRoles        |
| /user-roles     | /UserRoles        |
| /user-roles     | /user%20roles     |
| /user-roles     | /user roles       |
| /user-roles/123 | /user_roles/123   |
| /user-roles/123 | /User_Roles/123   |
| /user-roles/123 | /userRoles/123    |
| /user-roles/123 | /UserRoles/123    |
| /user-roles/123 | /user roles/123   |
| /user-roles/123 | /user%20roles/123 |

## 13. Use Underscores in Query String Parameters

Separate query string parameters with underscores (\_) to improve readability and maintain consistent URI formatting.

Examples:

| Do's                                  | Don'ts                              |
| ------------------------------------- | ----------------------------------- |
| /api/users?sort_by=firstName_desc     | /api/users?sortBy=firstName_desc    |
| /api/users?filter_by=active           | /api/users?filterBy=active          |
| /api/users?page_size=10&page_number=2 | /api/users?pageSize=10&pageNumber=2 |
| /api/users?search_query=john          | /api/users?searchQuery=john         |

## 14. Use Nesting to Show Resource Relationships

When API endpoints have relationships with each other, nesting them can improve clarity and understanding.

Examples:

| Do's                     | Don'ts                 |
| ------------------------ | ---------------------- |
| /api/users/1/roles       | /api/roles?userId=1    |
| /api/users/1/roles/3     | /api/roles/3           |
| /api/users/1/friends     | /api/friends?userId=1  |
| /api/users/1/friends/2   | /api/friends/2         |
| /api/users/1/posts       | /api/posts?userId=1    |
| /api/users/1/posts/5     | /api/posts/5           |
| /api/posts/5/comments    | /api/comments?postId=5 |
| /api/posts/5/comments/10 | /api/comments/10       |

## 15. Limit Nesting with Top-Level Resources

Keeping URI nesting shallow avoids overly complex and deeply nested paths and makes the API more intuitive. A flatter, more modular structure improves scalability and maintainability.

Examples:

| Do's                     | Don'ts                                   |
| ------------------------ | ---------------------------------------- |
| /api/comments/10/replies | /api/users/1/posts/5/comments/10/replies |
| /api/posts/5/tags        | /api/users/1/posts/5/tags                |
| /api/comments/10/likes   | /api/users/1/posts/5/comments/10/likes   |
| /api/posts/5/author      | /api/users/1/posts/5/author              |
| /api/users/1/followers   | /api/users/1/posts/5/author/followers    |

## 16. Use Forward Slashes for Hierarchy, No Trailing Slash

Use forward slashes to indicate hierarchy, but omit the trailing forward slash.

Examples:

| Do's                        | Don'ts                 |
| --------------------------- | ---------------------- |
| POST /users                 | POST /users/           |
| GET /users                  | GET /users/            |
| GET /users/123              | GET /users/123/        |
| PUT /users/123              | PUT /users/123/        |
| PATCH /users/123            | PATCH /users/123/      |
| DELETE /users/123           | DELETE /users/123/     |

## 17. Use Query Parameters for Filtering, Sorting, Pagination, and Field Selection

As your dataset grows, retrieving exactly the data you need without exposing the entire database becomes increasingly important. REST APIs support four query-based options to enable efficient, secure data retrieval: filtering, sorting, pagination, and field selection.

### Filtering

Retrieve only results that meet specific conditions, using parameters such as `country` or `creation_date`.

Example queries:

- `GET /users?country=UK`
- `GET /users?creation_date=2021-10-11`
- `GET /users?name=John&age=30`

### Sorting

Order results in ascending or descending order by a specified field.

Example queries:

- `GET /users?sort_by=birthdate_asc`
- `GET /users?sort_by=creation_date_desc`

### Pagination

Pagination narrows down results by specifying the number of items to display and the offset to skip.

Example queries:

- `GET /users?limit=50`
- `GET /users?limit=20&offset=40`

### Field Selection

Request only the fields you need in the response — especially useful for objects with many fields.

Example queries:

- For a specific user:
  `GET /users/123?fields=name,email`
- For a list of users:
  `GET /users?fields=name,email`

These query options make your API more flexible and user-friendly. Document the parameters so consumers can use them effectively.

## 18. Version Your APIs

Versioning provides a smooth upgrade path and maintains backward compatibility, letting clients adopt new features without breaking existing integrations. Best practices:

1. **Use URL Versioning:**

   Include the version directly in the URL to distinguish releases. For example:
   - `http://api.example.com/v1/store/employees/{emp-id}`
   - `http://api.example.com/v1/store/items/{item-id}`
   - `http://api.example.com/v2/store/employees/{emp-id}/address`

2. **API Documentation:**

   Document each version's changes, additions, and deprecations so users can plan their migration.

3. **Semantic Versioning:**

   Use Semantic Versioning (SemVer) — `MAJOR.MINOR.PATCH` — to indicate the extent of each change:
   - `MAJOR` version is incremented for incompatible changes.
   - `MINOR` version is incremented for backward-compatible additions.
   - `PATCH` version is incremented for backward-compatible bug fixes.

4. **Deprecation Policy:**

   Clearly state when older versions will no longer be supported so clients can plan their migration.

Following these practices keeps your API stable and reliable while you continue to evolve it.

## References

- [Stack Overflow](https://stackoverflow.blog/2020/03/02/best-practices-for-rest-api-design/)
- [Microsoft REST API Guidelines](https://github.com/Microsoft/api-guidelines/)

## API Documentation Examples

- [Twitter](https://developer.x.com/en/docs/x-api)
- [GitHub](https://docs.github.com/en)
- [Instagram](https://developers.facebook.com/docs/instagram-platform)
- [Facebook](https://developers.facebook.com/docs/graph-api/using-graph-api/)
- [Pinterest](https://developers.pinterest.com/docs/api/overview/)
- [apiDoc](http://apidocjs.com/)
- [REST API Example](https://dummy.restapiexample.com/)

## API Documentation and Testing Tools

- [Swagger (OpenAPI)](http://swagger.io/)
- [Postman](https://www.postman.com/)