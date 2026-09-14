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
|------|------|-------------|
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

#### Get File Details

```http
GET /files/{id}
```

**Example:**
```bash
curl -H "Authorization: Bearer TOKEN" \
  "http://localhost:3000/api/v1/files/file123"
```

**Response:**
```json
{
  "id": "file123",
  "name": "document.txt",
  "path": "/home/document.txt",
  "type": "file",
  "size": 2048,
  "mime_type": "text/plain",
  "created": "2025-05-26T10:30:00Z",
  "modified": "2025-05-26T11:00:00Z",
  "owner": "user123",
  "permissions": "rw-r--r--"
}
```

#### Upload File

```http
POST /files/upload
Content-Type: multipart/form-data
```

**Parameters:**
- `file` (file): File to upload
- `path` (string): Destination path
- `overwrite` (boolean): Overwrite existing (default: false)

**Example:**
```bash
curl -X POST \
  -H "Authorization: Bearer TOKEN" \
  -F "file=@document.txt" \
  -F "path=/home" \
  "http://localhost:3000/api/v1/files/upload"
```

**Response:**
```json
{
  "id": "file123",
  "name": "document.txt",
  "path": "/home/document.txt",
  "size": 1024,
  "url": "http://localhost:3000/files/file123"
}
```

#### Delete File

```http
DELETE /files/{id}
```

**Example:**
```bash
curl -X DELETE \
  -H "Authorization: Bearer TOKEN" \
  "http://localhost:3000/api/v1/files/file123"
```

**Response:**
```json
{
  "success": true,
  "message": "File deleted successfully"
}
```

#### Move/Rename File

```http
PUT /files/{id}/move
Content-Type: application/json
```

**Request Body:**
```json
{
  "new_path": "/new/location/filename.txt"
}
```

**Example:**
```bash
curl -X PUT \
  -H "Authorization: Bearer TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"new_path": "/documents/file.txt"}' \
  "http://localhost:3000/api/v1/files/file123/move"
```

#### Create Directory

```http
POST /directories
Content-Type: application/json
```

**Request Body:**
```json
{
  "path": "/path/to/new/directory",
  "name": "directory_name"
}
```

**Example:**
```bash
curl -X POST \
  -H "Authorization: Bearer TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"path": "/home", "name": "projects"}' \
  "http://localhost:3000/api/v1/directories"
```

### Applications

#### List Applications

```http
GET /apps
```

**Example:**
```bash
curl -H "Authorization: Bearer TOKEN" \
  "http://localhost:3000/api/v1/apps"
```

**Response:**
```json
{
  "apps": [
    {
      "id": "app123",
      "name": "Text Editor",
      "icon": "editor.png",
      "category": "productivity",
      "installed": true,
      "version": "1.0.0"
    }
  ]
}
```

#### Launch Application

```http
POST /apps/{id}/launch
Content-Type: application/json
```

**Request Body:**
```json
{
  "args": ["file.txt"],
  "options": {}
}
```

**Example:**
```bash
curl -X POST \
  -H "Authorization: Bearer TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"args": ["document.txt"]}' \
  "http://localhost:3000/api/v1/apps/editor123/launch"
```

**Response:**
```json
{
  "process_id": "proc123",
  "status": "running",
  "started_at": "2025-05-26T12:00:00Z"
}
```

#### Get Application Info

```http
GET /apps/{id}
```

**Example:**
```bash
curl -H "Authorization: Bearer TOKEN" \
  "http://localhost:3000/api/v1/apps/editor123"
```

**Response:**
```json
{
  "id": "editor123",
  "name": "Text Editor",
  "description": "Simple text editor",
  "version": "1.0.0",
  "author": "Puter",
  "installed": true,
  "category": "productivity",
  "icon": "data:image/png;base64,...",
  "permissions": ["files:read", "files:write"]
}
```

### System

#### Get System Information

```http
GET /system/info
```

**Example:**
```bash
curl -H "Authorization: Bearer TOKEN" \
  "http://localhost:3000/api/v1/system/info"
```

**Response:**
```json
{
  "version": "2.5.1",
  "uptime": 86400,
  "memory": {
    "total": 4294967296,
    "used": 2147483648,
    "free": 2147483648
  },
  "cpu": {
    "cores": 4,
    "usage": 25.5
  },
  "disk": {
    "total": 107374182400,
    "used": 53687091200,
    "free": 53687091200
  },
  "hostname": "puter-server"
}
```

#### Get System Health

```http
GET /system/health
```

**Example:**
```bash
curl "http://localhost:3000/api/v1/system/health"
```

