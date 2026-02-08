# EyeTouch Next.js App Deployment Guide

## Prerequisites

- Node.js 18+ installed
- Git repository initialized
- MongoDB Atlas account with a cluster created

## Deployment Options

### 1. Vercel Deployment (Recommended)

**Step 1: Install Vercel CLI**
```bash
npm install -g vercel
```

**Step 2: Login to Vercel**
```bash
vercel login
```

**Step 3: Initialize Deployment**
```bash
cd "c:\Users\ADMIN\Desktop\eyetouch-nextjs-full"
vercel
```

**Step 4: Production Deployment**
```bash
vercel --prod
```

**Step 5: Set Environment Variables**
In Vercel dashboard:
1. Go to Settings → Environment Variables
2. Add these variables:

| Key | Value |
|-----|-------|
| MONGODB_URI | mongodb+srv://eyetouch:eyetouch123@cluster0.mongodb.net/?retryWrites=true&w=majority |
| JWT_SECRET | eyetouch_jwt_secret_key_2024 |
| MONGODB_DB | eyetouch |

**Step 6: Redeploy**
After adding variables, redeploy your production build.

### 2. Netlify Deployment

**Step 1: Install Netlify CLI**
```bash
npm install -g netlify-cli
```

**Step 2: Initialize Deployment**
```bash
netlify init
```

**Step 3: Production Deployment**
```bash
netlify deploy --prod
```

**Step 4: Set Environment Variables**
In Netlify dashboard:
1. Go to Site settings → Build & deploy → Environment
2. Add the same variables as Vercel

### 3. Docker Deployment

**Step 1: Build Docker Image**
```bash
docker build -t eyetouch .
```

**Step 2: Run Docker Container**
```bash
docker run -p 3000:3000 -e NODE_ENV=production -e MONGODB_URI="mongodb+srv://eyetouch:eyetouch123@cluster0.mongodb.net/?retryWrites=true&w=majority" -e JWT_SECRET="eyetouch_jwt_secret_key_2024" -e MONGODB_DB="eyetouch" eyetouch
```

### 4. Server Deployment (VPS)

**Step 1: SSH to Server**
```bash
ssh user@your-server-ip
```

**Step 2: Install Node.js**
```bash
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs
```

**Step 3: Deploy Application**
```bash
git clone your-repo.git
cd eyetouch-nextjs-full
npm install
npm run build
npm start
```

**Step 4: PM2 Process Manager**
```bash
npm install -g pm2
pm2 start npm --name "eyetouch" -- start
```

## Verification

After deployment, verify:
1. Admin login page works
2. Student features are accessible
3. Attendance system functions correctly
4. Data is being stored in MongoDB

## Troubleshooting

**Common Issues:**
- **MongoDB Connection Errors**: Check IP whitelist in MongoDB Atlas
- **Environment Variables**: Ensure all variables are correctly set
- **Build Errors**: Check Node.js version compatibility
- **File Uploads**: Verify storage permissions

## Performance Optimization

**For Production:**
- Enable compression
- Set cache headers
- Use CDN for static assets
- Monitor MongoDB performance