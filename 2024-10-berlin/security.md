
# API Security Matrix

This matrix outlines the security requirements for each endpoint in the List Navigation API. OAuth 2.0 and JWT (JSON Web Token) are used to secure the API. 

- **OAuth**: Provides an authorization framework.
- **JWT**: Used for securely transmitting information between the client and the server.

## Security Scheme Definitions

- **OAuth2**:
  - **Type**: `oauth2`
  - **Flow**: `authorizationCode`
  - **Authorization URL**: `/auth/oauth2/authorize`
  - **Token URL**: `/auth/oauth2/token`
  - **Scopes**:
    - `list:read`: Read access to list navigation
    - `list:write`: Write access to list navigation

- **JWT**:
  - **Type**: `http`
  - **Scheme**: `bearer`
  - **Bearer format**: `JWT`
  - **Description**: JWT token is required to access secured endpoints.

## Security Matrix

| Endpoint        | HTTP Method | Requires OAuth2 | Requires JWT | Scopes          |
|-----------------|-------------|-----------------|--------------|-----------------|
| `/list`         | GET         | Yes             | Yes          | `list:read`     |
| `/list`         | POST        | Yes             | Yes          | `list:write`    |
| `/list/filter`  | GET         | Yes             | Yes          | `list:read`    |
| `/list/{id}`    | GET         | Yes             | Yes          | `list:read`     |
| `/list/{id}`    | PUT         | Yes             | Yes          | `list:write`    |
| `/list/{id}`    | DELETE      | Yes             | Yes          | `list:write`    |
| `/home`         | GET         | No              | No           | N/A             |
| `/exit`         | GET         | No              | No           | N/A             |

<!--
| `/list/first`   | GET         | Yes             | Yes          | `list:read`     |
| `/list/last`    | GET         | Yes             | Yes          | `list:read`     |
| `/list/next`    | GET         | Yes             | Yes          | `list:read`     |
| `/list/previous`| GET         | Yes             | Yes          | `list:read`     |
-->

## Security Settings for OpenAPI Specification

### 1. OAuth2 Security Scheme

```yaml
components:
  securitySchemes:
    OAuth2:
      type: oauth2
      flows:
        authorizationCode:
          authorizationUrl: /auth/oauth2/authorize
          tokenUrl: /auth/oauth2/token
          scopes:
            list:read: Read access to list navigation
            list:write: Write access to list navigation
```

### 2. JWT Security Scheme

```yaml
components:
  securitySchemes:
    JWT:
      type: http
      scheme: bearer
      bearerFormat: JWT
```

## Applying Security to Endpoints

### Secure Endpoints

- **`/list`**: OAuth2 and JWT with `list:read` scope
- **`/list/first`**: OAuth2 and JWT with `list:read` scope
- **`/list/last`**: OAuth2 and JWT with `list:read` scope
- **`/list/next`**: OAuth2 and JWT with `list:read` scope
- **`/list/previous`**: OAuth2 and JWT with `list:read` scope
- **`/list/select`**: OAuth2 and JWT with `list:write` scope

```yaml
paths:
  /list:
    get:
      summary: "Navigate to the list"
      security:
        - OAuth2:
            - list:read
        - JWT: []
  /list/first:
    get:
      summary: "Navigate to the first item in the list"
      security:
        - OAuth2:
            - list:read
        - JWT: []
  /list/last:
    get:
      summary: "Navigate to the last item in the list"
      security:
        - OAuth2:
            - list:read
        - JWT: []
  /list/next:
    get:
      summary: "Navigate to the next item in the list"
      security:
        - OAuth2:
            - list:read
        - JWT: []
  /list/previous:
    get:
      summary: "Navigate to the previous item in the list"
      security:
        - OAuth2:
            - list:read
        - JWT: []
  /list/select:
    get:
      summary: "Select an item in the list"
      security:
        - OAuth2:
            - list:write
        - JWT: []
```

### Unsecured Endpoints

- **`/home`**: No security
- **`/exit`**: No security

```yaml
paths:
  /home:
    get:
      summary: "Navigate to the home page"
      security: []
  /exit:
    get:
      summary: "Exit the list"
      security: []
```

---

This security matrix ensures that sensitive navigation operations (like navigating the list and selecting items) are protected using OAuth2 and JWT. In contrast, non-sensitive operations like navigating to the home page or exiting the list are left unsecured for easier access.
