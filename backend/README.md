# Cistra Backend Server

FastAPI backend server for cost-of-living predictions using ML models and Gemini AI.

## Quick Start

### Using Docker (Recommended)

1. **Build the Docker image:**
   ```bash
   docker build -t cistra-backend .
   ```

2. **Run the container:**
   ```bash
   docker run -d \
     --name cistra-api \
     -p 8000:8000 \
     -e GEMINI_API_KEY=your_api_key_here \
     -v $(pwd)/model:/app/model \
     cistra-backend
   ```

3. **Access the API:**
   - API Docs: http://localhost:8000/docs
   - Endpoint: POST http://localhost:8000/ai-chat

### Using Docker Compose

1. **Create `.env` file with your API key:**
   ```bash
   echo "GEMINI_API_KEY=your_api_key_here" > .env
   ```

2. **Run with docker-compose:**
   ```bash
   docker-compose up -d
   ```

### Local Development

1. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

2. **Create `.env` file:**
   ```bash
   echo "GEMINI_API_KEY=your_api_key_here" > .env
   ```

3. **Run the server:**
   ```bash
   uvicorn main:app --reload --port 8000
   ```

## API Usage

### Endpoint: `/ai-chat`

**Request:**
```json
{
  "session_id": "user123",
  "message": "What's the cost of living in Toronto with 2 kids?"
}
```

**Response:**
```json
{
  "session_id": "user123",
  "reply": "Toronto is a moderately expensive city...",
  "city": "Toronto, Canada",
  "kids": 2,
  "housing": null,
  "cars": null,
  "score": 0.6234,
  "monthly_estimate": 4250,
  "range_low": 3612,
  "range_high": 5312
}
```

## Environment Variables

- `GEMINI_API_KEY` (required): Your Google Gemini API key

## Docker Commands

- **View logs:** `docker logs cistra-api`
- **Stop container:** `docker stop cistra-api`
- **Remove container:** `docker rm cistra-api`
- **Restart:** `docker restart cistra-api`

## Health Check

The container includes a health check that verifies the API is responding:
```bash
docker inspect --format='{{.State.Health.Status}}' cistra-api
```
