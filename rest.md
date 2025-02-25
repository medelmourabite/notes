# REST API interview quesitons

## 1. What is REST?

REST stands for Representational State Transfer. It is a set of architectural style for building networked applications.

## 2. What is a RESTful API?

A RESTful API is a service that follws the REST architectural style.

## 3. What are HTTP Req/Resp?

An HTTP Request is sent from client to server. it contains:

- Request Method: GET, POST, PUT, DELETE, etc.
- Request URL: the URL of the resource to be accessed.
- Request Headers: additional information about the request.
- Request Body: the data to be sent to the server.

An HTTP Response is sent from server to client. it contains:

- Response Status Code: the status of the response.
- Response Headers: additional information about the response.
- Response Body: the data returned by the server, usually in JSON format.

## 4. What are the top 5 REST guidlines?

### 4.1. Seperation of Client and Server

Implementation of the client and server must be done independently.

- Easier maintenance, scalability, and evolution.

### 4.2. Stateless

The server does not keep track of the state of the client.

- Simplifies server implementation.
- Less overhead for the server to maintain the state.

### 4.3. Uniform Interface

Each url of the API should be unique and represnt one serivce.

- Standardized URLs, making it easier to understand and use.

### 4.4. Cacheable

Whenever possible, the server responses should be stored.

- Improve performance by removing the need of repeated requests.

### 4.5. Layered System

The API must follw the layered system like MVC.

- It promote modular design and separation of concerns.

## 5. What is the defference between REST and SOAP?

### 5.1. REST

- Rest is an architectural style
- Uses HTTP and HTTPS
- Uses JSON, XML...
- Stateless
- Relies on HTTP status codes
- Lightweight and faster

### 5.2. SOAP

- SOAP is a protocol
- Can use various protocols like HTTP, SMTP, FTP...
- Typically uses XML
- Can be stateless or stateful
- Defines it's own status codes
- Can be slow and heavy due to XML proccessing

## 6. What are HTTP Verbs?

Also known as HTTP Methods. they are a set of actions that a client can perform on a resouce.

- GET: Retrieve data from a resource
- POST: Submit data (body) to be processed
- PUT: Replace a resource or create a new one if it doesn't exist
- DELETE: Delete a resource
- PATCH: Update a resource partially

## 7. Explain the concept of Idempotence in RESTFul APIs

Idempotence means that a request can be repeated as many times as needed without changing the result.

Idempotent methods are: GET, PUT, DELETE.
POST is not idempotent as it create a new resource.

## 8. What is the role of status codes in RESTFul APIs?

Status codes are used to indicate the result of an HTTP request.

- 1xx: Informational - Request received, continuing process
  - 100: Continue
- 2xx: Success - The action was successful
  - 200: OK
  - 201: Created - The resource has been created
  - 202: Accepted - Request accepted for processing
  - 204: No Content - The server is not returning any content
- 3xx: Redirection - Further action must be taken in order to complete the request
  - 300: Multiple choices
- 4xx: Client Error - The request contains bad syntax or cannot be fulfilled
  - 400: Bad Request
  - 401: Unauthorized
  - 403: Forbidden
  - 404: Not Found
- 5xx: Server Error - The server failed to fulfill an apparently valid request
  - 500: Internal Server Error
  - 501: Not Implemented
  - 502: Bad Gateway
  - 503: Service Unavailable

## 9. What is CORS?

CORS is a security feature provided by the browser that restricts web pages or scripts to making requests to a different domain that the one that served the web page.

CORS restricts acces to resouces if:

- The domain is different
- The protocol is different
- The port is different
- The resource is on a subdomain

## 10. How to remove CORS restrictions?

Can be removed by enabling the CORS middleware

```js
app.use(
  cors({
    origin: 'http://example.com',
  })
);
```

## 11. What is Serialization and Deserialization?

Serialization and Deserialization is a process of converting data from one format to another. Usually, coverting Objeccts to JSON and vice versa.

```js
const user = { id: 1, name: 'John' };

// Serialization
const jsonStr = JSON.stringify(user);

// Deserialization
const deserializedUser = JSON.parse(jsonStr);
```

## 11. What are the types of serialization?

- Binary: Objects are converted to binary format.
- JSON: Objects are converted to JSON format.
- XML: Objects are converted to XML format.

## 12. Explain the concept of versoning in RESTful API?

It is the practice of maitaining mulitple versions of the same API to support backward compatibility.

For example:

- https://api.example.com/v1/users
- https://api.example.com/v2/users

## 13. What is an API document?

An API document desribes the funtionality, features and usages of a REST API.

Some popular docuemntaion formats are:

- Swager (OpenAPI)
- RAML
- API Bleuprint

## 14. What is a typical sturcture of Node.js REST API?

- node_modules
- src
  - controllers
  - models
  - routes
  - utils
  - app.js
- package.json
- .gitignore
- .env

## 15. What are Auhtorization and Authentication?

Authenication is the process of verifying the identity of a user by validating their credentials.

Authorization is the process of allowing an authenticated user to access a specific resource or set of resources.

## 16. What are the 5 types of Authentication?

### 16.1. Basic Authentication

Authentication using username and password.

- It is not secure as the password isn't encoded in the request.

### 16.2. API Key Authentication

Authentication using an API key. passed in the request header.

- The ApiKey can be shared with clients.
- Unwanted clients can access the API.

### 16.3. Token-based Authentication (JWT)

1. Client send a POST request with { username, password }
2. The server will authenticate the user, and generate a token to be sent to the client
3. The client will add the token to the headers of the requests { Authorization: Bearer <token> }
4. The server will validate the token signature

### 16.4. Multi-factor Authentication (MFA)

### 16.5. Certificate-based Authentication

## 17. What is the role of Hashing and Salt in securing passwords?

Hashing is the process of converting a password into a fixed-length hash string of characters using a mathematical alogorithm.

The Salt is a random string of characters that is added to the hash string to make it more difficult to crack (can be generated using bycrypt or other algorithms).

## 18. How to create Hash Passwords in Node.js?

```js
const crypto = require('crypto');

function hashAndSaltPassword(password) {
  // Generate a salt
  const salt = crypto.randomBytes(16).toString('hex');
  // Create a hash object
  const hash = crypto.createHash('sha256');
  // Hash the password
  hash.update(salt + password);
  const hexHash = hash.digest('hex');
  return `${salt}.${hexHash}`;
}
```

## 19. What are the parts of a JWT token?

1. Header: Contains the algorithm used to generate the token
2. Payload: Contains the Claims that are encoded in the token
3. Signature: A string used to verify that it has not been tampered with

```json
// Header
{
  "alg": "HS256",
  "typ": "JWT"
}
// Payload
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}

```
