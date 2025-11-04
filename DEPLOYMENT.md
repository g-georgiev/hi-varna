# Hi Varna! - Deployment Guide

Complete guide to deploy your website to GitHub Pages and set up Formspree.

---

## Part 1: Deploy to GitHub Pages

### Step 1: Create GitHub Repository

1. Go to https://github.com and log in
2. Click the **"+"** icon in the top right → **"New repository"**
3. Repository name: `hi-varna` (or any name you prefer)
4. Description: "Hi Varna! - Student Support Services Website"
5. Keep it **Public** (required for free GitHub Pages)
6. **DO NOT** check "Initialize with README" (we already have one)
7. Click **"Create repository"**

### Step 2: Push Your Code to GitHub

**Open your terminal/command prompt and run these commands:**

```bash
# Navigate to the project directory
cd /path/to/hi-varna-site

# Initialize git repository
git init

# Configure git with your details (first time only)
git config user.name "Your Name"
git config user.email "your.email@example.com"

# Add all files
git add .

# Create first commit
git commit -m "Initial commit - Hi Varna website"

# Add your GitHub repository as remote
# REPLACE 'YOUR-USERNAME' with your actual GitHub username
# REPLACE 'hi-varna' if you used a different repo name
git remote add origin https://github.com/YOUR-USERNAME/hi-varna.git

# Rename branch to main (GitHub's default)
git branch -M main

# Push to GitHub
git push -u origin main
```

**Authentication:** When you push, GitHub will ask for credentials:
- Username: Your GitHub username
- Password: Use a **Personal Access Token** (not your password)
  - Create one at: https://github.com/settings/tokens
  - Click "Generate new token (classic)"
  - Give it a name: "Hi Varna Deployment"
  - Select scope: **repo** (check the box)
  - Click "Generate token"
  - Copy the token and use it as your password

### Step 3: Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **"Settings"** tab
3. Scroll down to **"Pages"** in the left sidebar
4. Under "Source":
   - Select branch: **main**
   - Folder: **/ (root)**
5. Click **"Save"**
6. Wait 1-2 minutes for deployment

**Your site will be live at:**
`https://YOUR-USERNAME.github.io/hi-varna/`

---

## Part 2: Set Up Formspree (Contact Form)

### Step 1: Create Formspree Account

1. Go to https://formspree.io
2. Click **"Get Started"** or **"Sign Up"**
3. Sign up with:
   - Email address
   - Or GitHub account (recommended)
4. Verify your email if required

### Step 2: Create a New Form

1. After logging in, click **"+ New Form"**
2. Form name: `Hi Varna Contact Form`
3. Your email: Enter the email where you want to receive submissions
4. Click **"Create Form"**

### Step 3: Get Your Form Endpoint

1. You'll see your form endpoint: `https://formspree.io/f/YOUR_FORM_ID`
2. Copy the entire URL (example: `https://formspree.io/f/mwpezzzz`)

### Step 4: Update Your Website

**Option A: Edit directly on GitHub (easiest)**
1. Go to your repository on GitHub
2. Click on `index.html`
3. Click the pencil icon (Edit)
4. Find this line (around line 650):
   ```html
   <form class="contact-form" action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
   ```
5. Replace `YOUR_FORM_ID` with your actual form ID
6. Scroll down and click **"Commit changes"**
7. Wait 1-2 minutes for GitHub Pages to update

**Option B: Edit locally and push**
1. Open `index.html` in a text editor
2. Find the line with `YOUR_FORM_ID`
3. Replace with your actual form ID
4. Save the file
5. Run these commands:
   ```bash
   cd /path/to/hi-varna-site
   git add index.html
   git commit -m "Add Formspree form ID"
   git push
   ```

### Step 5: Test Your Form

1. Go to your live website
2. Scroll to the contact form
3. Fill it out and submit
4. You should receive an email notification
5. Check your Formspree dashboard to see the submission

### Step 6: Configure Formspree Settings (Optional)