**Response:**
```json
{
  "status": "healthy",
  "timestamp": "2025-05-26T12:30:00Z",
  "services": {
    "api": "running",
    "database": "running",
    "cache": "running"
  }
}
```

### User

#### Get Current User

```http
GET /user/profile
```

**Example:**
```bash
curl -H "Authorization: Bearer TOKEN" \
  "http://localhost:3000/api/v1/user/profile"
```

**Response:**
```json
{
  "id": "user123",
  "username": "john_doe",
  "email": "john@example.com",
  "created": "2025-01-01T00:00:00Z",
  "preferences": {
    "theme": "dark",
    "language": "en"
  }
}
```

#### Update User Profile

```http
PUT /user/profile
Content-Type: application/json
```

**Request Body:**
```json
{
  "email": "newemail@example.com",
  "preferences": {
    "theme": "light"
  }
}
```

**Example:**
```bash
curl -X PUT \
  -H "Authorization: Bearer TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"email": "new@example.com"}' \
  "http://localhost:3000/api/v1/user/profile"
```

#### List User Sessions

```http
GET /user/sessions
```

**Example:**
```bash
curl -H "Authorization: Bearer TOKEN" \
  "http://localhost:3000/api/v1/user/sessions"
```

**Response:**
```json
{
  "sessions": [
    {
      "id": "session123",
      "device": "Chrome on Windows",
      "ip": "192.168.1.1",
      "created": "2025-05-26T10:00:00Z",
      "last_activity": "2025-05-26T12:30:00Z",
      "active": true
    }
  ]
}
```

## Rate Limiting

API requests are rate-limited to prevent abuse.

**Limits:**
- 1000 requests per hour per token
- 100 requests per minute per token

**Response Headers:**
```http
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 999
X-RateLimit-Reset: 1653576600
```

**Rate Limit Exceeded:**
```json
{
  "error": {
    "code": "RATE_LIMIT_EXCEEDED",
    "message": "Too many requests",
    "retry_after": 60
  }
}
```

## Webhooks

### Register Webhook

```http
POST /webhooks
Content-Type: application/json
```

**Request Body:**
```json
{
  "url": "https://your-domain.com/webhook",
  "events": ["file.created", "file.deleted"],
  "active": true
}
```

**Example:**
```bash
curl -X POST \
  -H "Authorization: Bearer TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "url": "https://your-domain.com/webhook",
    "events": ["file.created"]
  }' \
  "http://localhost:3000/api/v1/webhooks"
```

### Webhook Events

| Event | Triggered | Payload |
|-------|-----------|---------|
| `file.created` | File is created | File object |
| `file.deleted` | File is deleted | File ID |
| `file.modified` | File is modified | File object |
| `app.launched` | App is launched | App ID, Process ID |
| `app.closed` | App is closed | App ID, Process ID |
| `user.login` | User logs in | User ID, Session ID |
| `user.logout` | User logs out | User ID, Session ID |

### Webhook Payload Example

```json
{
  "event": "file.created",
  "timestamp": "2025-05-26T12:30:00Z",
  "data": {
    "id": "file123",
    "name": "document.txt",
    "path": "/home/document.txt",
    "size": 1024,
    "created": "2025-05-26T12:30:00Z"
  }
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

// Upload file
async function uploadFile(filePath, destinationPath) {
  const FormData = require('form-data');
  const fs = require('fs');
  
  const form = new FormData();
  form.append('file', fs.createReadStream(filePath));
  form.append('path', destinationPath);
  
  const response = await fetch(`${apiUrl}/files/upload`, {
    method: 'POST',
    headers: {
      'Authorization': `Bearer ${token}`
    },
    body: form
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

# Upload file
def upload_file(file_path, destination_path):
    files = {'file': open(file_path, 'rb')}
    data = {'path': destination_path}
    response = requests.post(
        f'{api_url}/files/upload',
        files=files,
        data=data,
        headers=headers
    )
    return response.json()
```

### cURL

```bash
# Set token
TOKEN="YOUR_API_TOKEN"
API_URL="http://localhost:3000/api/v1"

# List files
curl -H "Authorization: Bearer $TOKEN" \
  "$API_URL/files?path=/home"

# Upload file
curl -X POST \
  -H "Authorization: Bearer $TOKEN" \
  -F "file=@myfile.txt" \
  -F "path=/home" \
  "$API_URL/files/upload"

# Get system info
curl -H "Authorization: Bearer $TOKEN" \
  "$API_URL/system/info"
```

## Changelog

### v1.0.0
- Initial API release
- File management endpoints
- Application control
- System information
- User management

---

**API Version:** v1.0.0  
**Last Updated:** 2025-05-26
