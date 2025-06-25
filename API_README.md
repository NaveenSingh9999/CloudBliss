
# CloudBliss API Documentation

CloudBliss provides a RESTful API for programmatic access to your cloud storage. This API allows you to upload, manage, and retrieve files securely.

## Base URL

```
https://aouqcwbdoyrccjcrhzzi.supabase.co/functions/v1/
```

## Authentication

All API requests require authentication using an API key. Include your API key in the Authorization header:

```
Authorization: Bearer YOUR_API_KEY
```

### Getting an API Key

1. Log in to your CloudBliss account
2. Navigate to Developer API section
3. Click "Generate API Key"
4. Copy and securely store your API key

**Important:** API keys start with `cb_` and should be kept secure. Never expose them in client-side code.

## Rate Limits

- **100 requests per minute** per API key
- Rate limit headers are included in responses:
  - `X-RateLimit-Limit`: Maximum requests per minute
  - `X-RateLimit-Remaining`: Remaining requests in current window
  - `X-RateLimit-Reset`: Time when rate limit window resets

## API Endpoints

### 1. Upload File

Upload a file to CloudBliss storage.

**Endpoint:** `POST /api-file-upload`

**Content-Type:** `multipart/form-data`

**Required Scopes:** `write`

**Parameters:**
- `file` (File): The file to upload

**Example Request:**
```bash
curl -X POST \
  -H "Authorization: Bearer cb_your_api_key_here" \
  -F "file=@document.pdf" \
  https://aouqcwbdoyrccjcrhzzi.supabase.co/functions/v1/api-file-upload
```

**Response (201 Created):**
```json
{
  "success": true,
  "file": {
    "id": "550e8400-e29b-41d4-a716-446655440000",
    "name": "document.pdf",
    "type": "application/pdf",
    "size": 1024000,
    "created_at": "2023-12-01T10:30:00Z",
    "encrypted": true,
    "storage_path": "github_distributed",
    "github_repo": "cryptoKeeper_abc123_0"
  },
  "message": "File uploaded successfully"
}
```

### 2. Get File Metadata

Retrieve metadata for a specific file.

**Endpoint:** `GET /api-file-metadata/{fileId}`

**Required Scopes:** `read`

**Example Request:**
```bash
curl -H "Authorization: Bearer cb_your_api_key_here" \
  https://aouqcwbdoyrccjcrhzzi.supabase.co/functions/v1/api-file-metadata/550e8400-e29b-41d4-a716-446655440000
```

**Response (200 OK):**
```json
{
  "success": true,
  "file": {
    "id": "550e8400-e29b-41d4-a716-446655440000",
    "name": "document.pdf",
    "type": "application/pdf",
    "size": 1024000,
    "created_at": "2023-12-01T10:30:00Z",
    "updated_at": "2023-12-01T10:30:00Z",
    "encrypted": true,
    "shared": false,
    "storage_path": "github_distributed",
    "github_repo": "cryptoKeeper_abc123_0",
    "tags": ["work", "important"]
  }
}
```

### 3. Delete File

Delete a file from CloudBliss storage.

**Endpoint:** `DELETE /api-file-delete/{fileId}`

**Required Scopes:** `delete`

**Example Request:**
```bash
curl -X DELETE \
  -H "Authorization: Bearer cb_your_api_key_here" \
  https://aouqcwbdoyrccjcrhzzi.supabase.co/functions/v1/api-file-delete/550e8400-e29b-41d4-a716-446655440000
```

**Response (200 OK):**
```json
{
  "success": true,
  "message": "File deleted successfully"
}
```

## API Key Scopes

API keys support different permission scopes:

- **`read`**: View file metadata and list files
- **`write`**: Upload new files
- **`delete`**: Delete existing files

When generating an API key, you can specify which scopes it should have. By default, new keys have all scopes.

## Error Handling

The API uses conventional HTTP response codes:

