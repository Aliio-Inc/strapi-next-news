# API Documentation for Next News

Welcome to the **Next News** API documentation! This guide provides comprehensive information about the available API endpoints, their functionalities, request and response structures, authentication methods, and usage examples. Whether you're a developer looking to integrate with Next News or extend its capabilities, this documentation will help you navigate the API effectively.

## Table of Contents

- [Authentication](#authentication)
  - [Register](#register)
  - [Login](#login)
  - [JWT Tokens](#jwt-tokens)
- [Endpoints](#endpoints)
  - [Articles](#articles)
    - [Get All Articles](#get-all-articles)
    - [Get Single Article](#get-single-article)
    - [Create an Article](#create-an-article)
    - [Update an Article](#update-an-article)
    - [Delete an Article](#delete-an-article)
  - [Categories](#categories)
    - [Get All Categories](#get-all-categories)
    - [Get Single Category](#get-single-category)
    - [Create a Category](#create-a-category)
    - [Update a Category](#update-a-category)
    - [Delete a Category](#delete-a-category)
  - [Authors](#authors)
    - [Get All Authors](#get-all-authors)
    - [Get Single Author](#get-single-author)
    - [Create an Author](#create-an-author)
    - [Update an Author](#update-an-author)
    - [Delete an Author](#delete-an-author)
- [Request Structure](#request-structure)
- [Response Structure](#response-structure)
- [Error Handling](#error-handling)
- [Rate Limiting](#rate-limiting)
- [Examples](#examples)
  - [Using cURL](#using-curl)
  - [Using JavaScript (Fetch API)](#using-javascript-fetch-api)
- [Best Practices](#best-practices)
- [Additional Resources](#additional-resources)

## Authentication

Authentication is required for accessing protected endpoints such as creating, updating, or deleting content. Next News uses JSON Web Tokens (JWT) for secure authentication.

### Register

**Endpoint:** `/api/auth/register`  
**Method:** `POST`

**Description:** Registers a new user.

**Request Body:**

```json
{
  "username": "john_doe",
  "email": "john@example.com",
  "password": "securePassword123"
}
```

**Response:**

```json
{
  "jwt": "your_jwt_token",
  "user": {
    "id": 1,
    "username": "john_doe",
    "email": "john@example.com",
    "created_at": "2024-04-27T12:34:56.789Z",
    "updated_at": "2024-04-27T12:34:56.789Z"
  }
}
```

### Login

**Endpoint:** `/api/auth/login`  
**Method:** `POST`

**Description:** Authenticates a user and returns a JWT.

**Request Body:**

```json
{
  "identifier": "john@example.com",
  "password": "securePassword123"
}
```

**Response:**

```json
{
  "jwt": "your_jwt_token",
  "user": {
    "id": 1,
    "username": "john_doe",
    "email": "john@example.com",
    "created_at": "2024-04-27T12:34:56.789Z",
    "updated_at": "2024-04-27T12:34:56.789Z"
  }
}
```

### JWT Tokens

- **Usage:** Include the JWT token in the `Authorization` header for protected requests.
- **Format:** `Bearer your_jwt_token`
- **Example Header:**

  ```
  Authorization: Bearer your_jwt_token
  ```

## Endpoints

### Articles

#### Get All Articles

**Endpoint:** `/api/articles`  
**Method:** `GET`

**Description:** Retrieves a list of all published articles.

**Query Parameters:**

- `?populate=*` - Populates related fields such as author and category.
- `?pagination[page]=1&pagination[pageSize]=10` - Paginates the results.

**Response:**

```json
{
  "data": [
    {
      "id": 1,
      "attributes": {
        "title": "Breaking News: AI Revolutionizes Tech",
        "content": "Lorem ipsum dolor sit amet...",
        "published_at": "2024-04-27T10:00:00.000Z",
        "author": {
          "data": {
            "id": 2,
            "attributes": {
              "name": "Jane Smith",
              "bio": "Tech enthusiast and writer.",
              "profile_picture": {
                "data": {
                  "id": 3,
                  "attributes": {
                    "url": "/uploads/jane_smith.jpg"
                  }
                }
              }
            }
          }
        },
        "category": {
          "data": {
            "id": 1,
            "attributes": {
              "name": "Technology",
              "description": "Latest updates in technology."
            }
          }
        },
        "featured_image": {
          "data": {
            "id": 4,
            "attributes": {
              "url": "/uploads/ai_revolution.jpg"
            }
          }
        }
      }
    }
    // More articles...
  ],
  "meta": {
    "pagination": {
      "page": 1,
      "pageSize": 10,
      "pageCount": 5,
      "total": 50
    }
  }
}
```

#### Get Single Article

**Endpoint:** `/api/articles/:id`  
**Method:** `GET`

**Description:** Retrieves a single article by its ID.

**Path Parameters:**

- `:id` - The ID of the article.

**Response:**

```json
{
  "data": {
    "id": 1,
    "attributes": {
      "title": "Breaking News: AI Revolutionizes Tech",
      "content": "Lorem ipsum dolor sit amet...",
      "published_at": "2024-04-27T10:00:00.000Z",
      "author": {
        "data": {
          "id": 2,
          "attributes": {
            "name": "Jane Smith",
            "bio": "Tech enthusiast and writer.",
            "profile_picture": {
              "data": {
                "id": 3,
                "attributes": {
                  "url": "/uploads/jane_smith.jpg"
                }
              }
            }
          }
        }
      },
      "category": {
        "data": {
          "id": 1,
          "attributes": {
            "name": "Technology",
            "description": "Latest updates in technology."
          }
        }
      },
      "featured_image": {
        "data": {
          "id": 4,
          "attributes": {
            "url": "/uploads/ai_revolution.jpg"
          }
        }
      }
    }
  }
}
```

#### Create an Article

**Endpoint:** `/api/articles`  
**Method:** `POST`  
**Authentication:** Required (Admin, Editor, Author)

**Description:** Creates a new article.

**Request Body:**

```json
{
  "data": {
    "title": "New Innovations in Renewable Energy",
    "content": "Detailed content about renewable energy...",
    "published_at": "2024-05-01T08:00:00.000Z",
    "author": 2,
    "category": 1,
    "featured_image": 5
  }
}
```

**Response:**

```json
{
  "data": {
    "id": 6,
    "attributes": {
      "title": "New Innovations in Renewable Energy",
      "content": "Detailed content about renewable energy...",
      "published_at": "2024-05-01T08:00:00.000Z",
      "author": {
        "data": {
          "id": 2,
          "attributes": {
            "name": "Jane Smith",
            "bio": "Tech enthusiast and writer.",
            "profile_picture": {
              "data": {
                "id": 3,
                "attributes": {
                  "url": "/uploads/jane_smith.jpg"
                }
              }
            }
          }
        }
      },
      "category": {
        "data": {
          "id": 1,
          "attributes": {
            "name": "Technology",
            "description": "Latest updates in technology."
          }
        }
      },
      "featured_image": {
        "data": {
          "id": 5,
          "attributes": {
            "url": "/uploads/renewable_energy.jpg"
          }
        }
      }
    }
  }
}
```

#### Update an Article

**Endpoint:** `/api/articles/:id`  
**Method:** `PUT`  
**Authentication:** Required (Admin, Editor, Author)

**Description:** Updates an existing article by its ID.

**Path Parameters:**

- `:id` - The ID of the article to update.

**Request Body:**

```json
{
  "data": {
    "title": "Updated Innovations in Renewable Energy",
    "content": "Updated detailed content about renewable energy..."
  }
}
```

**Response:**

```json
{
  "data": {
    "id": 6,
    "attributes": {
      "title": "Updated Innovations in Renewable Energy",
      "content": "Updated detailed content about renewable energy...",
      "published_at": "2024-05-01T08:00:00.000Z",
      "author": {
        "data": {
          "id": 2,
          "attributes": {
            "name": "Jane Smith",
            "bio": "Tech enthusiast and writer.",
            "profile_picture": {
              "data": {
                "id": 3,
                "attributes": {
                  "url": "/uploads/jane_smith.jpg"
                }
              }
            }
          }
        }
      },
      "category": {
        "data": {
          "id": 1,
          "attributes": {
            "name": "Technology",
            "description": "Latest updates in technology."
          }
        }
      },
      "featured_image": {
        "data": {
          "id": 5,
          "attributes": {
            "url": "/uploads/renewable_energy.jpg"
          }
        }
      }
    }
  }
}
```

#### Delete an Article

**Endpoint:** `/api/articles/:id`  
**Method:** `DELETE`  
**Authentication:** Required (Admin, Editor)

**Description:** Deletes an article by its ID.

**Path Parameters:**

- `:id` - The ID of the article to delete.

**Response:**

```json
{
  "data": {
    "id": 6,
    "attributes": {
      "title": "Updated Innovations in Renewable Energy",
      "content": "Updated detailed content about renewable energy...",
      "published_at": "2024-05-01T08:00:00.000Z",
      "author": {
        "data": {
          "id": 2,
          "attributes": {
            "name": "Jane Smith",
            "bio": "Tech enthusiast and writer.",
            "profile_picture": {
              "data": {
                "id": 3,
                "attributes": {
                  "url": "/uploads/jane_smith.jpg"
                }
              }
            }
          }
        }
      },
      "category": {
        "data": {
          "id": 1,
          "attributes": {
            "name": "Technology",
            "description": "Latest updates in technology."
          }
        }
      },
      "featured_image": {
        "data": {
          "id": 5,
          "attributes": {
            "url": "/uploads/renewable_energy.jpg"
          }
        }
      }
    }
  }
}
```

### Categories

#### Get All Categories

**Endpoint:** `/api/categories`  
**Method:** `GET`

**Description:** Retrieves a list of all categories.

**Query Parameters:**

- `?populate=*` - Populates related fields if any.

**Response:**

```json
{
  "data": [
    {
      "id": 1,
      "attributes": {
        "name": "Technology",
        "description": "Latest updates in technology."
      }
    }
    // More categories...
  ]
}
```

#### Get Single Category

**Endpoint:** `/api/categories/:id`  
**Method:** `GET`

**Description:** Retrieves a single category by its ID.

**Path Parameters:**

- `:id` - The ID of the category.

**Response:**

```json
{
  "data": {
    "id": 1,
    "attributes": {
      "name": "Technology",
      "description": "Latest updates in technology."
    }
  }
}
```

#### Create a Category

**Endpoint:** `/api/categories`  
**Method:** `POST`  
**Authentication:** Required (Admin, Editor)

**Description:** Creates a new category.

**Request Body:**

```json
{
  "data": {
    "name": "Health",
    "description": "Updates and news on health and wellness."
  }
}
```

**Response:**

```json
{
  "data": {
    "id": 2,
    "attributes": {
      "name": "Health",
      "description": "Updates and news on health and wellness."
    }
  }
}
```

#### Update a Category

**Endpoint:** `/api/categories/:id`  
**Method:** `PUT`  
**Authentication:** Required (Admin, Editor)

**Description:** Updates an existing category by its ID.

**Path Parameters:**

- `:id` - The ID of the category to update.

**Request Body:**

```json
{
  "data": {
    "description": "Comprehensive updates and news on health, wellness, and medical advancements."
  }
}
```

**Response:**

```json
{
  "data": {
    "id": 2,
    "attributes": {
      "name": "Health",
      "description": "Comprehensive updates and news on health, wellness, and medical advancements."
    }
  }
}
```

#### Delete a Category

**Endpoint:** `/api/categories/:id`  
**Method:** `DELETE`  
**Authentication:** Required (Admin, Editor)

**Description:** Deletes a category by its ID.

**Path Parameters:**

- `:id` - The ID of the category to delete.

**Response:**

```json
{
  "data": {
    "id": 2,
    "attributes": {
      "name": "Health",
      "description": "Comprehensive updates and news on health, wellness, and medical advancements."
    }
  }
}
```

### Authors

#### Get All Authors

**Endpoint:** `/api/authors`  
**Method:** `GET`

**Description:** Retrieves a list of all authors.

**Query Parameters:**

- `?populate=*` - Populates related fields if any.

**Response:**

```json
{
  "data": [
    {
      "id": 2,
      "attributes": {
        "name": "Jane Smith",
        "bio": "Tech enthusiast and writer.",
        "profile_picture": {
          "data": {
            "id": 3,
            "attributes": {
              "url": "/uploads/jane_smith.jpg"
            }
          }
        }
      }
    }
    // More authors...
  ]
}
```

#### Get Single Author

**Endpoint:** `/api/authors/:id`  
**Method:** `GET`

**Description:** Retrieves a single author by their ID.

**Path Parameters:**

- `:id` - The ID of the author.

**Response:**

```json
{
  "data": {
    "id": 2,
    "attributes": {
      "name": "Jane Smith",
      "bio": "Tech enthusiast and writer.",
      "profile_picture": {
        "data": {
          "id": 3,
          "attributes": {
            "url": "/uploads/jane_smith.jpg"
          }
        }
      }
    }
  }
}
```

#### Create an Author

**Endpoint:** `/api/authors`  
**Method:** `POST`  
**Authentication:** Required (Admin, Editor)

**Description:** Creates a new author profile.

**Request Body:**

```json
{
  "data": {
    "name": "John Doe",
    "bio": "Journalist with a passion for uncovering the truth.",
    "profile_picture": 6
  }
}
```

**Response:**

```json
{
  "data": {
    "id": 3,
    "attributes": {
      "name": "John Doe",
      "bio": "Journalist with a passion for uncovering the truth.",
      "profile_picture": {
        "data": {
          "id": 6,
          "attributes": {
            "url": "/uploads/john_doe.jpg"
          }
        }
      }
    }
  }
}
```

#### Update an Author

**Endpoint:** `/api/authors/:id`  
**Method:** `PUT`  
**Authentication:** Required (Admin, Editor)

**Description:** Updates an existing author profile by their ID.

**Path Parameters:**

- `:id` - The ID of the author to update.

**Request Body:**

```json
{
  "data": {
    "bio": "Seasoned journalist specializing in investigative reporting."
  }
}
```

**Response:**

```json
{
  "data": {
    "id": 3,
    "attributes": {
      "name": "John Doe",
      "bio": "Seasoned journalist specializing in investigative reporting.",
      "profile_picture": {
        "data": {
          "id": 6,
          "attributes": {
            "url": "/uploads/john_doe.jpg"
          }
        }
      }
    }
  }
}
```

#### Delete an Author

**Endpoint:** `/api/authors/:id`  
**Method:** `DELETE`  
**Authentication:** Required (Admin, Editor)

**Description:** Deletes an author profile by their ID.

**Path Parameters:**

- `:id` - The ID of the author to delete.

**Response:**

```json
{
  "data": {
    "id": 3,
    "attributes": {
      "name": "John Doe",
      "bio": "Seasoned journalist specializing in investigative reporting.",
      "profile_picture": {
        "data": {
          "id": 6,
          "attributes": {
            "url": "/uploads/john_doe.jpg"
          }
        }
      }
    }
  }
}
```

## Request Structure

All API requests should be sent to the base URL of the Strapi backend, typically `http://localhost:1337`.

### Headers

- **Content-Type:** `application/json`
- **Authorization:** `Bearer your_jwt_token` (required for protected routes)

**Example:**

```
Content-Type: application/json
Authorization: Bearer your_jwt_token
```

### Body

For `POST` and `PUT` requests, the body should be in JSON format, containing a `data` object with the relevant fields.

**Example:**

```json
{
  "data": {
    "field1": "value1",
    "field2": "value2"
  }
}
```

## Response Structure

All API responses are in JSON format and follow a consistent structure.

### Success Response

- **Status Code:** `200 OK` (or other relevant success codes like `201 Created`)
- **Body:** Contains a `data` object with the requested information.

**Example:**

```json
{
  "data": {
    "id": 1,
    "attributes": {
      "field1": "value1",
      "field2": "value2"
    }
  }
}
```

### Error Response

- **Status Code:** Relevant error code (e.g., `400 Bad Request`, `401 Unauthorized`, `404 Not Found`, `500 Internal Server Error`)
- **Body:** Contains an `error` object with details about the issue.

**Example:**

```json
{
  "error": {
    "status": 400,
    "name": "ValidationError",
    "message": "Invalid request payload.",
    "details": {
      "errors": [
        {
          "path": "field1",
          "message": "Field1 is required."
        }
      ]
    }
  }
}
```

## Error Handling

Proper error handling ensures that clients receive meaningful feedback when something goes wrong.

### Common Error Codes

- **400 Bad Request:** The request could not be understood or was missing required parameters.
- **401 Unauthorized:** Authentication failed or user does not have permissions for the desired action.
- **403 Forbidden:** Authentication succeeded but authenticated user does not have access to the requested resource.
- **404 Not Found:** The requested resource does not exist.
- **500 Internal Server Error:** An error occurred on the server.

### Best Practices

- **Consistent Error Structure:** Maintain a consistent error response structure for easier client-side handling.
- **Descriptive Messages:** Provide clear and concise error messages to aid in debugging.
- **Avoid Exposing Sensitive Information:** Do not include stack traces or sensitive server information in error responses.

## Rate Limiting

To protect the API from abuse and ensure fair usage, rate limiting is implemented.

### Limits

- **Unauthenticated Requests:** Limited to 100 requests per hour.
- **Authenticated Requests:** Limited to 1000 requests per hour.

### Headers

API responses include headers that inform clients about their current rate limit status.

- `X-RateLimit-Limit`: The maximum number of requests allowed in the current period.
- `X-RateLimit-Remaining`: The number of requests remaining in the current period.
- `X-RateLimit-Reset`: The time at which the current rate limit period resets in UTC epoch seconds.

**Example Headers:**

```
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 750
X-RateLimit-Reset: 1615125600
```

### Handling Rate Limit Exceeded

When the rate limit is exceeded, the API will respond with:

- **Status Code:** `429 Too Many Requests`
- **Body:**

  ```json
  {
    "error": {
      "status": 429,
      "name": "TooManyRequestsError",
      "message": "You have exceeded the rate limit. Please try again later."
    }
  }
  ```

## Examples

### Using cURL

#### Fetch All Articles

```bash
curl -X GET "http://localhost:1337/api/articles?populate=*" -H "Content-Type: application/json"
```

#### Create a New Article

```bash
curl -X POST "http://localhost:1337/api/articles" \
     -H "Content-Type: application/json" \
     -H "Authorization: Bearer your_jwt_token" \
     -d '{
           "data": {
             "title": "Exploring the Future of AI",
             "content": "Content about the future of AI...",
             "published_at": "2024-05-10T09:00:00.000Z",
             "author": 2,
             "category": 1,
             "featured_image": 7
           }
         }'
```

### Using JavaScript (Fetch API)

#### Fetch Single Article

```javascript
fetch("http://localhost:1337/api/articles/1?populate=*", {
  method: "GET",
  headers: {
    "Content-Type": "application/json",
  },
})
  .then((response) => response.json())
  .then((data) => console.log(data))
  .catch((error) => console.error("Error:", error));
```

#### Update an Article

```javascript
fetch("http://localhost:1337/api/articles/1", {
  method: "PUT",
  headers: {
    "Content-Type": "application/json",
    Authorization: "Bearer your_jwt_token",
  },
  body: JSON.stringify({
    data: {
      title: "Updated Article Title",
      content: "Updated content...",
    },
  }),
})
  .then((response) => response.json())
  .then((data) => console.log(data))
  .catch((error) => console.error("Error:", error));
```

## Best Practices

### Secure Your Endpoints

- **Use HTTPS:** Always serve your API over HTTPS to encrypt data in transit.
- **Validate Inputs:** Ensure all incoming data is validated to prevent injection attacks.
- **Limit Access:** Use roles and permissions to restrict access to sensitive endpoints.

### Optimize Performance

- **Pagination:** Implement pagination for endpoints that return large datasets to reduce load times.
- **Selective Population:** Only populate necessary fields to minimize payload sizes.
- **Caching:** Utilize caching mechanisms where appropriate to reduce server load and improve response times.

### Maintain Documentation

- **Keep It Updated:** Regularly update the API documentation to reflect any changes or new endpoints.
- **Provide Examples:** Include request and response examples to aid developers in understanding how to interact with the API.
- **Use Tools:** Consider using tools like Swagger or Postman to create interactive API documentation.

## Additional Resources

- [Strapi Documentation](https://strapi.io/documentation/developer-docs/latest/getting-started/introduction.html)
- [Next.js API Routes](https://nextjs.org/docs/api-routes/introduction)
- [JSON Web Tokens (JWT)](https://jwt.io/introduction/)
- [HTTP Status Codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
- [Rate Limiting in APIs](https://www.nginx.com/blog/rate-limiting-nginx/)

---

**Project:** [Next News](https://github.com/Aliio-Inc/strapi-next-news)  
**Author:** Atiq Israk  
**Website:** [https://aliio.tech](https://aliio.tech)  
**Contact:** [atiqisrak@gmail.com](mailto:atiqisrak@gmail.com)

---

## Brief Explanation

- **Title and Introduction**: Clearly states that the document is about the API for Next News, outlining its purpose.
- **Table of Contents**: Provides an organized structure for easy navigation through different sections of the API documentation.
- **Authentication**:
  - **Register** and **Login**: Details the endpoints for user registration and authentication, including request and response examples.
  - **JWT Tokens**: Explains how to use JWT tokens for securing API requests.
- **Endpoints**:
  - **Articles, Categories, Authors**: Each resource has its own set of CRUD (Create, Read, Update, Delete) endpoints with detailed descriptions, request structures, and response examples.
- **Request and Response Structure**:
  - **Headers**: Specifies necessary headers for API requests.
  - **Body**: Describes the expected JSON structure for POST and PUT requests.
- **Error Handling**: Outlines common error codes and best practices for handling errors, ensuring developers can effectively debug issues.
- **Rate Limiting**: Describes the rate limits applied to API requests to prevent abuse, including how to handle rate limit exceedances.
- **Examples**:
  - **cURL** and **JavaScript (Fetch API)**: Provides practical examples of how to interact with the API using different tools and languages.
- **Best Practices**:
  - **Security**: Emphasizes securing endpoints, validating inputs, and restricting access.
  - **Performance**: Advises on optimizing API performance through pagination, selective data population, and caching.
  - **Documentation Maintenance**: Encourages keeping the API documentation up-to-date and using tools for interactive documentation.
- **Additional Resources**: Links to relevant external documentation and resources for further learning and reference.
- **Footer**: Includes project information, author details, website link, and contact information for additional support.

---

**Project:** [Next News](https://github.com/Aliio-Inc/strapi-next-news)  
**Author:** Atiq Israk  
**Website:** [https://aliio.tech](https://aliio.tech)  
**Contact:** [atiqisrak@gmail.com](mailto:atiqisrak@gmail.com)

---

Feel free to customize this API documentation to better fit the specific needs of your project. If you have any questions or need further assistance, don't hesitate to [open an issue](https://github.com/Aliio-Inc/strapi-next-news/issues) or reach out to the maintainers.
