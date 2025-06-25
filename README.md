# **Cloudbliss – The Next Evolution of Cloud Storage**  
**An ultra-secure, unlimited cloud storage service by Inflate.**  

https://cloudbliss.inflate.live

## 🌍 **What is Cloudbliss?**  
Cloudbliss is a **cutting-edge cloud storage service** designed to provide **unlimited, high-speed, and encrypted storage** while ensuring absolute security and privacy. Powered by Inflate’s ecosystem, Cloudbliss offers **multi-layered encryption, intelligent file management, and advanced storage features**, making it the most secure and efficient cloud platform available.  

---

## 🔒 **Unmatched Security & Encryption**  
Cloudbliss is built on an **end-to-end encrypted storage model**, ensuring that your files are always protected.  

- **C2C Encryption** – A custom-built, next-generation encryption model, **impossible to break**, combining **AES-256 + GCM** without conventional data splitting.  
- **Multi-Level Encryption** – Files are encrypted at multiple layers, ensuring data remains **fully protected at rest and in transit**.  
- **Zero-Knowledge Privacy** – Only **you** have access to your files. No third parties, not even Cloudbliss, can decrypt your data.  

---

## ⚡ **Next-Gen File Management & Speed**  
- **RES54 Parallel Technology** – High-speed, multi-threaded file uploads & downloads without performance drops.  
- **Unlimited Storage** – No space restrictions, **store as much as you want**.  
- **Smart File Indexing** – Automatic organization of files for **instant searching & retrieval**.  
- **Real-Time Sync** – All files are **instantly available** across devices.  

---

## 🔥 **Advanced & Unique Features**  
- **Full File Preview & Editing** – View and edit PDFs, images, and documents directly in Cloudbliss.  
- **Integrated Book Reader** – A seamless reading experience for eBooks and documents.  
- **Theming & UI Customization** – Dark mode & theme toggles for a **personalized experience**.  
- **File Sharing & Collaboration** – Securely share files with others **without compromising privacy**.  
- **Direct Integration with InflateStorage** – Upload and manage files directly from Inflate’s ecosystem.  
- **Multi-Device & Multi-Account Support** – Seamlessly switch between accounts and devices.  
- **Mobile & Desktop Optimization** – Works across all devices with a **clean, fast, and Apple-inspired UI**.  

---

## 🛠 **How Cloudbliss Works?**  

### 1️⃣ **Uploading Files**  
When a user uploads a file, Cloudbliss performs the following steps:  
1. **Pre-processing** – The file metadata (name, size, type) is extracted and stored.  
2. **Encryption & Chunking**  
   - If the file is **≤512MB**, it is split into **10 encrypted parts**.  
   - If the file is **>512MB**, **RES54 intelligently splits** it based on **2^n exponent rules** for optimized storage and retrieval.  
3. **Parallel Uploading with RES54**  
   - Chunks are uploaded **simultaneously** across multiple storage nodes using **parallel transfer**.  
   - Each chunk is **stored separately** and mapped with a unique identifier.  
4. **Metadata Storage**  
   - The system **stores metadata** (file name, encryption keys, chunk locations) in the database for **quick access**.  

---

### 2️⃣ **Downloading & Retrieving Files**  
When a user **downloads a file**, Cloudbliss ensures ultra-fast and secure retrieval:  
1. **Request & Authentication**  
   - User sends a **download request** for a file.  
   - Cloudbliss verifies **ownership and access permissions**.  
2. **Parallel Chunk Retrieval**  
   - Cloudbliss **fetches all encrypted chunks simultaneously** from distributed storage nodes.  
   - RES54 ensures **no bottlenecks**, retrieving chunks in the most **efficient order**.  
3. **Reassembly & Decryption**  
   - Chunks are **merged back** into a single file.  
   - The encrypted chunks are **decrypted using the original encryption key** (only available to the user).  
4. **Final Delivery**  
   - The **original file is reconstructed** and provided to the user **instantly**.  

---

### 3️⃣ **File Metadata Retrieval & Searching**  
Cloudbliss enables **instant file searches and metadata retrieval**:  
1. **Indexed Metadata** – Every file’s metadata (size, name, format) is stored in a **highly optimized index**.  
2. **Optimized Query System** – Users can search files **instantly** using keywords, filters, or date ranges.  
3. **Smart Previews** – Before downloading, Cloudbliss generates **thumbnails & previews** for supported file types.  

---

## 📦 **How Cloudbliss Stores Your Files?**  
Cloudbliss **does not rely on centralized storage solutions**. Instead, it **utilizes ultra-secure storage buckets** with intelligent data distribution, ensuring **speed, scalability, and maximum redundancy**.  

---

## 🚀 **Why Cloudbliss?**  
Cloudbliss is **not just another cloud storage service**. It is a **revolution**—offering the **most advanced encryption, speed, and unlimited storage capabilities** in the world. With privacy-first architecture and an unparalleled feature set, **Cloudbliss redefines the way you store and access data**.


---


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

### Version 2.0.0
- Initial API release
- File upload, metadata retrieval, and deletion endpoints
- API key authentication with scopes
- Rate limiting implementation
