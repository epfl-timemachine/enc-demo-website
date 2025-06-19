# ENC_demo_website

## Local Development

### Requirements
- Python 3.11+
- Flask

### Setup
1. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

2. Configure environment variables (optional):
   ```bash
   cp .env.example .env
   # Edit .env with your specific paths
   ```

3. Run the application:
   ```bash
   python app.py
   ```

4. Access at `http://localhost:5000`

## Docker Deployment

### Quick Start
```bash
# Build the image
docker build -t enc-demo-website .

# Run with included sample data
docker run -p 8080:5000 enc-demo-website
```

Access at `http://localhost:8080`

The container includes sample data by default, so no configuration is needed for basic usage.

### Using Custom Data
To use your own images and JSON results, mount your data directory and optionally set environment variables:

```bash
# Mount external data directory
docker run -p 8080:5000 -v /path/to/your/data:/app/data enc-demo-website

# Or specify custom paths with environment variables
docker run -p 8080:5000 \
  -v /path/to/your/images:/custom/images \
  -v /path/to/your/results:/custom/results \
  -e IMAGE_FOLDER=/custom/images \
  -e JSON_FOLDER_GPT4O=/custom/results/gpt-4o \
  -e JSON_FOLDER_O4MINI=/custom/results/o4-mini \
  enc-demo-website
```

### Environment Variables (Optional)
- `IMAGE_FOLDER`: Path to raw images directory (default: `./data/raw_images`)
- `JSON_FOLDER_GPT4O`: Path to GPT-4o results directory (default: `./data/results/gpt-4o`)
- `JSON_FOLDER_O4MINI`: Path to O4-mini results directory (default: `./data/results/o4-mini`)

## GitHub Container Registry

Images are automatically built and published to `ghcr.io` via GitHub Actions on pushes to main branch.

### Pull and run from registry:
```bash
# Simple usage with included data
docker run -p 8080:5000 ghcr.io/epfl-timemachine/enc-demo-website:main

# With custom data
docker run -p 8080:5000 -v /path/to/your/data:/app/data ghcr.io/epfl-timemachine/enc-demo-website:main

# With custom data mounted to custom paths with environment variables
docker run -p 8080:5000 \
  -v /path/to/your/images:/custom/images \
  -v /path/to/your/results:/custom/results \
  -e IMAGE_FOLDER=/custom/images \
  -e JSON_FOLDER_GPT4O=/custom/results/gpt-4o \
  -e JSON_FOLDER_O4MINI=/custom/results/o4-mini \
  ghcr.io/epfl-timemachine/enc-demo-website:main
```