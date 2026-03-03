# Railway Deployment Guide

## Quick Deploy to Railway

### Step 1: Prepare Your Repository

✅ Already done! Your repository is now Railway-ready with:
- `Procfile` - Tells Railway how to start the app
- `railway.json` - Railway configuration
- `runtime.txt` - Python version specification
- `requirements.txt` - Python dependencies
- All files at root level (Railway requirement)

### Step 2: Deploy to Railway

1. **Go to Railway**: https://railway.app/
2. **Sign in** with your GitHub account
3. **Click "New Project"**
4. **Select "Deploy from GitHub repo"**
5. **Choose your repository**: 
   - `kp183/intent` OR
   - `kunalghanchi393-cpu/intent`
6. **Click "Deploy Now"**

### Step 3: Configure Environment Variables

In the Railway dashboard, go to your project and add these variables:

**Required:**
```
AGENT_IDENTIFIER=your_agent_identifier_here
SELLER_VKEY=your_seller_vkey_here
PAYMENT_API_KEY=your_payment_api_key_here
```

**Optional (with defaults):**
```
NETWORK=Preprod
PAYMENT_SERVICE_URL=https://masumi-payment-service-production-95fe.up.railway.app/api/v1
OUTREACH_SERVICE_URL=https://intent-driven-cold-outreach-agent-production.up.railway.app/
OUTREACH_TIMEOUT=30
HOST=0.0.0.0
PORT=8081
```

### Step 4: Get Your Public URL

1. Railway will automatically deploy your app
2. Go to **Settings** → **Networking** → **Generate Domain**
3. Your agent will be available at: `https://your-app-name.up.railway.app`

### Step 5: Test Your Deployment

Test these endpoints:
- `https://your-app-name.up.railway.app/availability`
- `https://your-app-name.up.railway.app/input_schema`
- `https://your-app-name.up.railway.app/docs`

### Troubleshooting

**If deployment fails:**

1. Check the logs in Railway dashboard
2. Verify all environment variables are set
3. Ensure `OUTREACH_SERVICE_URL` is accessible
4. Check that Python version matches (3.11)

**Common Issues:**

- **Port binding error**: Railway automatically sets the PORT variable
- **Module not found**: Check requirements.txt includes all dependencies
- **Connection timeout**: Verify OUTREACH_SERVICE_URL is correct

### Automatic Redeployment

Railway automatically redeploys when you push to GitHub:
```bash
git add .
git commit -m "Update agent"
git push origin main
```

### Monitor Your Agent

- **Logs**: Railway Dashboard → Your Project → Logs
- **Metrics**: Railway Dashboard → Your Project → Metrics
- **Health**: Check `/availability` endpoint

## What Railway Will Do

1. ✅ Detect Python project from `requirements.txt`
2. ✅ Install dependencies: `pip install -r requirements.txt`
3. ✅ Run the start command: `python main.py`
4. ✅ Expose your app on a public URL
5. ✅ Auto-restart on failures
6. ✅ Provide logs and monitoring

Your agent is now production-ready! 🚀