In your Formspree dashboard, you can:
- **Custom thank you page**: Redirect users after submission
- **Email notifications**: Customize the email you receive
- **Spam protection**: Already enabled by default
- **Auto-responder**: Send automatic replies to form submitters
- **Integration**: Connect to Slack, Google Sheets, etc.

---

## Part 3: Custom Domain (Optional)

If you want to use `hivarna.com` instead of `username.github.io/hi-varna`:

### Step 1: Buy a Domain
- Namecheap, Google Domains, Cloudflare, etc.
- Buy `hivarna.com` or `hi-varna.com`

### Step 2: Configure DNS
Add these DNS records at your domain provider:

**A Records** (point to GitHub Pages):
```
@    A    185.199.108.153
@    A    185.199.109.153
@    A    185.199.110.153
@    A    185.199.111.153
```

**CNAME Record** (for www):
```
www  CNAME  YOUR-USERNAME.github.io
```

### Step 3: Add CNAME to Repository
1. In your repo, create a file named `CNAME` (no extension)
2. Content: just one line with your domain
   ```
   hivarna.com
   ```
3. Commit and push

### Step 4: Enable Custom Domain in GitHub
1. Go to Settings → Pages
2. Under "Custom domain", enter: `hivarna.com`
3. Check "Enforce HTTPS" (after DNS propagates)

---

## Part 4: Update Content

### Add Logo Image

1. Create an `images` folder in your repository
2. Upload your logo file (e.g., `logo.png`)
3. Edit `index.html` and find the logo section (around line 172):
   ```html
   <div class="logo">
       <span>Hi Varna</span>
   </div>
   ```
4. Replace with:
   ```html
   <div class="logo">
       <img src="images/logo.png" alt="Hi Varna">
   </div>
   ```

### Update Contact Information

Edit `index.html` and replace:
- Phone: `+359 XXX XXX XXX` → your actual phone
- Email: `info@hivarna.com` → your actual email
- Social media links: Replace all `#` with your actual social URLs

### Update Colors (Optional)

Colors are defined at the top of the CSS (around line 12):
```css
:root {
    --primary-blue: #3B82F6;
    --primary-orange: #F59E0B;
    --dark-blue: #1E3A8A;
    --light-blue: #EFF6FF;
}
```

---

## Troubleshooting

### Site not showing after deployment
- Wait 2-3 minutes after pushing
- Check Settings → Pages for deployment status
- Clear browser cache (Ctrl+F5 / Cmd+Shift+R)

### Form not working
- Verify Formspree form ID is correct
- Check Formspree dashboard for errors
- Test in incognito/private browsing mode

### 404 Error
- Make sure file is named `index.html` (not `hivarna-website.html`)
- Check repository is public
- Verify GitHub Pages is enabled

### Images not loading
- Check image file paths are correct
- Ensure images are pushed to GitHub
- Use relative paths (e.g., `images/logo.png` not `/images/logo.png`)

---

## Maintenance

### Making Updates
1. Edit files locally
2. Test changes by opening `index.html` in browser
3. Commit and push:
   ```bash
   git add .
   git commit -m "Description of changes"
   git push
   ```
4. Wait 1-2 minutes for GitHub Pages to update

### Monitoring Form Submissions
- Check your email for notifications
- Log into Formspree dashboard
- Export submissions as CSV if needed

---

## Next Steps

1. ✅ Deploy to GitHub Pages
2. ✅ Set up Formspree
3. 📸 Add your logo image
4. 📞 Update contact information
5. 🔗 Add social media links
6. 🌐 Consider custom domain
7. 📊 Set up Google Analytics (optional)
8. 🔍 Submit to Google Search Console (optional)

---

## Support

If you run into issues:
- GitHub Pages docs: https://docs.github.com/en/pages
- Formspree docs: https://help.formspree.io
- GitHub community: https://github.com/orgs/community/discussions

Good luck with your launch! 🚀
