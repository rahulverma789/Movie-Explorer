# Movie Recommendation System

A FastAPI-based movie recommendation system with semantic search capabilities.

## Features

- Movie search and recommendations
- Semantic similarity using embeddings
- TMDB integration for movie details
- RESTful API endpoints

## Deployment on Railway

### Prerequisites

1. **Google Drive Setup**: Upload your files to Google Drive and get sharing URLs
2. **GitHub Repository**: Push your code to GitHub
3. **Railway Account**: Sign up at [railway.app](https://railway.app)

### Files Required

- `final_movies_cleaned.feather` - Cleaned movie dataset
- `movie_embeddings_float16.npy` - Movie embeddings
- `fine_tuned_sbert_multi_modal.zip` - Fine-tuned model (optional)

### Step 1: Prepare Google Drive URLs

1. Upload your files to Google Drive
2. Make them publicly accessible
3. Get the sharing URLs and convert them to direct download URLs:
   - Replace `https://drive.google.com/file/d/FILE_ID/view` with `https://drive.google.com/uc?id=FILE_ID`

### Step 2: Deploy to Railway

1. **Connect GitHub Repository**:
   - Go to Railway dashboard
   - Click "New Project"
   - Select "Deploy from GitHub repo"
   - Choose your repository

2. **Set Environment Variables**:
   - In Railway dashboard, go to your project
   - Click on "Variables" tab
   - Add the following environment variables:

```bash
MOVIES_FILE_URL=https://drive.google.com/uc?id=YOUR_MOVIES_FILE_ID
EMBEDDINGS_FILE_URL=https://drive.google.com/uc?id=YOUR_EMBEDDINGS_FILE_ID
MODEL_FILE_URL=https://drive.google.com/uc?id=YOUR_MODEL_FILE_ID
TMDB_API_KEY=your_tmdb_api_key_here
```

3. **Deploy**:
   - Railway will automatically detect the Python app
   - It will install dependencies from `requirements.txt`
   - The app will start using the `Procfile`

### Step 3: Verify Deployment

1. Check Railway logs for successful file downloads
2. Test your API endpoints
3. Monitor resource usage

## Local Development

1. Install dependencies:
```bash
pip install -r requirements.txt
```

2. Set environment variables in `.env` file (copy from `env.example`)

3. Run the application:
```bash
uvicorn main_v2:app --reload
```

## API Endpoints

- `GET /` - Health check
- `GET /search` - Search movies
- `GET /recommendations/{movie_id}` - Get movie recommendations
- `GET /movies/{movie_id}` - Get movie details

## Environment Variables

- `MOVIES_FILE_URL`: Google Drive URL for movies dataset
- `EMBEDDINGS_FILE_URL`: Google Drive URL for embeddings
- `MODEL_FILE_URL`: Google Drive URL for fine-tuned model (optional)
- `TMDB_API_KEY`: TMDB API key for movie data
- `PORT`: Port number (set automatically by Railway)

## Troubleshooting

1. **File Download Issues**: Check Google Drive sharing permissions
2. **Memory Issues**: Railway provides limited memory; consider using smaller file formats
3. **Timeout Issues**: Large files may take time to download; check Railway logs

## Notes

- Files are downloaded on startup to ensure they're available
- The app caches downloaded files locally
- Consider using Railway's persistent storage for production deployments
