# Railway Deployment Guide

## Quick Steps to Deploy Your Movie Recommendation System

### 1. Prepare Your Files on Google Drive

1. **Upload these files to Google Drive:**
   - `final_movies_cleaned.feather`
   - `movie_embeddings_float16.npy`
   - `fine_tuned_sbert_multi_modal.zip` (if you have it)

2. **Make files publicly accessible:**
   - Right-click each file → "Share" → "Anyone with the link" → "Viewer"

3. **Get direct download URLs:**
   - Copy the sharing link
   - Convert format: `https://drive.google.com/file/d/FILE_ID/view` → `https://drive.google.com/uc?id=FILE_ID`

### 2. Push Code to GitHub

```bash
# Initialize git if not already done
git init
git add .
git commit -m "Initial commit for Railway deployment"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
git push -u origin main
```

### 3. Deploy on Railway

1. **Go to [railway.app](https://railway.app)**
2. **Sign up/Login** with your GitHub account
3. **Create New Project** → "Deploy from GitHub repo"
4. **Select your repository**
5. **Wait for initial build** (this will fail initially due to missing env vars)

### 4. Configure Environment Variables

1. **In Railway dashboard**, go to your project
2. **Click "Variables" tab**
3. **Add these environment variables:**

```bash
MOVIES_FILE_URL=https://drive.google.com/uc?id=YOUR_ACTUAL_FILE_ID
EMBEDDINGS_FILE_URL=https://drive.google.com/uc?id=YOUR_ACTUAL_FILE_ID
MODEL_FILE_URL=https://drive.google.com/uc?id=YOUR_ACTUAL_FILE_ID
TMDB_API_KEY=your_actual_tmdb_api_key
```

4. **Click "Add" for each variable**

### 5. Redeploy

1. **Go to "Deployments" tab**
2. **Click "Deploy"** or wait for auto-deploy
3. **Monitor the logs** for successful file downloads

### 6. Test Your Deployment

1. **Check the health endpoint:** `https://your-app.railway.app/health`
2. **Test your API endpoints**
3. **Monitor Railway dashboard** for any issues

## Common Issues & Solutions

### File Download Fails
- **Check Google Drive permissions** - files must be publicly accessible
- **Verify URL format** - must use `https://drive.google.com/uc?id=FILE_ID`
- **Check file size** - very large files may timeout

### Build Fails
- **Check requirements.txt** - all dependencies must be compatible
- **Verify Python version** - Railway supports Python 3.8+
- **Check Procfile** - must be exactly as shown

### Memory Issues
- **Monitor Railway logs** for memory usage
- **Consider file compression** if files are very large
- **Use Railway's persistent storage** for production

## Cost Considerations

- **Railway free tier**: $5 credit monthly
- **Pay-as-you-use**: Only pay for actual usage
- **File downloads**: Count towards bandwidth usage
- **Storage**: Consider using Railway's persistent storage for large files

## Next Steps After Deployment

1. **Set up custom domain** (optional)
2. **Configure monitoring** and alerts
3. **Set up CI/CD** for automatic deployments
4. **Monitor performance** and optimize as needed

## Support

- **Railway Docs**: [docs.railway.app](https://docs.railway.app)
- **Railway Discord**: [discord.gg/railway](https://discord.gg/railway)
- **GitHub Issues**: For code-specific problems
