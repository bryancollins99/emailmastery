# 🚀 Deployment Guide

This guide covers multiple deployment options for your Email Empire Landing Page.

## 📋 Quick Deployment Options

### Option 1: GitHub Pages (Simplest)
Perfect for static sites, free hosting, and automatic deployment.

#### Setup GitHub Pages:
1. Go to your GitHub repository
2. Click **Settings** → **Pages**
3. Under **Source**, select **Deploy from a branch**
4. Choose **main** branch and **/ (root)** folder
5. Click **Save**

Your site will be available at: `https://yourusername.github.io/email-empire-landing`

#### Custom Domain (Optional):
1. Add a `CNAME` file to your repository root:
   ```
   your-domain.com
   ```
2. In GitHub Pages settings, add your custom domain
3. Enable **Enforce HTTPS**

---

### Option 2: GitHub Actions + Automated Deployment

#### For Netlify Integration:
Create `.github/workflows/deploy-netlify.yml`:

```yaml
name: Deploy to Netlify

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    
    steps:
    - name: Checkout
      uses: actions/checkout@v3
      
    - name: Setup Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18'
        
    - name: Install Netlify CLI
      run: npm install -g netlify-cli
      
    - name: Deploy to Netlify
      run: netlify deploy --prod --dir . --site ${{ secrets.NETLIFY_SITE_ID }}
      env:
        NETLIFY_AUTH_TOKEN: ${{ secrets.NETLIFY_AUTH_TOKEN }}
```

**Required Secrets:**
- `NETLIFY_AUTH_TOKEN`: Get from Netlify dashboard
- `NETLIFY_SITE_ID`: Found in your Netlify site settings

#### For GitHub Pages with Actions:
Create `.github/workflows/deploy-pages.yml`:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
        
      - name: Setup Pages
        uses: actions/configure-pages@v3
        
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v2
        with:
          path: '.'
          
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v2
```

---

### Option 3: Multi-Platform Deployment

Deploy to multiple platforms simultaneously:

`.github/workflows/deploy-multi.yml`:

```yaml
name: Multi-Platform Deploy

on:
  push:
    branches: [ main ]
  workflow_dispatch:

jobs:
  deploy:
    runs-on: ubuntu-latest
    
    steps:
    - name: Checkout
      uses: actions/checkout@v3
      
    - name: Deploy to Netlify
      run: |
        npm install -g netlify-cli
        netlify deploy --prod --dir . --site ${{ secrets.NETLIFY_SITE_ID }}
      env:
        NETLIFY_AUTH_TOKEN: ${{ secrets.NETLIFY_AUTH_TOKEN }}
        
    - name: Deploy to Vercel
      uses: amondnet/vercel-action@v25
      with:
        vercel-token: ${{ secrets.VERCEL_TOKEN }}
        vercel-org-id: ${{ secrets.ORG_ID }}
        vercel-project-id: ${{ secrets.PROJECT_ID }}
        working-directory: ./
```

---

## 🛠️ Pre-Deployment Checklist

### Optimize Your Site:
- [ ] Compress images in `assets/images/`
- [ ] Minify CSS and JavaScript (if needed)
- [ ] Test all links and forms
- [ ] Verify responsive design
- [ ] Check countdown timer functionality

### SEO & Performance:
- [ ] Add meta tags for social sharing
- [ ] Implement analytics (Google Analytics)
- [ ] Add favicon
- [ ] Test page load speed
- [ ] Add robots.txt if needed

---

## 📊 Monitoring & Analytics

### Add Google Analytics:
Add to your `index.html` `<head>` section:

```html
<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=GA_TRACKING_ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'GA_TRACKING_ID');
</script>
```

### Performance Monitoring:
- Use GitHub Actions to run Lighthouse tests
- Set up uptime monitoring (UptimeRobot, Pingdom)
- Monitor conversion rates through your checkout system

---

## 🔧 Advanced Configurations

### Custom Headers (Netlify):
Your existing `netlify.toml` can be enhanced:

```toml
[build]
  publish = "."

[[headers]]
  for = "/*"
  [headers.values]
    X-Frame-Options = "DENY"
    X-XSS-Protection = "1; mode=block"
    X-Content-Type-Options = "nosniff"
    Referrer-Policy = "strict-origin-when-cross-origin"

[[redirects]]
  from = "/old-path"
  to = "/new-path"
  status = 301
```

### Environment-Specific Deployments:
Create separate workflows for staging and production:

```yaml
# For staging
on:
  push:
    branches: [ develop ]

# For production  
on:
  push:
    branches: [ main ]
```

---

## 🚨 Troubleshooting

### Common Issues:

**GitHub Pages not updating:**
- Check Actions tab for deployment status
- Ensure branch and folder settings are correct
- Clear browser cache

**Netlify deployment fails:**
- Verify `netlify.toml` syntax
- Check build logs in Netlify dashboard
- Ensure all secrets are set correctly

**Images not loading:**
- Verify relative paths in HTML
- Check file case sensitivity
- Ensure images are committed to repository

### Debug Commands:
```bash
# Test site locally
python -m http.server 8000
# or
npx serve .

# Check file structure
ls -la assets/images/

# Validate HTML
npx html-validate index.html
```

---

## 📱 Mobile Testing

Before deploying, test on multiple devices:
- iPhone (Safari)
- Android (Chrome)
- iPad (Safari)
- Desktop (Chrome, Firefox, Safari)

Use browser dev tools to simulate different screen sizes.

---

## 🎯 Next Steps

1. Choose your deployment method
2. Set up the required secrets/tokens
3. Create the workflow file
4. Push to trigger deployment
5. Monitor and optimize

**Recommended:** Start with GitHub Pages for simplicity, then upgrade to automated deployments as needed. 