- **200**: Success
- **201**: Created (successful upload)
- **400**: Bad Request (invalid parameters)
- **401**: Unauthorized (invalid or missing API key)
- **403**: Forbidden (insufficient permissions)
- **404**: Not Found (file doesn't exist or access denied)
- **429**: Too Many Requests (rate limit exceeded)
- **500**: Internal Server Error

**Error Response Format:**
```json
{
  "success": false,
  "error": "Error message describing what went wrong"
}
```

## Common Error Examples

### Invalid API Key
```json
{
  "success": false,
  "error": "Invalid API key format"
}
```

### File Not Found
```json
{
  "success": false,
  "error": "File not found or access denied"
}
```

### Rate Limit Exceeded
```json
{
  "success": false,
  "error": "Rate limit exceeded. Please try again later."
}
```

### Insufficient Permissions
```json
{
  "success": false,
  "error": "API key does not have write permissions"
}
```

## SDK Examples

### Node.js/JavaScript

```javascript
const API_KEY = 'cb_your_api_key_here';
const BASE_URL = 'https://aouqcwbdoyrccjcrhzzi.supabase.co/functions/v1';

// Upload a file
async function uploadFile(file) {
  const formData = new FormData();
  formData.append('file', file);
  
  const response = await fetch(`${BASE_URL}/api-file-upload`, {
    method: 'POST',
    headers: {
      'Authorization': `Bearer ${API_KEY}`
    },
    body: formData
  });
  
  return response.json();
}

// Get file metadata
async function getFileMetadata(fileId) {
  const response = await fetch(`${BASE_URL}/api-file-metadata/${fileId}`, {
    headers: {
      'Authorization': `Bearer ${API_KEY}`
    }
  });
  
  return response.json();
}

// Delete a file
async function deleteFile(fileId) {
  const response = await fetch(`${BASE_URL}/api-file-delete/${fileId}`, {
    method: 'DELETE',
    headers: {
      'Authorization': `Bearer ${API_KEY}`
    }
  });
  
  return response.json();
}
```

### Python

```python
import requests

API_KEY = 'cb_your_api_key_here'
BASE_URL = 'https://aouqcwbdoyrccjcrhzzi.supabase.co/functions/v1'

headers = {
    'Authorization': f'Bearer {API_KEY}'
}

# Upload a file
def upload_file(file_path):
    with open(file_path, 'rb') as file:
        files = {'file': file}
        response = requests.post(f'{BASE_URL}/api-file-upload', 
                               headers=headers, files=files)
    return response.json()

# Get file metadata
def get_file_metadata(file_id):
    response = requests.get(f'{BASE_URL}/api-file-metadata/{file_id}', 
                           headers=headers)
    return response.json()

# Delete a file
def delete_file(file_id):
    response = requests.delete(f'{BASE_URL}/api-file-delete/{file_id}', 
                              headers=headers)
    return response.json()
```

### cURL Examples

```bash
# Upload a file
curl -X POST \
  -H "Authorization: Bearer cb_your_api_key_here" \
  -F "file=@/path/to/your/file.pdf" \
  https://aouqcwbdoyrccjcrhzzi.supabase.co/functions/v1/api-file-upload

# Get file metadata
curl -H "Authorization: Bearer cb_your_api_key_here" \
  https://aouqcwbdoyrccjcrhzzi.supabase.co/functions/v1/api-file-metadata/FILE_ID

# Delete a file
curl -X DELETE \
  -H "Authorization: Bearer cb_your_api_key_here" \
  https://aouqcwbdoyrccjcrhzzi.supabase.co/functions/v1/api-file-delete/FILE_ID
```

## Security Best Practices

1. **Keep API keys secure**: Never commit API keys to version control or expose them in client-side code
2. **Use environment variables**: Store API keys in environment variables
3. **Rotate keys regularly**: Generate new API keys periodically and revoke old ones
4. **Use minimal scopes**: Only grant the permissions your application needs
5. **Monitor usage**: Check API request logs regularly for suspicious activity

## Support

- **Documentation**: Visit the Developer API section in your CloudBliss dashboard
- **Rate Limits**: Contact support if you need higher rate limits
- **Issues**: Report API issues through the CloudBliss support channels

## Changelog

### Version 1.0.0
- Initial API release
- File upload, metadata retrieval, and deletion endpoints
- API key authentication with scopes
- Rate limiting implementation
