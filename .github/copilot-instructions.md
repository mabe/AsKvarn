# AsKvarn - Copilot Instructions

## Project Overview
Jekyll-based static website for Ås väderkvarn (Ås windmill), a historical Swedish windmill in Derome, Varberg. The site documents the mill's history, restoration progress, and photo gallery. Content is in Swedish.

## Architecture & Structure

### Theme & Styling
- Built on HTML5 UP's "Story" theme (free under CCA 3.0 license)
- Modular SCSS architecture in `_sass/`:
  - `libs/` - Variables (`_vars.scss`), functions, mixins, skel framework
  - `components/` - Reusable components (banner, spotlight, gallery, etc.)
  - `base/` - Typography and page foundations
  - `layout/` - Layout wrappers
- Main stylesheet: `assets/css/main.scss` imports all SCSS modules
- JavaScript in `assets/js/` (~950 LOC total): jQuery, scrolling effects, lightbox gallery

### Content Structure
- **Posts**: `_posts/YYYY-MM-DD-title.markdown` with frontmatter:
  ```yaml
  layout: post
  title: "Title"
  date: 2024-12-24 12:00:00 +0200
  image: images/photo.jpg
  description: "Brief description"
  type: banner fullscreen
  ```
- **Layouts**: `_layouts/default.html` (main wrapper), `_layouts/post.html`
- **Pages**: Root-level HTML files (`index.html`, `about.html`, `history.html`, `other.html`)
- **Images**: `images/` directory with historical photos (JPG format, various years)

### Key Components
- **Banner sections**: Full-screen hero sections with content + image (`.banner.style1`)
- **Spotlight sections**: Alternating left/right content blocks (`.spotlight.style1`)
- **Gallery**: Dynamic gallery from `_posts` with lightbox functionality
- **Liquid templating**: Uses `{{ site.baseurl }}`, `{{ site.title }}`, post loops

## Development Workflow

### Local Development
```bash
bundle install                  # Install dependencies
bundle exec jekyll serve        # Run dev server at http://localhost:4000/AsKvarn
```

### GitHub Pages Deployment
- Configured in `_config.yml` with `baseurl: /AsKvarn`
- Uses `github-pages` gem for automatic deployment
- Lives at: `https://mabe.github.io/AsKvarn`
- **Critical**: Always use `{{ site.baseurl }}` prefix for internal links/assets

## Project-Specific Conventions

### Swedish Language Content
- All user-facing content is in Swedish
- Date formats: `date_to_long_string` filter for Swedish dates
- Maintain Swedish naming in titles, descriptions, and navigation

### Image Handling
- Photos stored in `/images/` with descriptive filenames (e.g., `1978.jpg`, `Flygfoto1.jpg`)
- Post images referenced in frontmatter: `image: images/photo.jpg`
- Use relative paths from root, not from baseurl

### HTML/CSS Patterns
- Section structure: `<section class="[banner|spotlight] style1 orient-[left|right] ...">`
- Content-image pairs: `.content` div + `.image` div within sections
- Scroll animations: `onscroll-image-fade-in`, `onload-content-fade-right`
- Responsive breakpoints defined in `main.scss` via `skel-breakpoints`

### SCSS Variables
- Color palette, sizing, duration timing in `_sass/libs/_vars.scss`
- Use `_size()`, `_palette()`, `_duration()` functions from libs
- Maintain consistency with existing `$misc`, `$duration`, `$size`, `$font` maps

## Common Tasks

### Adding a New Post
1. Create `_posts/YYYY-MM-DD-slug.markdown` with required frontmatter
2. Add image to `images/` directory
3. Reference image path in frontmatter
4. Post appears automatically in index.html gallery

### Modifying Styles
- Edit component-specific files in `_sass/components/`
- Adjust global variables in `_sass/libs/_vars.scss`
- Changes compile through `assets/css/main.scss`

### Adding Pages
- Create HTML file in root with layout: `default` in frontmatter
- Follow existing patterns for banner/spotlight sections
- Update navigation links in other pages if needed

## Dependencies
- Jekyll 3.7.3
- Minima theme ~2.0
- GitHub Pages gem
- jekyll-feed ~0.6

## Notes
- No test infrastructure exists (static content site)
- No build scripts beyond Jekyll's built-in compilation
- Gemfile.lock tracked for reproducible builds
- Site excludes: vendor/, _site/, .sass-cache/
