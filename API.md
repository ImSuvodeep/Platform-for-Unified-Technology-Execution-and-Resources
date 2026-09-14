# API Documentation

Complete API reference for Puter platform.

## Table of Contents

- [Overview](#overview)
- [Base URL](#base-url)
- [Authentication](#authentication)
- [Error Handling](#error-handling)
- [Endpoints](#endpoints)
  - [File Management](#file-management)
  - [Applications](#applications)
  - [System](#system)
  - [User](#user)
- [Rate Limiting](#rate-limiting)
- [Webhooks](#webhooks)

## Overview

Puter provides a RESTful API for accessing platform functionality programmatically. This API allows you to:
- Manage files and directories
- Control applications
- Access system information
- Manage user accounts
- Configure settings

## Base URL

```
http://localhost:3000/api/v1
```

For production:
```
https://your-domain.com/api/v1
```

## Authentication

### Token-Based Authentication

Include your API token in the request header:

```http
Authorization: Bearer YOUR_API_TOKEN
```

### Getting a Token

```bash
curl -X POST http://localhost:3000/api/v1/auth/token \
  -H "Content-Type: application/json" \
  -d '{
    "username": "user@example.com",
    "password": "password"
  }'
```

Response:
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "expires_in": 3600
}
```

## Error Handling

All errors follow a consistent format:

```json
{
  "error": {
    "code": "ERROR_CODE",
    "message": "Human-readable error message",
    "details": {
      "field": "value"
    }
  }
}
```

### Common Error Codes

| Code | HTTP | Description |
|------|------|----------|
| `UNAUTHORIZED` | 401 | Authentication failed |
| `FORBIDDEN` | 403 | Permission denied |
| `NOT_FOUND` | 404 | Resource not found |
| `INVALID_REQUEST` | 400 | Invalid request parameters |
| `INTERNAL_ERROR` | 500 | Server error |

## Endpoints

### File Management

#### List Files

```http
GET /files?path=/path/to/directory
```

**Parameters:**
- `path` (string): Directory path
- `limit` (number): Results per page (default: 50)
- `offset` (number): Pagination offset (default: 0)

**Example:**
```bash
curl -H "Authorization: Bearer TOKEN" \
  "http://localhost:3000/api/v1/files?path=/home&limit=10"
```

**Response:**
```json
{
  "files": [
    {
      "name": "document.txt",
      "path": "/home/document.txt",
      "type": "file",
      "size": 1024,
      "created": "2025-05-26T10:30:00Z",
      "modified": "2025-05-26T11:00:00Z",
      "permissions": "rw-r--r--"
    }
  ],
  "total": 25,
  "offset": 0,
  "limit": 10
}
```

## Code Examples

### JavaScript/Node.js

```javascript
const fetch = require('node-fetch');
const apiUrl = 'http://localhost:3000/api/v1';
const token = 'YOUR_API_TOKEN';

// List files
async function listFiles(path) {
  const response = await fetch(`${apiUrl}/files?path=${path}`, {
    headers: {
      'Authorization': `Bearer ${token}`
    }
  });
  return response.json();
}
```

### Python

```python
import requests
api_url = 'http://localhost:3000/api/v1'
token = 'YOUR_API_TOKEN'
headers = {'Authorization': f'Bearer {token}'}

# List files
def list_files(path):
    response = requests.get(
        f'{api_url}/files',
        params={'path': path},
        headers=headers
    )
    return response.json()
```

---

**API Version:** v1.0.0  
**Last Updated:** 2025-05-26