# Custom Domain Setup Guide for GitHub Pages - wafihassan.ca

## Step 1: CNAME File Updated ✅
The CNAME file has been updated with your domain: `wafihassan.ca`

## Step 2: Commit and Push CNAME File
The CNAME file will be committed and pushed to GitHub.

## Step 3: Configure GitHub Pages Settings
1. Go to your repository: https://github.com/Wafinator/Wafinator.github.io
2. Click **Settings** → **Pages** (in the left sidebar)
3. Under **Custom domain**, enter: `wafihassan.ca`
4. Click **Save**
5. **Don't check "Enforce HTTPS" yet** - wait until DNS is configured (Step 4)

## Step 4: Configure DNS in Porkbun

### How to Access DNS Settings in Porkbun:
1. Log in to your Porkbun account: https://porkbun.com
2. Go to **Account** → **Domain List** (or click on your domain)
3. Click on **wafihassan.ca** to manage it
4. Click on the **DNS** tab

### DNS Configuration for wafihassan.ca:

#### Option A: Apex Domain Only (wafihassan.ca)
Add **4 A records** with these values:

**Record 1:**
- **Type:** A
- **Host:** `@` (or leave blank/empty)
- **Answer:** `185.199.108.153`
- **TTL:** 3600 (or default)

**Record 2:**
- **Type:** A
- **Host:** `@` (or leave blank/empty)
- **Answer:** `185.199.109.153`
- **TTL:** 3600 (or default)

**Record 3:**
- **Type:** A
- **Host:** `@` (or leave blank/empty)
- **Answer:** `185.199.110.153`
- **TTL:** 3600 (or default)

**Record 4:**
- **Type:** A
- **Host:** `@` (or leave blank/empty)
- **Answer:** `185.199.111.153`
- **TTL:** 3600 (or default)

#### Option B: Both Apex and www (Recommended)
1. Add the 4 A records above for `wafihassan.ca`
2. Add **1 CNAME record** for www:
   - **Type:** CNAME
   - **Host:** `www`
   - **Answer:** `wafinator.github.io`
   - **TTL:** 3600 (or default)

**Note:** In Porkbun, if the Host field shows `@`, that means the apex domain. Some interfaces might require you to leave it blank or enter just `@`.

## Step 5: Verify DNS Configuration
After adding the DNS records:
1. Wait 5-10 minutes for initial propagation
2. Check DNS propagation at: https://www.whatsmydns.net/#A/wafihassan.ca
3. You can also test locally: `ping wafihassan.ca` (should resolve to one of the GitHub IPs)

## Step 6: Enable HTTPS in GitHub
1. Go back to GitHub repository → **Settings** → **Pages**
2. Wait until you see a green checkmark next to your custom domain
3. Check the **Enforce HTTPS** checkbox
4. GitHub will automatically provision an SSL certificate (may take a few minutes to hours)

## Step 7: Wait for Full Propagation
- DNS changes typically take 24-48 hours to fully propagate worldwide
- Your site should be accessible within a few hours, but full propagation takes longer
- You can check status at: https://www.whatsmydns.net/#A/wafihassan.ca

## Verification
Once setup is complete, your site will be accessible at:
- `https://wafihassan.ca` ✅
- `https://www.wafihassan.ca` (if you configured www subdomain)

## Troubleshooting

### If site doesn't load:
- Check DNS propagation: https://www.whatsmydns.net/#A/wafihassan.ca
- Verify DNS records are correct in Porkbun
- Make sure CNAME file is committed to GitHub repository

### If HTTPS doesn't work:
- Wait 24 hours after DNS setup
- Make sure DNS is fully propagated
- Check GitHub Pages settings - the domain should show a green checkmark

### If you see GitHub's 404 page:
- Verify CNAME file is in the root directory of your repository
- Make sure CNAME file contains exactly: `wafihassan.ca` (no www, no http://, no trailing slash)

## Porkbun-Specific Notes
- Porkbun's DNS interface is straightforward - look for "DNS" or "DNS Records" tab
- If you see existing records (like A records pointing to Porkbun's IPs), you can delete or modify them
- The `@` symbol in Porkbun typically means the root domain (apex domain)
