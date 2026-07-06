# Personal Website Developer & Compilation Guide

This repository contains the source files for Dr. Ankur Awadhiya's personal website, generated using a customized version of **Jemdoc with MathJax**.

The website is designed with a premium, responsive glassmorphic aesthetic and utilizes a top horizontal navigation bar. 

---

## 🎨 Theme & Design Guidelines

- **Style:** Glassmorphism (`backdrop-filter: blur(18px)`) with modern translucent cards, subtle borders, and smooth shadows.
- **Background:** Multi-gradient mesh background using radial gradients (supports both light and dark system schemes automatically).
- **Typography:** Uses Google Font `Plus Jakarta Sans` (`300`, `400`, `500`, `600`, `700`) as the primary font family.
- **Layout:** Centered single-column structure (`max-width: 900px`) where both the menu navigation card and the main content card stack vertically.
- **Navigation:** Top horizontal menu bar with flat, lowercase menu links (`home`, `courses`, `writings`). Do not use category grouping headers to keep navigation minimal.
- **Subfigures:** In the `wildfires/` book directory, multi-image subfigures are wrapped in `.sub-image-wrapper` with a `.sub-image-label` tag to display absolute-positioned corner labels (a, b, c...).

---

## 🎓 Credentials Hierarchy Rules

When updating credentials in the **`index.jemdoc`** (Home) file, group them by study areas (e.g., Engineering, Data Science, Remote Sensing, Economics/Management/Law) and arrange items within each category in the following tier order:

1. **Tier 1 (Elite Institutions):** IIT, IIM, Oxford, Cambridge, Harvard, MIT, Johns Hopkins, Duke, and other Ivy League organizations.
2. **Tier 2 (Other Prominent Universities):** Standard universities and higher-education research institutes (ranked by prominence, e.g., University of Florida, Toronto, UC Davis).
3. **Tier 3 (Certifications & Others):** Professional credentials from companies/platforms (e.g., Google) or specific local institutes (e.g., Wildlife Institute of India, IGNFA).
*Note: Do not list years for credentials to keep the layout timeless.*

---

## ⚙️ Compilation & Build Instructions

Always build the website using the local custom configuration to ensure mobile device compatibility (viewport meta tags):

```bash
# Compile all source jemdoc files using the custom configuration
python3 jemdoc_mathjax-master/jemdoc -c mysite.conf *.jemdoc
```

### Configuration Files:
- **`mysite.conf`:** Custom configuration override injecting `<meta name="viewport" content="width=device-width, initial-scale=1.0" />` into the HTML `<head>`.
- **`MENU`:** Contains the flat list of site links. Each line should be structured as `linkname [filename.html]` without category header text lines.

---

## 🚀 Deployment Workflow

The live website is served via GitHub Pages from the **`rebuild-pages`** branch. To deploy updates:

1. **Commit changes to `main` branch:**
   ```bash
   git checkout main
   git add .
   git commit -m "Your commit message"
   git push origin main
   ```
2. **Merge `main` into `rebuild-pages` branch:**
   ```bash
   git checkout rebuild-pages
   # Resolve any minor .DS_Store conflicts by keeping theirs (main) if they arise
   git merge main -m "Merge main branch updates into rebuild-pages"
   ```
3. **Push to deploy:**
   ```bash
   git push origin rebuild-pages
   ```
4. **Verify Build Status:** Check the status of the "pages build and deployment" action on GitHub. If the deployment fails due to a temporary GitHub Pages error, trigger a fresh rebuild by pushing an empty commit on `rebuild-pages`:
   ```bash
   git commit --allow-empty -m "Trigger rebuild to fix failed pages deployment"
   git push origin rebuild-pages
   ```
5. **Clean up:** Switch back to `main` branch to resume local development:
   ```bash
   git checkout main
   ```
