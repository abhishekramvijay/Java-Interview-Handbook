# REST APIs & SOAP Web Services

> REST and SOAP are two widely used approaches for communication between distributed systems. REST is lightweight, resource-oriented, and the preferred choice for modern microservices, while SOAP is protocol-based and commonly used in enterprise systems requiring strict contracts, security, and reliability.

---

# Must Revise (★★★★★)

- REST
- SOAP
- HTTP Methods
- Idempotency
- Statelessness
- REST Constraints
- Request vs Response
- HTTP Status Codes
- REST vs SOAP
- REST Best Practices

---

# Contents

1. REST
2. REST Principles
3. HTTP Methods
4. Idempotency
5. HTTP Status Codes
6. Request & Response
7. SOAP
8. REST vs SOAP
9. REST Best Practices

---

# What is REST? ★★★★★

## Interview Answer

REST (Representational State Transfer) is an architectural style used for designing web services.

A REST API exposes resources identified by URIs and communicates primarily using HTTP.

Example

```
GET /employees/101
```

returns Employee 101.

---

# REST Principles ★★★★★

A RESTful service follows these constraints.

## Client-Server

Client and server are independent.

---

## Stateless

Every request contains all the information required to process it.

The server does not maintain client session state between requests.

Example

Authentication token is sent with every request.

---

## Cacheable

Responses can be cached to improve performance.

Example

```
Cache-Control
```

header.

---

## Uniform Interface

Resources are accessed consistently using URIs and standard HTTP methods.

---

## Layered System

Clients are unaware of intermediate components such as load balancers or gateways.

---

# Resource Naming ★★★★★

Resources should be nouns, not verbs.

Good

```
GET /employees

POST /employees

GET /employees/101
```

Avoid

```
/getEmployee

/createEmployee

/deleteEmployee
```

---

# HTTP Methods ★★★★★

## GET

Retrieve data.

Should not modify data.

Example

```
GET /employees/101
```

---

## POST

Create a new resource.

Example

```
POST /employees
```

---

## PUT

Replace an existing resource.

Example

```
PUT /employees/101
```

---

## PATCH

Partially update a resource.

Example

```
PATCH /employees/101
```

---

## DELETE

Delete a resource.

Example

```
DELETE /employees/101
```

---

# PUT vs PATCH ★★★★★

| PUT | PATCH |
|------|--------|
| Full update | Partial update |
| Replaces resource | Updates selected fields |
| Missing fields may be overwritten | Unspecified fields remain unchanged |

---

# Safe Methods ★★★★☆

Safe methods do not modify server data.

Examples

- GET
- HEAD
- OPTIONS

---

# Idempotency ★★★★★

## Interview Answer

An operation is idempotent if performing it multiple times produces the same result as performing it once.

Examples

| Method | Idempotent |
|---------|------------|
| GET | Yes |
| PUT | Yes |
| DELETE | Yes |
| POST | No |
| PATCH | Usually No |

Example

Deleting the same employee multiple times leaves the system in the same final state.

---

# HTTP Request Structure ★★★★☆

```
Request Line

↓

Headers

↓

Body (Optional)
```

Example

```
POST /employees

Content-Type: application/json

Authorization: Bearer token

{
   "name":"John"
}
```

---

# HTTP Response Structure ★★★★☆

```
Status Code

↓

Headers

↓

Body
```

Example

```
HTTP/1.1 200 OK

Content-Type: application/json

{
   "id":101
}
```

---

# Common HTTP Status Codes ★★★★★

## 2xx Success

| Code | Meaning |
|------|---------|
| 200 | OK |
| 201 | Created |
| 202 | Accepted |
| 204 | No Content |

---

## 3xx Redirection

| Code | Meaning |
|------|---------|
| 301 | Permanent Redirect |
| 302 | Temporary Redirect |
| 304 | Not Modified |

---

## 4xx Client Errors

| Code | Meaning |
|------|---------|
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 405 | Method Not Allowed |
| 409 | Conflict |
| 415 | Unsupported Media Type |
| 429 | Too Many Requests |

---

## 5xx Server Errors

