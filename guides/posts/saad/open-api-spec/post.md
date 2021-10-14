---
title: What is OpenAPI spec?
slug: open-api-spec
description: There are different kinds of specifications available that you can use while building an API.
publishedDate: 2021-10-13T11:27:45.681Z
lastModifiedDate: 2021-10-13T11:27:45.681Z
authors:
    - saad
category: api
tags:
    - api
    - open-api
    - specs
coverImage: ''
draft: false
---

<Lead>
There are different kinds of specifications available that you can use while building an API. These specifications provide a standard for data exchange between web services, and one of these specifications is REST that further follows OpenAPI specifications.
</Lead>

## OpenAPI Specification

It is a format to define structure and syntax for REST APIs. It provides a standard that allows both humans and computers to discover and understand the service's capabilities without access to source code, documentation, or traffic inspection. The OpenAPI document defines or describes an API.

## OpenAPI Document

The OpenAPI specification document can use either JSON or YAML for describing the API’s capabilities. Both of these formats include the same elements. All the field names in the specification are case-sensitive, and this consists of all fields that are used as keys in a map, except where explicitly noted that keys are case-insensitive.

The schema exposes two types of fields: Fixed fields and Patterned fields. Fixed fields have declared names, whereas Patterned fields are the ones that declare the regex patterns for the field name.

## Benefits of OpenAPI Document

Working with the API becomes streamlined once you have a complete description of how the REST API works. The OpenAPI specifications document helps you to do this. For instance, it enables you to curate accurate documentation and helps you with the stub code for API development.

The OpenAPI specification document also contributes toward better collaboration across teams. The frontend team does not have to wait for the backend to be completed, and they can use the specification to start developing the frontend.