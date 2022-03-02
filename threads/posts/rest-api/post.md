---
title: 'Lets try to get a quick introduction to the REST API.'
date: 'Feb 24 2022'
---

## You must have heard of the term RESTful API. Let's try to get a quick introduction to the REST API.

Before jumping onto REST

An API is an Application Programming Interface that lets you connect two computers, where one computer or application requests the data from the server.

RESTful APIs are the most famous type of API.

REST APIs are APIs that follow standardized principles, properties, and constraints.

You can access resources in the REST API using HTTP verbs. 👇🏻

Here are a few common HTTP verbs:

📄 GET (read existing data)
📲 POST (create a new response or data)
♻️ PATCH (update the data)
🗑️ DELETE (delete the data)

RESTful API is entirely based on a request/response system.

The client can make requests using HTTP verbs followed by the endpoint. Let's talk a bit about endpoints.

The endpoint (or route) is the URL you request for. The path determines the resource you’re requesting.

When you send a request to an endpoint, the server responds with the relevant data, generally formatted as JSON, XML, plain text, images, HTML, and more.

An actual RESTful API will follow the following constraints. 👇🏻

### Client-Server Architecture

The client requests the data from the server with no third-party interpretation.

### Statelessness

Statelessness means that every HTTP request happens in complete isolation. The client and the server don't need to store any information about each other, and there is no state.

### Cacheability

The response can be cacheable, and it can improve the performance and scalability of an API. Also, cacheability allows the client to get the data even quicker.

### Layering

Different layers of the API architecture should work together, creating a scalable system that is easy to update or adjust.

### Uniform Interface

Communication between the client and the server must be done in a standardized language that is independent of both. This improves scalability and flexibility.

With that being said, this was the quick introduction of REST API in ten tweets.

We hope you find this thread helpful.