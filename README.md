# Fake Restaurant API

## Table of Contents

- [1. Introduction](#1-introduction)
  - [1.1 Purpose](#11-purpose)
  - [1.2 Scope](#12-scope)
  - [1.3 Intended Audience](#13-intended-audience)
- [2. System Overview](#2-system-overview)
  - [2.1 Architecture](#21-architecture)
  - [2.2 Technology Stack](#22-technology-stack)
  - [2.3 Features Summary](#23-features-summary)
- [3. Getting Started](#3-getting-started)
  - [3.1 Prerequisites](#31-prerequisites)
  - [3.2 Installation](#32-installation)
  - [3.3 Running the Application](#33-running-the-application)
- [4. API Reference](#4-api-reference)
  - [4.1 Order Endpoints](#41-order-endpoints)
    - [4.1.1 POST /api/Order/{restaurantid}/makeorder](#411-post-apiorderrestaurantidmakeorder)
    - [4.1.2 GET /api/Order](#412-get-apiorder)
    - [4.1.3 DELETE /api/Order/{Order_id}](#413-delete-apiorderorder_id)
    - [4.1.4 DELETE /api/Order/master/{master_id}](#414-delete-apiordermastermaster_id)
    - [4.1.5 GET /api/Order/{id}](#415-get-apiorderid)
  - [4.2 Restaurant Endpoints](#42-restaurant-endpoints)
    - [4.2.1 GET /api/Restaurant](#421-get-apirestaurant)
    - [4.2.2 POST /api/Restaurant](#422-post-apirestaurant)
    - [4.2.3 GET /api/Restaurant/{Restaurant_id}](#423-get-apirestaurantrestaurant_id)
    - [4.2.4 GET /api/Restaurant/{Restaurant_id}/menu](#424-get-apirestaurantrestaurant_idmenu)
    - [4.2.5 POST /api/Restaurant/{Restaurant_id}/additem](#425-post-apirestaurantrestaurant_idadditem)
    - [4.2.6 GET /api/Restaurant/items](#426-get-apirestaurantitems)
  - [4.3 User Endpoints](#43-user-endpoints)
    - [4.3.1 POST /api/User/register](#431-post-apiuserregister)
    - [4.3.2 GET /api/User/getusercode](#432-get-apiusergetusercode)
    - [4.3.3 GET /api/User](#433-get-apiuser)
    - [4.3.4 DELETE /api/User/{apikey}](#434-delete-apiuserapikey)
    - [4.3.5 PUT /api/User/{apikey}](#435-put-apiuserapikey)
- [5. Data Models](#5-data-models)
  - [5.1 Order](#51-order)
  - [5.2 Restaurant](#52-restaurant)
  - [5.3 Menu Item](#53-menu-item)
  - [5.4 User](#54-user)
- [6. Authentication](#6-authentication)
- [7. Error Handling](#7-error-handling)
- [8. Contributing](#8-contributing)
- [9. Legal Notice and Media Policy](#9-legal-notice-and-media-policy)

---

## 1. Introduction

### 1.1 Purpose

The Fake Restaurant API is a simple RESTful web service that
simulates the data and behavior of a restaurant ordering system.
It is intended for testing, learning, and development purposes.
The API provides mock data and endpoints that imitate real-world
restaurant operations, such as retrieving restaurant details,
viewing menus, placing orders, and managing users.

This document serves as the complete reference for developers,
testers, and contributors who need to understand, use, or extend
the API.

### 1.2 Scope

This documentation covers:

- The system architecture and technology stack.
- Instructions for installing and running the application.
- A complete reference for every API endpoint, including
  request and response formats.
- The data models used by the application.
- Guidelines for contributing to the project.
- Legal and media usage policies.

This documentation does not cover the internal source code
implementation of the API. It focuses on behavior, usage, and
integration.

### 1.3 Intended Audience

This document is written for:

- Software developers who want to integrate with or extend
  the API.
- Testers who need to validate API behavior.
- Students and beginners learning ASP.NET Core and Entity
  Framework Core.
- Contributors who want to improve the project.

Readers are expected to have a basic understanding of REST
APIs, HTTP methods, and JSON data format. No prior knowledge
of ASP.NET Core is required, but it is helpful.

---

## 2. System Overview

### 2.1 Architecture

The Fake Restaurant API follows a standard layered architecture
typical of ASP.NET Core applications:

| Layer | Responsibility |
|-------|----------------|
| Controllers | Handle incoming HTTP requests and return responses. |
| Services (if present) | Contain business logic and coordinate operations. |
| Data Access Layer | Uses Entity Framework Core to interact with the database. |
| Models | Represent the data structures used by the API. |

The API is stateless. Each request contains all the information
needed to process it. Authentication is simulated and does not
rely on external identity providers.

### 2.2 Technology Stack

The following technologies are used in this project:

| Technology | Version | Purpose |
|------------|---------|---------|
| ASP.NET Core | .NET 8.0 | Framework for building the REST API. |
| Entity Framework Core | Compatible with .NET 8.0 | ORM for database interaction. |
| JSON | Standard | Data format for API requests and responses. |
| .NET | 8.0 | Runtime platform for the application. |

### 2.3 Features Summary

The API provides the following features:

- **Restaurant Details:** Retrieve information about a
  restaurant.
- **Menu:** Fetch the menu of a restaurant, including item
  names, descriptions, and prices.
- **Orders:** Place new orders and view existing orders.
- **Order History:** View past orders made by customers.
- **Authentication:** Simulate basic authentication using
  user codes and API keys.

---

## 3. Getting Started

### 3.1 Prerequisites

Before running the application, ensure the following tools
are installed:

- .NET 8.0 SDK or later.
- A code editor such as Visual Studio, Visual Studio Code,
  or JetBrains Rider.
- A database supported by Entity Framework Core, such as
  SQL Server, SQLite, or InMemory (for testing).
- Git, if you plan to clone the repository.

### 3.2 Installation

Follow these steps to install the project:

1. Clone the repository:

   ```
   git clone https://github.com/your-org/fake-restaurant-api.git
   ```

2. Navigate to the project directory:

   ```
   cd fake-restaurant-api
   ```

3. Restore dependencies:

   ```
   dotnet restore
   ```

4. Apply database migrations (if applicable):

   ```
   dotnet ef database update
   ```

### 3.3 Running the Application

To run the application:

1. Build the project:

   ```
   dotnet build
   ```

2. Run the application:

   ```
   dotnet run
   ```

3. Open a browser or API client and navigate to the base URL,
   for example:

   ```
   https://localhost:5001/swagger
   ```

   The Swagger UI provides an interactive interface for
   testing all endpoints.

---

## 4. API Reference

This section describes every endpoint provided by the API.
Each entry includes the HTTP method, the URL pattern, a
description, request parameters, and example responses where
applicable.

### 4.1 Order Endpoints

#### 4.1.1 POST /api/Order/{restaurantid}/makeorder

**Description:** Place a new order for a specific restaurant.

**Path Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| restaurantid | integer | The unique identifier of the restaurant. |

**Request Body:** An Order object containing the items and
customer details.

**Response:** Returns the created order with its assigned
identifier.

**Status Codes:**

| Code | Meaning |
|------|---------|
| 201 | Order created successfully. |
| 400 | Invalid request data. |
| 404 | Restaurant not found. |

#### 4.1.2 GET /api/Order

**Description:** Retrieve all orders.

**Response:** Returns a list of Order objects.

**Status Codes:**

| Code | Meaning |
|------|---------|
| 200 | Orders retrieved successfully. |

#### 4.1.3 DELETE /api/Order/{Order_id}

**Description:** Delete a specific order by its identifier.

**Path Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| Order_id | integer | The unique identifier of the order. |

**Status Codes:**

| Code | Meaning |
|------|---------|
| 204 | Order deleted successfully. |
| 404 | Order not found. |

#### 4.1.4 DELETE /api/Order/master/{master_id}

**Description:** Delete all orders associated with a master
identifier.

**Path Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| master_id | integer | The master identifier linking multiple orders. |

**Status Codes:**

| Code | Meaning |
|------|---------|
| 204 | Orders deleted successfully. |
| 404 | No orders found for the given master identifier. |

#### 4.1.5 GET /api/Order/{id}

**Description:** Retrieve details of a specific order by its
identifier.

**Path Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| id | integer | The unique identifier of the order. |

**Response:** Returns an Order object.

**Status Codes:**

| Code | Meaning |
|------|---------|
| 200 | Order retrieved successfully. |
| 404 | Order not found. |

### 4.2 Restaurant Endpoints

#### 4.2.1 GET /api/Restaurant

**Description:** Retrieve a list of all restaurants.

**Response:** Returns a list of Restaurant objects.

**Status Codes:**

| Code | Meaning |
|------|---------|
| 200 | Restaurants retrieved successfully. |

#### 4.2.2 POST /api/Restaurant

**Description:** Create a new restaurant.

**Request Body:** A Restaurant object containing the
restaurant details.

**Response:** Returns the created restaurant with its
assigned identifier.

**Status Codes:**

| Code | Meaning |
|------|---------|
| 201 | Restaurant created successfully. |
| 400 | Invalid request data. |

#### 4.2.3 GET /api/Restaurant/{Restaurant_id}

**Description:** Retrieve details of a specific restaurant.

**Path Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| Restaurant_id | integer | The unique identifier of the restaurant. |

**Response:** Returns a Restaurant object.

**Status Codes:**

| Code | Meaning |
|------|---------|
| 200 | Restaurant retrieved successfully. |
| 404 | Restaurant not found. |

#### 4.2.4 GET /api/Restaurant/{Restaurant_id}/menu

**Description:** Retrieve the menu of a specific restaurant.

**Path Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| Restaurant_id | integer | The unique identifier of the restaurant. |

**Response:** Returns a list of Menu Item objects.

**Status Codes:**

| Code | Meaning |
|------|---------|
| 200 | Menu retrieved successfully. |
| 404 | Restaurant not found. |

#### 4.2.5 POST /api/Restaurant/{Restaurant_id}/additem

**Description:** Add a new menu item to a specific restaurant.

**Path Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| Restaurant_id | integer | The unique identifier of the restaurant. |

**Request Body:** A Menu Item object containing the item
details.

**Response:** Returns the created menu item.

**Status Codes:**

| Code | Meaning |
|------|---------|
| 201 | Menu item created successfully. |
| 400 | Invalid request data. |
| 404 | Restaurant not found. |

#### 4.2.6 GET /api/Restaurant/items

**Description:** Retrieve a list of all menu items across all
restaurants.

**Response:** Returns a list of Menu Item objects.

**Status Codes:**

| Code | Meaning |
|------|---------|
| 200 | Items retrieved successfully. |

### 4.3 User Endpoints

#### 4.3.1 POST /api/User/register

**Description:** Register a new user.

**Request Body:** A User object containing the registration
details.

**Response:** Returns the created user with an assigned API
key.

**Status Codes:**

| Code | Meaning |
|------|---------|
| 201 | User registered successfully. |
| 400 | Invalid request data. |

#### 4.3.2 GET /api/User/getusercode

**Description:** Retrieve the user code for a user.

**Query Parameters:** May require identifying information
such as email or username.

**Response:** Returns the user code associated with the user.

**Status Codes:**

| Code | Meaning |
|------|---------|
| 200 | User code retrieved successfully. |
| 404 | User not found. |

#### 4.3.3 GET /api/User

**Description:** Retrieve a list of all users.

**Response:** Returns a list of User objects.

**Status Codes:**

| Code | Meaning |
|------|---------|
| 200 | Users retrieved successfully. |

#### 4.3.4 DELETE /api/User/{apikey}

**Description:** Delete a user by their API key.

**Path Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| apikey | string | The API key of the user. |

**Status Codes:**

| Code | Meaning |
|------|---------|
| 204 | User deleted successfully. |
| 404 | User not found. |

#### 4.3.5 PUT /api/User/{apikey}

**Description:** Update user details by their API key.

**Path Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| apikey | string | The API key of the user. |

**Request Body:** A User object containing the updated
details.

**Response:** Returns the updated user.

**Status Codes:**

| Code | Meaning |
|------|---------|
| 200 | User updated successfully. |
| 400 | Invalid request data. |
| 404 | User not found. |

---

## 5. Data Models

This section describes the main data models used by the API.
Each model represents a resource that can be created,
retrieved, updated, or deleted through the API.

### 5.1 Order

The Order model represents a customer order placed at a
restaurant.

| Field | Type | Description |
|-------|------|-------------|
| Id | integer | Unique identifier of the order. |
| RestaurantId | integer | Identifier of the restaurant where the order was placed. |
| MasterId | integer | Identifier linking related orders. |
| Items | list | List of menu items included in the order. |
| TotalPrice | decimal | Total price of the order. |
| CreatedAt | datetime | Date and time when the order was created. |

### 5.2 Restaurant

The Restaurant model represents a restaurant registered in
the system.

| Field | Type | Description |
|-------|------|-------------|
| Id | integer | Unique identifier of the restaurant. |
| Name | string | Name of the restaurant. |
| Address | string | Physical address of the restaurant. |
| Menu | list | List of menu items offered by the restaurant. |

### 5.3 Menu Item

The Menu Item model represents a single item on a restaurant
menu.

| Field | Type | Description |
|-------|------|-------------|
| Id | integer | Unique identifier of the menu item. |
| RestaurantId | integer | Identifier of the restaurant offering the item. |
| Name | string | Name of the item. |
| Description | string | Description of the item. |
| Price | decimal | Price of the item. |

### 5.4 User

The User model represents a registered user of the API.

| Field | Type | Description |
|-------|------|-------------|
| Id | integer | Unique identifier of the user. |
| Name | string | Name of the user. |
| Email | string | Email address of the user. |
| ApiKey | string | API key used for authentication. |
| UserCode | string | User code assigned during registration. |

---

## 6. Authentication

The Fake Restaurant API uses simulated authentication. This
means that authentication is not connected to any external
identity provider. Instead, the API issues an API key or
user code when a user registers.

To authenticate a request, include the API key in the request
header or as a query parameter, depending on the endpoint.
The exact method is defined by the API implementation.

This authentication model is intended for testing and
development only. It does not provide the security guarantees
required for production systems.

---

## 7. Error Handling

The API returns standard HTTP status codes to indicate the
outcome of a request. Common codes include:

| Code | Meaning |
|------|---------|
| 200 | Success. |
| 201 | Resource created. |
| 204 | Success with no content. |
| 400 | Bad request. The request data is invalid. |
| 404 | Resource not found. |
| 500 | Internal server error. |

Where applicable, the response body includes a message
describing the error.

---

## 8. Contributing

Contributions to the Fake Restaurant API are welcome. Whether
you are an experienced developer or just getting started with
.NET Web APIs, your input is valued.

To contribute:

1. Fork the repository.
2. Create a feature branch:

   ```
   git checkout -b feature-xyz
   ```

3. Commit your changes:

   ```
   git commit -am 'Add feature xyz'
   ```

4. Push to the branch:

   ```
   git push origin feature-xyz
   ```

5. Open a pull request.

Please ensure that your contributions follow the existing
coding style and include appropriate documentation.

---

## 9. Legal Notice and Media Policy

```
UNDER NO CIRCUMSTANCES SHOULD IMAGES OR EMOJIS BE INCLUDED
DIRECTLY IN THIS FILE. ALL VISUAL MEDIA, INCLUDING
SCREENSHOTS AND IMAGES OF THE APPLICATION, MUST BE STORED IN
A DEDICATED FOLDER WITHIN THE PROJECT DIRECTORY. THIS FOLDER
SHOULD BE CLEARLY STRUCTURED AND NAMED ACCORDINGLY TO
INDICATE THAT IT CONTAINS ALL VISUAL CONTENT RELATED TO THE
APPLICATION, FOR EXAMPLE A FOLDER NAMED IMAGES, SCREENSHOTS,
OR MEDIA. THE AUTHOR IS NOT LIABLE OR RESPONSIBLE FOR ANY
MALFUNCTIONS, DEFECTS, OR ISSUES THAT MAY OCCUR AS A RESULT
OF COPYING, MODIFYING, OR USING THIS SOFTWARE. IF ANY
PROBLEMS OR ERRORS ARE ENCOUNTERED, PLEASE DO NOT ATTEMPT TO
FIX THEM SILENTLY OR OUTSIDE THE PROJECT. INSTEAD, SUBMIT A
PULL REQUEST OR OPEN AN ISSUE ON THE CORRESPONDING GITHUB
REPOSITORY SO THAT IT CAN BE ADDRESSED APPROPRIATELY BY THE
MAINTAINERS OR CONTRIBUTORS.
```

---

*END OF DOCUMENT*

---
