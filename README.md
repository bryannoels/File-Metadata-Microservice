# File Metadata Analyzer API

## Overview

The File Metadata Analyzer API is a lightweight and efficient service that instantly extracts essential information from uploaded files without storing or processing the actual file content. This tool provides users with quick access to file details like name, type, and size, making it perfect for file validation, organization, and content management workflows.

Whether you're building a file upload system, need to validate file types before processing, or want to display file information to users, this API delivers the metadata you need in seconds.

## Key Benefits

- **Instant File Analysis:** Get file metadata immediately upon upload without waiting for complex processing
- **Privacy-Focused:** Files are analyzed in memory and never stored on the server, ensuring complete data privacy
- **Universal File Support:** Works with any file type - documents, images, videos, archives, and more
- **Lightweight & Fast:** Minimal resource usage with quick response times for optimal user experience
- **Easy Integration:** Simple REST API that works with any programming language or platform
- **Validation Ready:** Perfect for implementing file type and size restrictions in your applications

## Business Use Cases

### For Businesses & Organizations
- **Document Management Systems:** Automatically categorize and organize uploaded files based on type and size
- **Content Management:** Validate file uploads before processing to ensure they meet company standards
- **Storage Optimization:** Monitor file sizes to manage storage costs and implement upload limits
- **Compliance & Security:** Screen file types to prevent unauthorized file formats from entering your systems

### For Developers & Applications
- **File Upload Validation:** Implement client-side file checks before sending files to expensive processing services
- **User Interface Enhancement:** Display file information to users immediately after file selection
- **Batch Processing:** Analyze multiple files quickly to sort and route them to appropriate processing pipelines
- **API Gateway:** Use as a preliminary step before routing files to specialized processing services

### For Content Creators & Educators
- **Media Asset Management:** Quickly identify and organize digital assets by type and size
- **Course Material Organization:** Automatically categorize educational resources and documents
- **Portfolio Management:** Analyze and organize creative files for better project management

## How It Works

1. **Upload Any File:** Submit a file through the API endpoint using standard multipart form data
2. **Instant Analysis:** The system immediately extracts metadata from the file header and properties
3. **Receive Results:** Get back essential file information including original name, MIME type, and size in bytes
4. **Privacy Protection:** Your file is processed in memory only and never stored on our servers

## Why Choose This API?

- **Zero Storage Footprint:** Files are never saved, ensuring complete privacy and minimal server overhead
- **Universal Compatibility:** Works with any file format without requiring specific codecs or libraries
- **Developer-Friendly:** Simple, straightforward API that can be integrated in minutes
- **Production-Ready:** Built with Express.js for reliability and scalability
- **Cost-Effective:** Minimal resource usage means lower hosting costs and faster response times

## Getting Started

Simply send a POST request with your file to the `/api/fileanalyse` endpoint and receive instant metadata. No authentication required, no file size limits, and no complex setup needed.

---

# Technical Documentation

## Software Architecture Overview

The File Metadata Analyzer API is built using a minimalist architecture optimized for speed and privacy:

- **Express.js Framework:** Lightweight web server handling HTTP requests and routing
- **Multer Middleware:** Handles multipart/form-data file uploads with memory storage
- **Memory-Only Processing:** Files are processed entirely in RAM, never touching disk storage
- **CORS Enabled:** Cross-origin resource sharing configured for web browser compatibility
- **Environment Configuration:** Uses dotenv for flexible deployment configuration
- **Stateless Design:** Each request is independent, enabling easy horizontal scaling

### Key Architecture Decisions

- **Memory Storage:** Uses `multer.memoryStorage()` to process files in memory, ensuring privacy and speed
- **No Persistence:** Files are discarded immediately after analysis, minimizing security risks
- **Minimal Dependencies:** Uses only essential packages to reduce attack surface and improve performance

## API Documentation

### 1. Analyze File Metadata

**Endpoint:**  
`POST /api/fileanalyse`

**Request:**
- **Content-Type:** `multipart/form-data`
- **Form Field:** `upfile` (file) - The file to analyze

**Behavior:**
- Accepts any file type and size
- Extracts metadata from file properties
- Processes file in memory without storage
- Returns structured file information

**Response:**
- On success:
  ```json
  {
    "name": "document.pdf",
    "type": "application/pdf",
    "size": 2048576
  }
  ```
- On error (no file uploaded):
  ```json
  { "error": "No file uploaded" }
  ```

**Response Fields:**
- `name` (string): Original filename as uploaded by the user
- `type` (string): MIME type of the file (e.g., "image/jpeg", "text/plain")
- `size` (number): File size in bytes

### 2. Application Root

**Endpoint:**  
`GET /`

**Response:**  
Serves the main HTML interface from `/views/index.html`

### 3. Static Assets

**Endpoint:**  
`GET /public/*`

**Behavior:**  
Serves static files from the `/public` directory

## Environment Configuration

The application uses environment variables for configuration:

- `PORT` (optional): Server port number (defaults to 3000)

## Installation & Setup

1. **Install Dependencies:**
   ```bash
   npm install express cors multer dotenv
   ```

2. **Environment Setup:**
   Create a `.env` file (optional):
   ```
   PORT=3000
   ```

3. **Run the Application:**
   ```bash
   node server.js
   ```

## File Upload Examples

### Using cURL
```bash
curl -X POST -F "upfile=@/path/to/your/file.pdf" http://localhost:3000/api/fileanalyse
```

### Using JavaScript (Browser)
```javascript
const formData = new FormData();
formData.append('upfile', fileInput.files[0]);

fetch('/api/fileanalyse', {
  method: 'POST',
  body: formData
})
.then(response => response.json())
.then(data => console.log(data));
```

### Using Python
```python
import requests

with open('file.pdf', 'rb') as f:
    files = {'upfile': f}
    response = requests.post('http://localhost:3000/api/fileanalyse', files=files)
    print(response.json())
```

## Security Considerations

- **Memory Processing:** Files are processed in memory and never written to disk
- **No File Storage:** Zero persistence means no risk of unauthorized file access
- **Input Validation:** Always check for file presence before processing
- **CORS Configuration:** Configured for cross-origin requests - adjust as needed for production

## Deployment Notes

- **Memory Usage:** Monitor memory consumption for large files or high concurrency
- **File Size Limits:** Consider implementing upload size limits for production use
- **Error Handling:** Add additional error handling for production environments
- **Logging:** Implement proper logging for monitoring and debugging

---

*Last updated: June 2, 2025*