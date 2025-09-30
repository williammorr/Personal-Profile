# Personal Profile Site

A personal portfolio website built with Jekyll 4.4+ using the [Creative Theme](http://startbootstrap.com/template-overviews/creative/) from Start Bootstrap. This is a fully customizable, single-page Bootstrap site with a modern, tokenized configuration system.

**✨ Key Features:**
- Fully tokenized configuration - all content managed through `_config.yml`
- Modern modular SCSS architecture (7-1 pattern with Sass modules)
- Bootstrap 5.3.8 with responsive design
- Font Awesome 6.7.2 icons
- Smooth scrolling animations
- GitHub Pages ready with automated deployment

**🔗 Live Site:** [https://williammorr.github.io/Personal-Profile](https://williammorr.github.io/Personal-Profile)

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
   git clone https://github.com/williammorr/Personal-Profile.git
   cd Personal-Profile
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

### Color Theme (New in Week 9!)

**🎨 User-Customizable Color Theming System**

Your site now supports easy color customization! Choose from 5 pre-defined color palettes without editing any CSS.

#### Available Color Palettes

- **orange** - Warm, energetic (default)
- **blue** - Professional, trustworthy
- **green** - Fresh, growth-oriented
- **purple** - Creative, sophisticated
- **red** - Bold, attention-grabbing

#### How to Change Colors

Edit the `theme` section in `_config.yml`:

```yaml
theme:
  brand_primary: "orange"      # Main brand color - Choose: orange, blue, green, purple, red
  brand_secondary: "blue"      # Optional accent color - Choose: orange, blue, green, purple, red, or null
  neutral: "slate"             # Text/backgrounds - Choose: slate, gray
  mode: "light"                # Theme mode - Choose: light, dark, auto
```

Then rebuild your site:
```bash
bundle exec jekyll build
```

**That's it!** All buttons, links, navigation, and portfolio overlays will automatically use your chosen colors.

#### Theme Modes

The theming system now supports three modes:

- **`light`** - Always display light theme (white background, dark text)
- **`dark`** - Always display dark theme (dark background, light text)
- **`auto`** - Automatically respect user's OS/browser theme preference

For complete details, see [THEMING.md](THEMING.md).

#### Separation of Concerns

The theming system separates user configuration from system files:

**User Configuration** (`_config.yml`):
- ✅ Simple color selection (brand_primary, brand_secondary, neutral)
- ✅ No technical knowledge required
- ✅ Clear options and comments

**System Files** (not user-editable):
- `_data/color-palettes.yml` - Color palette library (5 palettes × 10 shades each)
- `_includes/design-tokens.html` - Dynamic token generation logic
- `_sass/` - Component styles using semantic tokens

#### Under the Hood

The theming system uses:
- **Color Palette Library** - 5 palettes × 10 shades each (50-900) in `_data/color-palettes.yml`
- **Liquid Template Engine** - Resolves user selection to CSS custom properties
- **Semantic Tokens** - Components reference meaningful names (`--color-primary`, `--color-secondary`, `--color-text`)
- **CSS Custom Properties** - Runtime theming without recompilation

See `_includes/design-tokens.html` for the full token architecture.

#### Implementation Status

- ✅ **Phase 1** (Complete): Color palette selection system
- ✅ **Phase 2** (Complete): Multi-color support (5 palettes)
- ✅ **Phase 3** (Complete): Dark theme support with `mode: "light"`, `mode: "dark"`, and `mode: "auto"`
- 🔄 **Phase 4** (Future): Theme toggle button (optional)
- 🔄 **Phase 5** (Future): Custom color overrides for advanced users

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
- **CSS Custom Properties** - Runtime theming support for light/dark modes
- **Modular & maintainable** - Each component in its own file
- **BEM-ready** - Structured for easy migration to BEM naming
- **Bootstrap 5 compatible** - Modern grid and components
- **User-Customizable Colors** (Week 9) - Choose from 5 color palettes via `_config.yml`

#### CSS File Structure

**Design Tokens (Dynamic):**
- `_includes/design-tokens.html` → Generates CSS custom properties from user theme selection
  - Reads color selection from `_config.yml` (brand_primary, brand_secondary, neutral)
  - Resolves palettes from `_data/color-palettes.yml` (system file)
  - Creates 20-30 color shades depending on configuration
  - Defines semantic tokens (--color-primary, --color-secondary, --color-text, --bg-dark, etc.)
  - Injected into `<head>` before main.css for proper cascade

**Your Custom Styles (Modular):**
- `css/main.scss` → Compiles to `main.css` (13KB)
- `_sass/` → Modular SCSS architecture (7-1 pattern)
  - `abstracts/` - Variables, functions, mixins (now includes token documentation)
  - `base/` - Reset, typography, utilities
  - `components/` - Buttons, service boxes, portfolio boxes (now use CSS custom properties)
  - `layout/` - Navigation, header, sections, contact (now use CSS custom properties)
  - `pages/` - Page-specific styles
  - `vendors/` - Bootstrap 5 overrides

**Third-Party Libraries (CDN):**
- **Bootstrap 5.3.8** - Framework via CDN (no local files)
- **Font Awesome 6.7.2** - Icons via CDN (no local files)

**Vendor CSS (Local):**
- `css/animate.min.css` (53KB) - Animate.css library for WOW.js animations
  - **Not modularized** - Third-party library kept separate per best practices
  - Update by replacing entire file when needed

---

## Deploying to GitHub Pages

This site is configured as a **project site** (`Personal-Profile`), meaning it will be available at `https://williammorr.github.io/Personal-Profile`.

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

Once the workflow completes (✅ green checkmark), your site will be live at **https://williammorr.github.io/Personal-Profile**

### Important: URL Configuration

For a **project site** (repo named `Personal-Profile`):
- `url`: `"https://williammorr.github.io"`
- `baseurl`: `"/Personal-Profile"` (must match repository name exactly)

These are already correctly configured in your `_config.yml`.

**Why the baseurl matters:** Project sites are served from a subdirectory, so all links need the `/Personal-Profile` prefix to work correctly.

---

## Troubleshooting

### Local Development Issues

**"Could not locate Gemfile"**
- Make sure you're in the project directory
- Run `bundle install`

**"bundle: command not found"**
- Bundler isn't installed. Run `gem install bundler`

**Site builds but CSS/images don't load locally**
- The site is configured for project site deployment with `baseurl: "/Personal-Profile"`
- When testing locally, use: `bundle exec jekyll serve --baseurl ""`
- Or visit: `http://localhost:4000/Personal-Profile/`

### GitHub Pages Deployment Issues

**404 Error on GitHub Pages**
- ✅ **Repository name:** Must be `Personal-Profile` (case-sensitive)
- ✅ **GitHub Pages enabled:** Settings → Pages → Source: "GitHub Actions"
- ✅ **Baseurl matches repo name:** `_config.yml` has `baseurl: "/Personal-Profile"`
- ✅ **Branch is correct:** Workflow triggers on `master` branch
- ✅ **Workflow file exists:** `.github/workflows/jekyll.yml` is present

**CSS/JS/Images don't load on GitHub Pages (404 errors)**
- Check that `baseurl` in `_config.yml` is set to `"/Personal-Profile"` (must match repository name exactly)
- Verify all asset links use `| relative_url` filter in templates
- Check browser console for 404 errors showing the wrong path

**GitHub Actions build fails**
- Check the **Actions** tab for error details
- Common issues:
  - Missing `Gemfile` or syntax errors
  - Image paths in `_config.yml` pointing to non-existent files
  - SCSS compilation errors (should show in build logs)

**Changes not appearing on live site**
- Wait 1-2 minutes for GitHub Actions to rebuild
- Check the **Actions** tab to verify build succeeded (green checkmark)
- Hard refresh your browser (Ctrl+Shift+R or Cmd+Shift+R)
- Clear browser cache completely

**Site URL is correct but shows old content**
- GitHub Pages has CDN caching (can take 5-10 minutes)
- Check if the latest commit triggered a build in Actions tab
- Try accessing in private/incognito browser window

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
    link: "https://github.com/williammorr/my-project"
```

---

## Theme Customization

### Colors (Week 9: User-Customizable System)

**✨ Easy Color Customization** - No CSS editing required!

Theme colors are now configured in `_config.yml` using pre-defined color palettes:

```yaml
theme:
  brand_primary: "orange"      # Main brand color
  brand_secondary: "blue"      # Optional accent color (or null)
  neutral: "slate"             # Text/backgrounds
  mode: "light"                # Theme mode - Choose: light, dark, auto
```

**How it works:**

1. **User Configuration** - Simple color selection in `_config.yml` (brand_primary, brand_secondary, neutral)
2. **Color Palette Library** - System file `_data/color-palettes.yml` contains 5 palettes × 10 shades each
3. **Dynamic Token Generation** - `_includes/design-tokens.html` resolves your selection
4. **CSS Custom Properties** - Generates semantic tokens (--color-primary, --color-secondary, --color-text, etc.)
5. **Component Integration** - All components reference semantic tokens, not hardcoded colors

**Example: Switching to Blue Primary with Green Secondary**

```yaml
# Change this in _config.yml
theme:
  brand_primary: "blue"
  brand_secondary: "green"
```

Then rebuild:
```bash
bundle exec jekyll build
```

All buttons, navigation, links, and portfolio overlays instantly use your chosen palette!

**Available Palettes:**
- **orange** (#f97316) - Warm, energetic (default)
- **blue** (#3b82f6) - Professional, trustworthy
- **green** (#22c55e) - Fresh, growth-oriented
- **purple** (#a855f7) - Creative, sophisticated
- **red** (#ef4444) - Bold, attention-grabbing

**Benefits:**
- ✅ No CSS knowledge required
- ✅ Consistent color system (10 shades per palette)
- ✅ Semantic naming (primary, hover, active, text, background)
- ✅ Runtime theming via CSS custom properties
- ✅ Future-ready for dark mode (Phase 2)

### Advanced: Custom Colors

For advanced users who want colors not in the pre-defined palettes:

1. Add a new palette to `_data/color-palettes.yml` (system file)
2. Follow the same structure as existing palettes (shades 50-900)
3. Reference your custom palette name in `theme.brand_primary` or `theme.brand_secondary`

**Example** (`_data/color-palettes.yml`):
```yaml
teal:
  50: "#f0fdfa"
  100: "#ccfbf1"
  # ... continue with 200-900
  500: "#14b8a6"    # Base color
  900: "#134e4a"
```

Then use in `_config.yml`:
```yaml
theme:
  brand_primary: "teal"
```

See `_includes/design-tokens.html` for the complete token architecture.

---

## Credits

- **Jekyll:** Static site generator - [jekyllrb.com](https://jekyllrb.com)
- **Creative Theme:** Start Bootstrap - [startbootstrap.com](http://startbootstrap.com)
- **Bootstrap:** Front-end framework - [getbootstrap.com](https://getbootstrap.com)
- **Font Awesome:** Icon library - [fontawesome.com](https://fontawesome.com)

---

## License

See [LICENCE](LICENCE) file for details.
