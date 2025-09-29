# Personal Profile Site

A personal portfolio website built with Jekyll 4.4+ using the [Creative Theme](http://startbootstrap.com/template-overviews/creative/) from Start Bootstrap. This is a fully customizable, single-page Bootstrap site with a modern, tokenized configuration system.

**✨ Key Features:**
- Fully tokenized configuration - all content managed through `_config.yml`
- Modern modular SCSS architecture (7-1 pattern with Sass modules)
- Bootstrap 5.3.8 with responsive design
- Font Awesome 6.7.2 icons
- Smooth scrolling animations
- GitHub Pages ready with automated deployment

**🔗 Live Site:** [https://wmorr.github.io](https://wmorr.github.io)

---

## Quick Start

### Prerequisites

You'll need these installed on your machine:

**Git**
- Windows: [Git for Windows](https://gitforwindows.org/)
- macOS: `xcode-select --install`
- Linux: `sudo apt-get install -y git`

**Ruby + Bundler**
- Windows: [Ruby+Devkit from RubyInstaller](https://rubyinstaller.org/)
- macOS: `brew install ruby`
- Linux: `sudo apt-get install -y ruby-full build-essential zlib1g-dev`

Then install Bundler:
```bash
gem install bundler
```

### Local Development

1. **Clone the repository:**
   ```bash
   git clone https://github.com/wmorr/wmorr.github.io.git
   cd wmorr.github.io
   ```

2. **Install dependencies:**
   ```bash
   bundle install
   ```

3. **Serve locally:**
   ```bash
   bundle exec jekyll serve
   ```
   Open [http://localhost:4000](http://localhost:4000) in your browser.

4. **Serve with live reload:**
   ```bash
   bundle exec jekyll serve --livereload
   ```

---

## Architecture: Tokenization & Modularity

This project follows Jekyll best practices with a **fully tokenized, modular architecture** that separates content from presentation.

### Why Tokenization?

Traditional static sites hard-code content directly into HTML templates, making updates tedious and error-prone. This site uses **Liquid template variables** to pull all content from a central configuration file (`_config.yml`), providing:

- **Single source of truth** - All content in one place
- **Zero HTML editing** - Update text, images, and links without touching templates
- **Type safety** - Structured YAML prevents formatting errors
- **Version control friendly** - Content changes are clearly visible in diffs
- **Rapid customization** - Fork, edit config, deploy

### How It Works

**Traditional approach (❌ Hard-coded):**
```html
<h1>Your Favorite Source of Free Bootstrap Themes</h1>
<p>Start Bootstrap can help you build...</p>
```

**This project (✅ Tokenized):**
```html
<h1>{{ site.hero.heading }}</h1>
<p>{{ site.hero.description }}</p>
```

**Configuration (_config.yml):**
```yaml
hero:
  heading: Your Favorite Source of Free Bootstrap Themes
  description: Start Bootstrap can help you build...
```

### Modular Components

Each page section lives in its own include file (`_includes/`):
- `header.html` → Hero section
- `services.html` → Services grid (loops through `site.services.list`)
- `portfolio.html` → Portfolio grid (loops through `site.portfolio`)
- `contact.html` → Contact section with social links

These components are:
1. **Reusable** - Include anywhere in any layout
2. **Composable** - Reorder by changing include order in `_layouts/front.html`
3. **Self-contained** - Each manages its own markup and styling
4. **Data-driven** - All content pulled from `_config.yml`

### Benefits

✅ **No code knowledge required** - Edit YAML, not HTML
✅ **Maintainable** - Update content without breaking markup
✅ **Scalable** - Add portfolio items, services, etc. as array entries
✅ **Static & fast** - No database, all compiled at build time
✅ **GitHub Pages compatible** - Uses only standard Jekyll features

---

## Customization

All site content is managed through `_config.yml`. No need to edit HTML files!

### Site Metadata
```yaml
title: wmorr                    # Browser tab title
email: your-email@example.com
description: 'Your site description'
author: Your Name
twitter_username: yourhandle
github_username: yourhandle
```

### Navigation
```yaml
brand_name: Your Brand          # Top-left navbar brand
```

### Hero Section
The landing section with heading and call-to-action:
```yaml
hero:
  heading: Your main headline
  description: Your tagline or description
  button_text: Call to Action
  button_link: "#about"         # Anchor link or URL
```

### Call-to-Action Section
```yaml
cta:
  heading: Section heading
  description: Longer description text
  button_text: Button text
  button_link: "#services"
```

### Services Section
Define up to 4 services (or skills):
```yaml
services:
  heading: Services Heading
  list:
    - icon: fa-diamond           # Font Awesome icon
      title: Service Name
      description: Service description
      delay: 0                   # Animation delay
    - icon: fa-paper-plane
      title: Another Service
      description: Another description
      delay: .1s
```

**Available Font Awesome Icons:** See [Font Awesome 6 Free icons](https://fontawesome.com/search?o=r&m=free) (use `fa-solid` or `fa-brands` prefix)

### Portfolio Section
Showcase projects with images:
```yaml
portfolio:
  - image: img/portfolio/1.jpg   # Image path
    category: Project Type
    name: Project Name
    link: "#"                    # Project URL or modal link
  - image: img/portfolio/2.jpg
    category: Another Type
    name: Another Project
    link: "https://example.com"
```

Add your images to `img/portfolio/` and reference them here.

### Aside Section
A prominent call-out section:
```yaml
aside:
  heading: Download or special offer text
  button_text: Download Now!
  button_link: "#"
```

### Contact Section
```yaml
contact:
  heading: Let's Get In Touch!
  description: Contact prompt or additional info
```

Social links (Twitter, Email, GitHub) are shown automatically using the usernames defined at the top of `_config.yml`.

---

## Site Structure

```
.
├── _includes/          # Reusable HTML components
│   ├── head.html       # <head> metadata
│   ├── nav.html        # Navigation bar
│   ├── header.html     # Hero section
│   ├── call-to-action.html
│   ├── services.html   # Services grid
│   ├── portfolio.html  # Portfolio grid
│   ├── aside.html      # CTA aside
│   ├── contact.html    # Contact section
│   └── scripts.html    # JavaScript includes
├── _layouts/
│   └── front.html      # Main layout composing all sections
├── _sass/              # Modern SCSS architecture (7-1 pattern)
│   ├── abstracts/      # Variables, functions, mixins
│   ├── base/           # Reset, typography, utilities
│   ├── components/     # Buttons, service-box, portfolio-box
│   ├── layout/         # Navigation, header, sections, contact
│   ├── pages/          # Page-specific styles
│   └── vendors/        # Bootstrap overrides
├── css/
│   └── main.scss       # Master stylesheet (uses @use/@forward)
├── img/                # Images and graphics
├── js/                 # JavaScript files
├── _config.yml         # Site configuration (edit this!)
├── Gemfile             # Ruby dependencies
└── index.html          # Entry point
```

**To reorder or remove sections:** Edit `_layouts/front.html` and rearrange the `{% include %}` statements.

### Modern SCSS Architecture

This project uses the **7-1 Pattern** with modern Sass module system (`@use`/`@forward`):

- **No deprecation warnings** - Uses `color.adjust()` instead of deprecated `darken()`
- **CSS Custom Properties** - Runtime theming support for future light/dark modes
- **Modular & maintainable** - Each component in its own file
- **BEM-ready** - Structured for easy migration to BEM naming
- **Bootstrap 5 compatible** - Modern grid and components

---

## Deploying to GitHub Pages

This site is configured as a **user site** (`wmorr.github.io`), meaning it will be available at `https://wmorr.github.io`.

### Automated Deployment (Recommended)

The repository includes a **GitHub Actions workflow** (`.github/workflows/jekyll.yml`) that automatically builds and deploys your site on every push to the `master` branch.

**Setup Steps:**

### Step 1: Enable GitHub Pages

1. Go to your repository on GitHub
2. Navigate to **Settings** → **Pages**
3. Under **Build and deployment**, select **GitHub Actions** (not "Deploy from branch")

### Step 2: Push Changes

```bash
git add .
git commit -m "Deploy site to GitHub Pages"
git push origin master
```

GitHub Actions will automatically:
1. Build the Jekyll site with modern Sass compilation
2. Deploy to GitHub Pages

**Monitor progress:** Check the **Actions** tab in your repository for build status.

Once the workflow completes (✅ green checkmark), your site will be live at **https://wmorr.github.io**

### Important: URL Configuration

For a **user site** (repo named `username.github.io`):
- `url`: `"https://wmorr.github.io"`
- `baseurl`: `"/"` or `""` (either works)

These are already correctly configured in your `_config.yml`.

---

## Troubleshooting

**"Could not locate Gemfile"**
- Make sure you're in the project directory
- Run `bundle install`

**"bundle: command not found"**
- Bundler isn't installed. Run `gem install bundler`

**Site builds but CSS/images don't load**
- Check that `baseurl` in `_config.yml` is set to `"/"`
- Clear your browser cache

**GitHub Actions build fails**
- Check the Actions tab for error details
- Ensure `Gemfile` has no syntax errors
- Verify all image paths in `_config.yml` point to existing files

**Local site looks different from GitHub Pages**
- Make sure you're using `bundle exec jekyll serve` (not just `jekyll serve`)
- Check that your Ruby version matches the workflow (3.3)

**Changes not appearing on live site**
- Wait 1-2 minutes for GitHub Actions to rebuild
- Hard refresh your browser (Ctrl+Shift+R or Cmd+Shift+R)
- Check the Actions tab to ensure the build succeeded

---

## Adding New Portfolio Images

1. Add your image to `img/portfolio/` (recommended size: 650x350px)
2. Update `_config.yml` portfolio section with the new item
3. Commit and push

Example:
```yaml
portfolio:
  - image: img/portfolio/my-new-project.jpg
    category: Web Development
    name: My Awesome Project
    link: "https://github.com/wmorr/my-project"
```

---

## Theme Customization

### Colors

Theme colors are defined as **CSS Custom Properties** in `_sass/abstracts/_variables.scss`:

```scss
:root {
  --color-primary: #F05F40;       // Primary color (buttons, links)
  --color-primary-dark: #d94621;  // Hover states
  --color-dark: #222;              // Dark sections background
  --color-light: #fff;             // Light sections background
}
```

**Benefits of CSS Custom Properties:**
- Runtime theming (can be changed without rebuilding)
- Future-ready for light/dark mode switching
- Browser DevTools can inspect/change values live

### Backward Compatibility

SCSS variables are still available for color functions:
```scss
$theme-primary: #F05F40;
$theme-dark: #222;
```

Change values in `_sass/abstracts/_variables.scss` and rebuild (`bundle exec jekyll build`).

---

## Credits

- **Jekyll:** Static site generator - [jekyllrb.com](https://jekyllrb.com)
- **Creative Theme:** Start Bootstrap - [startbootstrap.com](http://startbootstrap.com)
- **Bootstrap:** Front-end framework - [getbootstrap.com](https://getbootstrap.com)
- **Font Awesome:** Icon library - [fontawesome.com](https://fontawesome.com)

---

## License

See [LICENCE](LICENCE) file for details.
