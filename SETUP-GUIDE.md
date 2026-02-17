# Hugo + Stack Theme + Decap CMS + Netlify: Setup Guide

## What you'll get
- A fast, card-style blog using the [Stack theme](https://stack.jimmycai.com/) hosted for free on Netlify
- A web-based admin panel at `yoursite.com/admin/` where the blogger can write posts with a rich text editor (like WordPress)
- The blogger never touches code or Git — they just log in and write
- Dark/light mode, search, archives, tags, and categories built in

---

## Step 1: Push to GitHub

Create a **private** repository on GitHub (e.g., `my-blog`), then push this project:

```bash
cd my-blog
git branch -m master main
git add -A
git commit -m "Initial commit: Hugo Stack + Decap CMS"
git remote add origin https://github.com/YOUR_USERNAME/my-blog.git
git push -u origin main
```

> **Note:** The theme is included as a git submodule. If you cloned from a tarball,
> you'll need to add it first:
> `git submodule add https://github.com/CaiJimmy/hugo-theme-stack.git themes/hugo-theme-stack`

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

### Custom domain
- Go to **Domain management** → **Add custom domain**
- Add a CNAME record in your domain registrar's DNS pointing to your Netlify site
- Netlify auto-provisions a free SSL certificate
- Update `baseURL` in `config/_default/hugo.toml` to your domain

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
5. After confirming, they can log in at `yoursite.com/admin/`

---

## Step 5: The blogger's workflow

Share these instructions with the blogger:

### Writing a new post
1. Go to `https://yoursite.com/admin/`
2. Log in with your email (or Google if enabled)
3. Click **"Blog Posts"** in the sidebar
4. Click **"New Blog Posts"**
5. Fill in the title, date, description, categories, tags
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
├── config/
│   └── _default/
│       ├── hugo.toml        # Main Hugo config (baseURL, title, theme)
│       ├── params.toml      # Theme parameters (sidebar, widgets, etc.)
│       ├── menu.toml        # Navigation menus
│       └── markup.toml      # Markdown rendering settings
├── content/
│   ├── _index.md            # Homepage
│   ├── page/
│   │   ├── archives/        # Archives page
│   │   └── search/          # Search page
│   └── post/                # Blog posts (managed by Decap CMS)
│       └── welcome/
│           └── index.md
├── layouts/
│   └── partials/
│       └── head/
│           └── custom.html  # Injects Netlify Identity widget
├── static/
│   ├── admin/
│   │   ├── index.html       # Decap CMS admin page
│   │   └── config.yml       # CMS configuration (collections, fields)
│   └── uploads/             # Media uploads from the CMS
├── themes/
│   └── hugo-theme-stack/    # Stack theme (git submodule)
├── netlify.toml             # Netlify build config
└── .gitignore
```

---

## Customization

### Site settings
Edit `config/_default/hugo.toml` to change the site title, base URL, etc.

### Theme appearance
Edit `config/_default/params.toml` to customize:
- Sidebar emoji and subtitle
- Color scheme (dark/light/auto)
- Widgets (search, archives, tag cloud)
- Article settings (reading time, table of contents)

### Add more CMS fields
Edit `static/admin/config.yml` to add new fields. See [Decap CMS widgets docs](https://decapcms.org/docs/widgets/).

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

### Build fails on Netlify
- Check that `HUGO_VERSION` in `netlify.toml` is set to `0.155.0` or higher
- Stack requires Hugo extended edition (Netlify uses extended by default)

---

## Costs

| Service | Free tier |
|---------|-----------|
| Netlify hosting | 100 GB bandwidth/month, 300 build min/month |
| Netlify Identity | Up to 5 invited users |
| GitHub | Unlimited private repos |
| **Total** | **$0/month** for a light blog |

You'd only start paying if you exceed 5 CMS users or get very heavy traffic.
