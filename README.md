# Kubr-QR

A full-stack QR Code Generator application that allows users to generate QR codes from URLs. The generated QR codes are stored in AWS S3 and can be accessed via public URLs.

## Features

- 🎯 **URL to QR Code Conversion**: Convert any URL into a scannable QR code
- ☁️ **Cloud Storage**: QR codes are automatically uploaded to AWS S3 for persistent storage
- 🌐 **Web Interface**: Modern and responsive Next.js frontend for easy interaction
- ⚡ **Fast API**: High-performance FastAPI backend for QR code generation
- 🔗 **Public URLs**: Each QR code gets a publicly accessible URL for easy sharing

## Tech Stack

### Backend
- **FastAPI** - Modern Python web framework
- **Python QRCode** - QR code generation library
- **boto3** - AWS SDK for S3 integration
- **Pillow** - Image processing

### Frontend
- **Next.js 14** - React framework with App Router
- **React 18** - UI library
- **Axios** - HTTP client for API requests
- **Tailwind CSS** - Utility-first CSS framework

### Infrastructure
- **AWS S3** - Object storage for QR code images

## Project Structure

```
Kubr-QR/
├── api/                      # Backend API
│   ├── main.py              # FastAPI application
│   ├── requirements.txt     # Python dependencies
│   └── test_main.py         # API tests
├── front-end-nextjs/        # Frontend application
│   ├── src/
│   │   └── app/            # Next.js app directory
│   ├── public/             # Static assets
│   └── package.json        # Node dependencies
└── README.md               # This file
```

## Prerequisites

Before you begin, ensure you have the following installed:

- **Python 3.8+** - For running the backend API
- **Node.js 18+** - For running the frontend
- **npm** or **yarn** - Package manager for Node.js
- **AWS Account** - With an S3 bucket created
- **AWS Access Key & Secret Key** - For S3 authentication

## Setup Instructions

### 1. Clone the Repository

```bash
git clone <repository-url>
cd Kubr-QR
```

### 2. Backend Setup (API)

Navigate to the API directory:

```bash
cd api
```

Create a virtual environment:

```bash
python -m venv .venv
```

Activate the virtual environment:

- **macOS/Linux:**
  ```bash
  source .venv/bin/activate
  ```

- **Windows:**
  ```bash
  .venv\Scripts\activate
  ```

Install dependencies:

```bash
pip install -r requirements.txt
```

Create a `.env` file in the `api` directory:

```bash
touch .env
```

Add your AWS credentials to `.env`:

```env
AWS_ACCESS_KEY=your_access_key_here
AWS_SECRET_KEY=your_secret_key_here
```

Update the bucket name in `api/main.py`:

```python
bucket_name = 'your-bucket-name'  # Replace with your S3 bucket name
```

Run the API server:

```bash
uvicorn main:app --reload
```

The API server will be running on `http://localhost:8000`

### 3. Frontend Setup

Open a new terminal and navigate to the frontend directory:

```bash
cd front-end-nextjs
```

Install dependencies:

```bash
npm install
```

Run the development server:

```bash
npm run dev
```

The frontend will be running on `http://localhost:3000`

## AWS S3 Configuration

### Create an S3 Bucket

1. Log in to your AWS Console
2. Navigate to S3 service
3. Create a new bucket with your preferred name
4. Configure bucket permissions to allow public read access for the `qr_codes/` prefix (optional, if you want public URLs)

### Configure CORS (if needed)

If you plan to deploy the frontend separately, you may need to configure CORS on your S3 bucket.

## Usage

1. Open your browser and navigate to `http://localhost:3000`
2. Enter a URL in the input field (e.g., `https://example.com`)
3. Click "Generate QR Code"
4. The generated QR code will appear below the form
5. The QR code image is stored in your S3 bucket at `qr_codes/{url_domain}.png`

## API Documentation

### Generate QR Code

**Endpoint:** `POST /generate-qr/`

**Parameters:**
- `url` (query parameter): The URL to convert to a QR code

**Example Request:**
```bash
curl -X POST "http://localhost:8000/generate-qr/?url=https://example.com"
```

**Example Response:**
```json
{
  "qr_code_url": "https://your-bucket-name.s3.amazonaws.com/qr_codes/example.com.png"
}
```

### Interactive API Docs

Once the API server is running, you can access:
- **Swagger UI**: `http://localhost:8000/docs`
- **ReDoc**: `http://localhost:8000/redoc`

## Development

### Backend Development

The API uses FastAPI's auto-reload feature. Any changes to `main.py` will automatically reload the server.

### Frontend Development

The Next.js app uses hot module replacement. Changes to the frontend code will be reflected immediately in the browser.

## Testing

Run the API tests:

```bash
cd api
pytest test_main.py
```

## Troubleshooting

### Common Issues

1. **CORS Errors**: Ensure the frontend URL is included in the CORS origins list in `api/main.py`
2. **AWS Credentials Error**: Verify your `.env` file has the correct AWS credentials
3. **S3 Upload Failed**: Check that your AWS credentials have permission to upload to the specified bucket
4. **Port Already in Use**: Change the port in `uvicorn` command or `package.json`

## Future Enhancements

- [ ] Custom QR code styling options (colors, sizes)
- [ ] Batch QR code generation
- [ ] QR code analytics and tracking
- [ ] Download QR codes locally
- [ ] User authentication and QR code history
- [ ] Docker containerization
- [ ] CI/CD pipeline setup
