# REST API Design Guideline 1.0.0-beta

## Summary
A RESTful API design should be:
- Consistent
- Follows web and HTTP Standards
- Intuitive
- Well documented

## Introduction
As REST APIs become more common in many different backed systems.  the importance of a clean REST API design standard is needed. The concept of REST is to separate the API structure into logical resources. REST APIs should adhere to consistent guidelines to make using them easy and intuitive. This document serves as a starting point to aide in consistent RESTful API design.

## REST API Design Guideline Specification
1. Version your API in URL (e.g. /api/v1/)
1. Use nouns for resouce naming
1.  Resource names should always be plural
> GET api/v1/companies
> GET api/v1/employees
1. Keep using the plural name even for detail endpoints
  GET api/v1/employees/1
1. Sometimes a relation may exist under another resource (sub-resource). 
 - Use the detail pattern for the parent resource followed by the child resource
> GET /employees/1/departments/
> GET /employees/1/departments/4  
1. Use standard HTTP status codes (e.g. 200 – OK, 400 – Bad Request)
1. Map your exceptions in an error payload. Each error payload should include a message/reason for the error. If applicable an error code and/or link to more information.
1. Use HTTP headers for Content Negotiation (serialization formats)
Content-Type defines the request format.
Accept defines a list of acceptable response formats.
1. Allow HTTP Method Overrides. Some proxies do not support arbitrary HTTP methods or newer HTTP methods.
1. Provide filtering, sorting, field selection and paging for collections
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
1. Update (e.g PUT) and create (e.g POST) should return the representation of the new resource
- This prevents (if necessary) the API consumer to hit the API again for the updated resource
- POST /api/v1/employees for creating a new employee should return a 201 response with
  a) a representation of the new employee created
  b) A [Location header](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.30) which points to the new URL of the resource
1. If Rate Limiting is necessary, use HTTP code [429](https://tools.ietf.org/html/rfc6585#section-4) for rate limiting exceeded
- Return the headers X-RateLimit-Limit, X-RateLimit-Remaining, X-RateLimit-Reset (although non standard they seem to be a widely used combination)
- Reponse should include details explaining the condition of the rate-limit
- Optional to include a Retry-After header within the 429 response
1. Use HATEOS (Hypermedia as the Engine of Application State) for better navigation through the API

## FAQ
1. **Frequently Asked Question 1** 
 Response to frequently asked question 1
1. **Frequently Asked Question 2**
Response to frequently asked question 2
1. **Frequently Asked Question 3**
Response to frequently asked question 3

## About
The REST API Design Guideline specification is authored by [Ashton Paul](https://ashtonpaul.com)

If you'd like to leave feedback, please [open an issue on Github](https://github.com/jusdev)

## License
[Creative Commons - CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)

