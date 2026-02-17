# Hugo + Decap CMS + Netlify: Setup Guide

## What you'll get
- A fast static blog hosted for free on Netlify
- A web-based admin panel at `yoursite.netlify.app/admin/` where the blogger can write posts with a rich text editor (like WordPress)
- The blogger never touches code or Git — they just log in and write

---

## Step 1: Push to GitHub

Create a new repository on GitHub (e.g., `my-blog`), then push this project:

```bash
cd my-blog
git branch -m master main
git add -A
git commit -m "Initial commit: Hugo + Decap CMS"
git remote add origin https://github.com/YOUR_USERNAME/my-blog.git
git push -u origin main
```

---

## Step 2: Connect Netlify

1. Go to [app.netlify.com](https://app.netlify.com) and sign up with your GitHub account (free)
2. Click **"Add new site"** → **"Import an existing project"**
3. Select **GitHub** and choose your `my-blog` repository
4. Netlify will auto-detect the settings from `netlify.toml`, but verify:
   - **Build command:** `hugo`
   - **Publish directory:** `public`
5. Click **"Deploy site"**
6. Wait ~1 minute for the first build. Your site is now live at `https://random-name.netlify.app`

### (Optional) Rename your site
- Go to **Site settings** → **Site name** → Change to something memorable like `myblog.netlify.app`

### (Optional) Custom domain
- Go to **Domain management** → **Add custom domain** and follow the DNS instructions

---

## Step 3: Enable Netlify Identity (authentication)

This is what lets the blogger log in to the admin panel.

1. In Netlify dashboard, go to **Integrations** → **Netlify Identity** → **Enable**
2. Under **Registration**, set to **Invite only** (so random people can't create accounts)
3. Under **External providers**, you can optionally enable **Google** login for convenience
4. Go to **Services** → **Git Gateway** → **Enable Git Gateway**
   - This allows Decap CMS to commit to your GitHub repo on behalf of the logged-in user

---

## Step 4: Invite the blogger

1. In Netlify dashboard, go to **Identity** tab
2. Click **"Invite users"**
3. Enter the blogger's email address
4. They'll receive an email with a confirmation link
5. After confirming, they can log in at `yoursite.netlify.app/admin/`

---

## Step 5: The blogger's workflow

Share these instructions with the blogger:

### Writing a new post
1. Go to `https://yoursite.netlify.app/admin/`
2. Log in with your email (or Google if enabled)
3. Click **"Blog Posts"** in the sidebar
4. Click **"New Blog Posts"**
5. Fill in the title, date, description, tags
6. Write your post in the rich text editor (supports bold, italic, headings, images, links)
7. Set "Draft" to OFF when ready to publish
8. Click **"Publish"** → **"Publish now"**
9. Wait ~1 minute for the site to rebuild — your post is live!

### Uploading images
- In the editor, click the **"+"** button or drag & drop images
- Images are stored in the `uploads/` folder automatically

### Saving drafts
- The editorial workflow is enabled, so you can save posts as drafts
- Click **"Save"** without publishing to keep it as a draft
- Come back later to edit and publish

---

## Project structure

```
my-blog/
├── archetypes/          # Default front matter templates
├── content/
│   ├── _index.md        # Homepage
│   └── posts/           # Blog posts (managed by Decap CMS)
├── layouts/
│   └── partials/        # Custom template overrides
│       ├── head-additions.html          # Injects Netlify Identity widget
│       └── netlify-identity-redirect.html
├── static/
│   ├── admin/
│   │   ├── index.html   # Decap CMS admin page
│   │   └── config.yml   # CMS configuration (collections, fields)
│   └── uploads/         # Media uploads from the CMS
├── themes/
│   └── ananke/          # Hugo theme (git submodule)
├── hugo.toml            # Hugo site configuration
├── netlify.toml         # Netlify build configuration
└── .gitignore
```

---

## Customization

### Change the theme
The current theme is [Ananke](https://github.com/theNewDynamic/gohugo-theme-ananke). To use a different theme:
1. Remove the ananke submodule: `git submodule deinit themes/ananke && git rm themes/ananke`
2. Add a new theme: `git submodule add https://github.com/THEME_REPO.git themes/THEME_NAME`
3. Update `hugo.toml`: change `theme = "ananke"` to your new theme
4. Check if the new theme uses `head-additions.html` partial — if not, you may need to adjust the Netlify Identity injection

### Add more CMS fields
Edit `static/admin/config.yml` to add new fields to posts. See [Decap CMS widgets docs](https://decapcms.org/docs/widgets/) for available field types.

### Add pages (not just posts)
Add another collection in `static/admin/config.yml`:

```yaml
  - name: "pages"
    label: "Pages"
    folder: "content"
    create: true
    slug: "{{slug}}"
    fields:
      - { label: "Title", name: "title", widget: "string" }
      - { label: "Body", name: "body", widget: "markdown" }
```

---

## Troubleshooting

### "Unable to authenticate" at /admin/
- Make sure Git Gateway is enabled (Step 3, item 4)
- Make sure Identity is enabled (Step 3, item 1)
- Try clearing browser cache and cookies

### Posts not appearing after publish
- Netlify rebuilds take ~1 minute — wait and refresh
- Check the Netlify deploy log for build errors
- Make sure the post's `draft` field is set to `false`

### Images not loading
- Check that `media_folder` in `config.yml` matches your Hugo static directory
- Verify the image was uploaded to `static/uploads/`

---

## Costs

| Service | Free tier |
|---------|-----------|
| Netlify hosting | 100 GB bandwidth/month, 300 build min/month |
| Netlify Identity | Up to 5 invited users |
| GitHub | Unlimited public repos |
| **Total** | **$0/month** for a light blog |

You'd only start paying if you exceed 5 CMS users or get very heavy traffic.
