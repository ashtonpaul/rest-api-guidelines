# REST API Design Guideline 1.0.0-beta

## Summary
A RESTful API design should be:
- Consistent
- Follows web and HTTP Standards
- Intuitive
- Well documented

## Introduction
As REST APIs become more common in many different backed systems.  the importance of a clean REST API design standard is needed. The concept of REST is to separate the API structure into logical resources. REST APIs should adhere to consistent guidelines to make using them easy and intuitive. This document serves as a starting point to aide in consistent RESTful API design.

## REST API Design Guideline 
1. Version your API in URL (e.g. /api/v1/) Preferably use URL method for versioning. It gives better discoverability of a resource by looking at the URL. Always update the API verion when there are breaking changes. Breaking changes include 
   - removing any part of the API
   - a change in the response type (e.g integer to float)
   - a change in the format of a response data for any call
1. If possible use a subdomain for a shorter concise URL. 
    - GET api.example.com/v1/exmployees vs GET www.example.com/api/v1/employees
1. Ensure CORS is enabled for public access
1. All request should be made over HTTPS (SSL) as a basic security implementation.
1. Use nouns for resource naming
1. Do not use file extensions in the URI
   - BAD: **GET api/v1/employees.json**
   - GOOD: **GET api/v1/employees**
1. Resource names should always be plural
    > GET api/v1/companies
    > GET api/v1/employees
1. Keep using the plural name even for detail endpoints
    > GET api/v1/employees/1
1. Sometimes a relation may exist under another resource (sub-resource). 
   - Use the detail pattern for the parent resource followed by the child resource
    > GET /employees/1/departments/
    > GET /employees/1/departments/4  
1. Do not include trailing foward slashes in the URI. Adds no semantic value and may cause confusion
1. Map your exceptions in an error payload. Each error payload should include a message/reason for the error. If applicable an error code, description and/or link to more information. Errors should include all information the client needs to move forward from the error.
1. Use HTTP headers for Content Negotiation (serialization formats)
   - Content-Type defines the request format. (Content-Type: application/json)
   - Accept defines a list of acceptable response formats.
1. Default Content-Type should be json. If json is the default the field names should be snake case.
1. Allow HTTP Method Overrides. Some proxies do not support arbitrary HTTP methods or newer HTTP methods.
1. Provide filtering, sorting, field selection and paging for collections
1. For pagination use [Link Header](https://tools.ietf.org/html/rfc5988#page-6) protocol. Combine this with a "X-Total-Count" header to indicate the total number of items returned.
1. Limit which fields are returned by the API
    > GET /api/v1/employees?fields=id,first_name,last_name
1. Use nouns for resource names
1. Use UUID if possible instead of resource ids.
   - Keeps business logic away from the consumer of the API
   - It can be a security issue, this way is a preventive practice to aid in managing risks in case of developer mistakes 
1. Use standard (verb) HTTP methods for actions (GET, POST, PUT, DELETE etc)
1. Use standard HTTP status codes 
   - 2xx (Success category)
   - 3xx (Redirection Category)
   - 4xx (Client Error Category)
   - 5xx (Server Error Category)
1. Sorting, filtering, searching and pagination should be done via the query params and the GET method
   - Have aliases for common queries e.g GET /employees/new_hires
1. Use hyphens instead of underscores where necessary in the URI. Never use camel case because of case sensitivity.
1. Always use lowercase letters for URI paths
1. Update (e.g PUT, PATCH) and create (e.g POST) should return the representation of the new resource
   - This prevents (if necessary) the API consumer to hit the API again for the updated resource
   - POST /api/v1/employees for creating a new employee should return a 201 response with
     * a representation of the new employee created
     * A [Location header](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.30) which points to the new URL of the resource
1. For actions that don't require any response object like DELETE, return the appropriate code with an null response
   - For DELETE /api/v1/employees/1 return 204 with response { data: null }
1. If Rate Limiting is necessary, use HTTP code [429](https://tools.ietf.org/html/rfc6585#section-4) for rate limiting exceeded
   - Return the headers X-RateLimit-Limit, X-RateLimit-Remaining, X-RateLimit-Reset (although non standard they seem to be a widely used combination)
   - Response should include details explaining the condition of the rate-limit
   - Optional to include a Retry-After header within the 429 response
   - Don't use unix timestamp for X-Rate-Limit-Reset, use number of seconds
1. Use HATEOS (Hypermedia as the Engine of Application State) for better navigation through the API and this prevents the client from having to construct URIs.
1. Be mindful about Idempotence. Safe methods like GET, HEAD, OPTIONS should return the same result every time and should only be used for retrieving data and not changing any data. Use the appropriate actions e.g DELETE, PUT for such.
1. Keep Authorization and Authentication stateless. Don't use sessions to store authentication information for the API, each request should be self-sufficient.
1. Gzip and/or deflate should be supported. This should be expressed in the Content-Encoding header.
1. Envelope your data e.g { data: [{ ... }, { ... }]} This allows for relialby testing for response data, e.g if response['data'] does not exist, then check response['error'] to figure out why. This reduces the need of having to parse returned data to figure out if its an error or not consistently. 

## FAQ
1. **Frequently Asked Question 1**
    > Response to frequently asked question 1
1. **Frequently Asked Question 2**
    > Response to frequently asked question 2
1. **Frequently Asked Question 3**
    > Response to frequently asked question 3

## About
The REST API Design Guideline specification is authored by [Ashton Paul](https://ashtonpaul.com)

If you'd like to leave feedback, please [open an issue on Github](https://github.com/jusdev)

## License
[Creative Commons - CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)