| Code | Meaning |
|------|---------|
| 500 | Internal Server Error |
| 502 | Bad Gateway |
| 503 | Service Unavailable |
| 504 | Gateway Timeout |

---

# Content Negotiation ★★★★☆

Clients specify the response format using the

```
Accept
```

header.

Example

```
Accept: application/json
```

The request body format is specified using

```
Content-Type
```

Example

```
Content-Type: application/json
```

---

# Path Parameters vs Query Parameters ★★★★★

## Path Parameter

Identifies a specific resource.

```
GET /employees/101
```

---

## Query Parameter

Filters or modifies the result.

```
GET /employees?department=IT&page=2
```

---

# Path Variable vs Request Parameter (Spring) ★★★★☆

```java
@GetMapping("/employees/{id}")
public Employee getEmployee(
    @PathVariable int id) {

}
```

```java
@GetMapping("/employees")
public List<Employee> getEmployees(
    @RequestParam String department) {

}
```

---

# SOAP ★★★★★

## Interview Answer

SOAP (Simple Object Access Protocol) is a protocol for exchanging structured information using XML.

Unlike REST, SOAP follows strict messaging standards.

---

# SOAP Characteristics

- XML based
- Uses WSDL contract
- Platform independent
- Built-in security support
- Reliable messaging

---

# SOAP Message Structure

```
Envelope

↓

Header

↓

Body

↓

Fault (Optional)
```

---

# WSDL ★★★★☆

WSDL (Web Services Description Language) defines

- Available operations
- Request format
- Response format
- Endpoint details

Acts as the contract between client and server.

---

# REST vs SOAP ★★★★★

| REST | SOAP |
|------|------|
| Architectural Style | Protocol |
| JSON/XML | XML Only |
| Lightweight | Heavyweight |
| Faster | Slower |
| Easy to develop | Strict contract |
| Stateless | Can be Stateful |
| No built-in security | WS-Security support |
| Preferred for Microservices | Preferred for Enterprise Integrations |

---

# When to Use REST?

- Public APIs
- Mobile Applications
- Web Applications
- Microservices
- High Performance Systems

---

# When to Use SOAP?

- Banking
- Payment Systems
- Government Systems
- Enterprise Integrations
- Systems requiring WS-Security

---

# REST API Best Practices ★★★★★

- Use nouns in URLs.
- Use correct HTTP methods.
- Return appropriate HTTP status codes.
- Version APIs (`/v1/employees`).
- Keep APIs stateless.
- Validate request payloads.
- Use pagination for large datasets.
- Return meaningful error messages.
- Secure APIs using HTTPS and authentication.
- Maintain backward compatibility.

---

# Frequently Asked Questions

1. What is REST?
2. Explain REST constraints.
3. What is Statelessness?
4. PUT vs PATCH.
5. GET vs POST.
6. What is Idempotency?
7. Safe vs Idempotent methods.
8. Path Parameter vs Query Parameter.
9. Content-Type vs Accept.
10. Explain HTTP status codes.
11. What is SOAP?
12. REST vs SOAP.
13. What is WSDL?
14. When should SOAP be preferred over REST?

---

# REST & SOAP Quick Revision

### REST
- Resource based
- Stateless
- HTTP
- JSON
- Cacheable

### HTTP Methods
- GET → Read
- POST → Create
- PUT → Replace
- PATCH → Partial Update
- DELETE → Remove

### Idempotent Methods
- GET
- PUT
- DELETE

### Common Status Codes
- 200 OK
- 201 Created
- 204 No Content
- 400 Bad Request
- 401 Unauthorized
- 403 Forbidden
- 404 Not Found
- 409 Conflict
- 500 Internal Server Error
- 503 Service Unavailable

### Spring
- @PathVariable
- @RequestParam

### SOAP
- XML
- WSDL
- WS-Security
- Enterprise Integrations

### Most Asked Questions
- PUT vs PATCH
- GET vs POST
- Idempotency
- Statelessness
- REST vs SOAP
- Path vs Query Parameter
- Content-Type vs Accept
- HTTP Status Codes
