# Fix GitHub Pages HTTPS Issue

## Problem
- HTTP works: http://techdevops.co.uk ✅
- HTTPS redirects to default page: https://techdevops.co.uk ❌
- SSL certificate is from Sectigo, not GitHub Pages

## Solution Steps

### 1. Remove Custom Domain Temporarily
```bash
# Remove CNAME file temporarily
git rm CNAME
git commit -m "Temporarily remove custom domain"
git push origin main
```

### 2. Wait 10 minutes, then re-add domain
```bash
# Re-create CNAME file
echo "techdevops.co.uk" > CNAME
git add CNAME
git commit -m "Re-add custom domain"
git push origin main
```

### 3. GitHub Repository Settings
Go to: https://github.com/ThopuriSeetaramaiah/ThopuriSeetaramaiah.github.io/settings/pages

Ensure:
- Source: Deploy from a branch → main
- Custom domain: techdevops.co.uk
- Enforce HTTPS: ✅ (enable after domain verification)

### 4. Verify DNS Propagation
```bash
# Check if GitHub recognizes the domain
curl -I https://thopuriseetaramaiah.github.io
```

## Expected Result
GitHub Pages will issue a new SSL certificate and HTTPS will work properly.
