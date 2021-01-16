# serverless-dotnet-web-api
A library to help you building efficient AWS Lambda functions, which are triggered by an HTTP API Gateway

## Why?

I started building AWS Lambda functions connected to an HTTP API Gateway and I was unhappy with the choices I've found:

1. use a huge framework like ASP.Net Core, which is built on reflection and therefore slow
    - Don't get me wrong, I love ASP.Net Core as a framework for a monolith, even micro services, and it's extremely fast and efficient for those use cases. But not for Lambda functions.
2. work directly with the native APIs. 
    - Those APIs are actually good enough for the first few functions, so I stuck with that for a while, but it got very quickly out of hand.

## Design goals

- Make it easy to have multiple HTTP API Gateway events pointing to the same AWS Lambda function.
    - For this we need a simple router. The simpler and faster, the better.
- Lavarage HTTP API Gatway features.
    - The object you get as an event is very detailed and easy to use. This library should lavarage all those properties, instead of parsing raw query strings.
- Allow defining a pipline. This could be used for ...
    - Exception handling
    - Checking headers, such as content type or authorization (authentication should be checked by the HTTP API Gateway)
    - Compression / post processing
- Make it easy to respond with data objects, instead of creating the Response object manually every time
- Optimize it for JSON (and System.Text.Json)
- Make monitoring easy (logging, AWS X-Ray, other APM services)

### This is not meant to be a framework

It's mean to be a libray of tools, built directly on the .Net Core 3.1 API and AWS SDKs, trying to limit any heavy weight dependencies.
