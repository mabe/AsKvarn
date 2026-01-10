# Ås väderkvarn (AsKvarn)

Jekyll-based static website for Ås väderkvarn (Ås windmill), a historical Swedish windmill in Derome, Varberg. The site documents the mill's history, restoration progress, and photo gallery. Content is in Swedish.

The site is live at: [https://mabe.github.io/AsKvarn](https://mabe.github.io/AsKvarn)

## Architecture & Structure

### Theme & Styling
- Built on [HTML5 UP's "Story" theme](https://html5up.net/story) (free under CCA 3.0 license)
- Modular SCSS architecture in `_sass/`:
  - `libs/` - Variables (`_vars.scss`), functions, mixins, skel framework
  - `components/` - Reusable components (banner, spotlight, gallery, etc.)
  - `base/` - Typography and page foundations
  - `layout/` - Layout wrappers
- Main stylesheet: `assets/css/main.scss` imports all SCSS modules
- JavaScript in `assets/js/` (~950 LOC total): jQuery, scrolling effects, lightbox gallery

### Content Structure
- **Posts**: `_posts/YYYY-MM-DD-title.markdown`
- **Layouts**: `_layouts/default.html` (main wrapper), `_layouts/post.html`
- **Pages**: Root-level HTML files (`index.html`, `about.html`, `history.html`, `other.html`)
- **Images**: `images/` directory with historical photos (JPG format)

### Key Components
- **Banner sections**: Full-screen hero sections (`.banner.style1`)
- **Spotlight sections**: Alternating left/right content blocks (`.spotlight.style1`)
- **Gallery**: Dynamic gallery from `_posts` with lightbox functionality

## Development Workflow

### Local Development
Prerequisites: Ruby, Bundler, Jekyll.

```bash
bundle install                  # Install dependencies
bundle exec jekyll serve        # Run dev server at http://localhost:4000/AsKvarn
```

### GitHub Pages Deployment
- Configured in `_config.yml` with `baseurl: /AsKvarn`
- Uses `github-pages` gem for automatic deployment
- **Critical**: Always use `{{ site.baseurl }}` prefix for internal links/assets

## Conventions

### Swedish Language Content
- All user-facing content is in Swedish
- Date formats: `date_to_long_string` filter for Swedish dates

### Image Handling
- Photos stored in `/images/` with descriptive filenames (e.g., `1978.jpg`)
- Post images referenced in frontmatter: `image: images/photo.jpg`
- Use relative paths from root

### HTML/CSS Patterns
- Section structure: `<section class="[banner|spotlight] style1 orient-[left|right] ...">`
- Scroll animations: `onscroll-image-fade-in`, `onload-content-fade-right`

## Common Tasks

### Adding a New Post
1. Create `_posts/YYYY-MM-DD-slug.markdown` with required frontmatter:
   ```yaml
   layout: post
   title: "Title"
   date: 2024-12-24 12:00:00 +0200
   image: images/photo.jpg
   description: "Brief description"
   type: banner fullscreen
   ```
2. Add image to `images/` directory
3. Reference image path in frontmatter

## Dependencies
- Jekyll 3.7.3
- Minima theme ~2.0
- GitHub Pages gem
- jekyll-feed ~0.6
