# GitHub Pages Setup Guide

This document provides step-by-step instructions for configuring GitHub Pages to deploy your Jekyll site via GitHub Actions.

## Prerequisites

- Repository pushed to GitHub (https://github.com/ProfSantosh/santosh)
- GitHub Actions workflow file in place (`.github/workflows/pages.yml`)

## Configuration Steps

### 1. Enable GitHub Pages

1. Go to your repository on GitHub: `https://github.com/ProfSantosh/santosh`
2. Click **Settings** (top navigation)
3. In the left sidebar, click **Pages**

### 2. Configure Build Source

Under **Build and deployment**:

1. **Source:** Select `GitHub Actions` from the dropdown
   - This tells GitHub Pages to use your workflow file instead of building from a branch
   - The workflow in `.github/workflows/pages.yml` will handle the build and deployment

2. That's it! No need to select a branch or directory when using GitHub Actions.

### 3. Verify Workflow Permissions

Ensure GitHub Actions has the necessary permissions:

1. Go to **Settings** → **Actions** → **General**
2. Scroll to **Workflow permissions**
3. Select: `Read and write permissions`
4. Check: `Allow GitHub Actions to create and approve pull requests`
5. Click **Save**

### 4. Trigger First Deployment

Push any change to the `main` branch:

```bash
git add .
git commit -m "Initial Jekyll site deployment"
git push origin main
```

Or manually trigger the workflow:

1. Go to **Actions** tab
2. Click on **Build and Deploy Jekyll Site to GitHub Pages**
3. Click **Run workflow** → **Run workflow**

### 5. Monitor Deployment

1. Go to the **Actions** tab
2. Watch the workflow run in real-time
3. Verify both `build` and `deploy` jobs complete successfully

### 6. Access Your Site

Once deployed, your site will be available at:

```
https://profsantosh.github.io/santosh
```

The full URL will also be shown in:
- **Settings** → **Pages** (under "Your site is live at...")
- The **Actions** workflow summary (deployment URL)

## Troubleshooting

### Workflow Fails

**Problem:** Python dependencies fail to install
- **Solution:** Check `requirements.txt` is valid and dependencies are available

**Problem:** CV extraction fails
- **Solution:** Ensure `_source/html/CV.html` exists and is a valid HTML file
- **Solution:** Ensure `scripts/base_cv.json` is valid JSON
- **Solution:** Run `python scripts/extract_cv.py` locally and check console output

**Problem:** Jekyll build fails
- **Solution:** Run `bundle exec jekyll build` locally to identify issues

### Site Not Updating

**Problem:** Changes pushed but site doesn't update
- **Solution:** Check the Actions tab for failed workflows
- **Solution:** Verify the correct branch is being built (should be `main`)

### 404 Errors

**Problem:** Site returns 404
- **Solution:** Ensure GitHub Pages source is set to "GitHub Actions"
- **Solution:** Verify the baseurl in `_config.yml` matches your repository name
- **Solution:** Wait 1-2 minutes after deployment for DNS propagation

### CSS/Assets Not Loading

**Problem:** Styles or images missing
- **Solution:** Check file paths use `relative_url` filter in templates
- **Solution:** Verify assets are in the `assets/` directory
- **Solution:** Clear browser cache

## Custom Domain (Optional)

To use a custom domain:

1. Go to **Settings** → **Pages**
2. Under **Custom domain**, enter your domain (e.g., `santosh.dev`)
3. Click **Save**
4. Configure DNS with your domain provider:
   - Add a CNAME record pointing to `profsantosh.github.io`
   - Or add A records pointing to GitHub's IPs (see GitHub docs)

## Support

For issues:
- Check GitHub Pages documentation: https://docs.github.com/pages
- Check Jekyll documentation: https://jekyllrb.com/docs/
- Review workflow logs in the Actions tab

## Success Checklist

- [ ] Repository settings → Pages → Source set to "GitHub Actions"
- [ ] Workflow permissions set to "Read and write"
- [ ] First workflow run completed successfully
- [ ] Site accessible at https://profsantosh.github.io/santosh
- [ ] All pages load correctly (Home, About, Experience, etc.)
- [ ] Social links work correctly
- [ ] CV source files present (`_source/html/CV.html` and `scripts/base_cv.json`)
- [ ] CV data displays properly (`_data/cv.json` generated correctly)
- [ ] Mobile responsive design works
