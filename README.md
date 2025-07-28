# 📧 Email Empire Landing Page

A high-converting sales page for the Email Empire Blueprint course - designed to help creators build profitable newsletter operations.

## 🚀 Quick Start

### Option 1: GitHub Pages (Recommended)
1. **Enable GitHub Pages:**
   - Go to your repository **Settings** → **Pages**
   - Under **Source**, select **Deploy from a branch**
   - Choose **main** branch and **/ (root)** folder
   - Click **Save**

2. **Automatic Deployment:**
   - The included GitHub Action (`.github/workflows/deploy.yml`) will automatically deploy your site
   - Every push to `main` branch triggers a new deployment
   - Your site will be available at: `https://yourusername.github.io/email-empire-landing`

### Option 2: Local Development
```bash
# Clone the repository
git clone https://github.com/yourusername/email-empire-landing.git
cd email-empire-landing

# Serve locally
python -m http.server 8000
# or
npx serve .

# Open http://localhost:8000
```

## 📁 Project Structure
```
email-empire-landing/
├── index.html              # Main landing page
├── assets/
│   └── images/             # Images and media files
├── netlify.toml            # Netlify configuration
├── .github/
│   └── workflows/
│       └── deploy.yml      # GitHub Actions deployment
├── DEPLOYMENT.md           # Comprehensive deployment guide
└── README.md              # This file
```

## ✨ Features

- **📱 Fully Responsive** - Looks great on all devices
- **⏰ Countdown Timer** - Creates urgency with deadline
- **🧮 Revenue Calculator** - Interactive tool showing earning potential
- **🎯 Exit Intent Popup** - Captures leaving visitors
- **📊 Analytics Ready** - Google Analytics integration
- **🔧 High Performance** - Optimized for speed and conversions

## 🛠️ Customization

### Update Countdown Timer
Edit the countdown date in `index.html`:
```javascript
const countDownDate = DateTime.fromObject({
    year: 2025,
    month: 7,    // July
    day: 31,     // 31st
    hour: 23,
    minute: 59,
    second: 59
}, { zone: 'America/New_York' });
```

### Change Purchase Links
Update all checkout URLs:
```html
<!-- Find and replace this URL throughout index.html -->
https://checkout.teachable.com/secure/37332/checkout/order_pz65ndkp
```

### Modify Calculator Settings
Adjust revenue projections in the calculator section:
```javascript
// Update ARPU (Average Revenue Per User) data
const arpuData = {
    writers: { sponsorships: 1.5, paid: 5, digital: 3, services: 8, hybrid: 4 },
    // ... other niches
};
```

## 📊 Analytics Setup

1. **Google Analytics:**
   - Get your GA4 tracking ID
   - Replace `GA_TRACKING_ID` in the analytics code
   - Uncomment the Google Analytics section in `index.html`

2. **Facebook Pixel** (optional):
   - Add your Facebook Pixel ID
   - Enable conversion tracking

## 🔧 Advanced Features

### A/B Testing
- Test different headlines, prices, or CTAs
- Use Google Optimize or similar tools
- Monitor conversion rates

### Performance Optimization
- Images are already optimized
- CSS and JS are minified inline
- Page loads in under 2 seconds

## 📈 Deployment Options

For detailed deployment instructions, see [DEPLOYMENT.md](DEPLOYMENT.md)

**Quick Options:**
- ✅ **GitHub Pages** (Free, automatic)
- ✅ **Netlify** (Free tier, custom domains)
- ✅ **Vercel** (Free tier, great performance)
- ✅ **Custom hosting** (Full control)

## 🚨 Pre-Launch Checklist

- [ ] Update all purchase links to your payment processor
- [ ] Set correct countdown deadline
- [ ] Test on mobile devices
- [ ] Verify calculator accuracy
- [ ] Add your analytics tracking
- [ ] Test exit intent popup
- [ ] Check all images load correctly
- [ ] Proofread all copy

## 🤝 Support

Need help with deployment or customization? 

- 📖 Check [DEPLOYMENT.md](DEPLOYMENT.md) for detailed guides
- 🐛 Open an issue for bugs or questions
- 💬 Contact support for advanced customization

## 📄 License

This landing page template is designed for the Email Empire Blueprint course. Customize freely for your own products and services.

---

**Ready to deploy?** Follow the GitHub Pages instructions above or check [DEPLOYMENT.md](DEPLOYMENT.md) for advanced options! 🚀 