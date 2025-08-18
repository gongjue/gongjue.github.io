# Jue Gong's Blog

A modern Jekyll blog built with the Chirpy theme, featuring automated deployment, bilingual support (silent), and modern web standards.

## Features

- **Chirpy Theme v7.3.1** - Modern, responsive Jekyll theme
- **Jekyll 4.4.1** with Ruby 3.4.5
- **Automated GitHub Actions deployment**
- **SEO optimized** with jekyll-seo-tag
- **Responsive design** with dark/light mode toggle
- **Mermaid diagram support** with theme-aware styling
- **Code syntax highlighting** with customizable padding
- **RSS/Atom feed** auto-generation
- **Further Reading** recommendations based on tags/categories
- **Bilingual foundation** (Chinese pages exist but silent)
- **Performance optimized** with modern web standards

## Prerequisites

- Ruby 3.3+ 
- Bundler gem
- Jekyll 4.4+

## Local Development

### 1. Clone and Install Dependencies

```bash
git clone https://github.com/gongjue/gongjue.github.io.git
cd gongjue.github.io
bundle install
```

### 2. Run Development Server

```bash
# Start Jekyll with live reload
bundle exec jekyll serve --livereload

# Build for production
bundle exec jekyll build
```

Visit `http://localhost:4000` to see your site.

## Site Structure

The site uses the Chirpy theme structure with these main sections:

```
Navigation:
├── Home (/)
├── Categories (/categories/)
├── Tags (/tags/)
├── Archives (/archives/)
└── About (/about/)

Posts:
└── /:year/:month/:day/:title/ (SEO-friendly permalinks)
```

## Writing Posts

Create new posts in the `_posts` directory with the format: `YYYY-MM-DD-title.md`

```markdown
---
layout: post
title: "Your Post Title"
categories: [category1, category2]
tags: [tag1, tag2, tag3]
---

Your content here...

## Mermaid Diagrams

\`\`\`mermaid
graph TD
    A[Start] --> B[Process]
    B --> C[End]
\`\`\`
```

### Tag & Category Strategy

For effective "Further Reading" recommendations:
- **Categories**: Use broad topics (AI, Data Science, MLOps)
- **Tags**: Use specific keywords (machine-learning, python, api-design)
- **Consistency**: Maintain consistent naming across posts

## Deployment

The site automatically deploys via GitHub Actions when you push to the main branch:

1. Builds Jekyll site with Chirpy theme
2. Generates RSS feed and sitemaps
3. Deploys to GitHub Pages

## Configuration

Key settings in `_config.yml`:

- **Site info**: title, description, url
- **Social links**: GitHub, Twitter, email
- **Comments**: Disabled (provider: empty)
- **Permalinks**: `/:year/:month/:day/:title/`
- **Kramdown**: Syntax highlighting without line numbers

## Theme Customizations

- **Custom CSS**: `/assets/css/custom.css` for code block padding
- **Mermaid Support**: Theme-aware diagram rendering
- **RSS Feed**: Auto-generated at `/feed.xml`
- **No Comments**: Disqus disabled for faster loading

## Development Commands

```bash
# Install dependencies
bundle install

# Start development server
bundle exec jekyll serve --livereload

# Build for production
bundle exec jekyll build

# Check for updates
bundle update
```

## Migration History

- **2025-08**: Migrated from Jekyll Now to Chirpy theme
- **Ruby**: Upgraded from 2.6.10 to 3.4.5
- **Jekyll**: Upgraded to 4.4.1
- **Features**: Added Mermaid support, custom CSS, improved navigation

## RSS Feed

RSS/Atom feed is automatically available at:
- **URL**: `https://gongjue.github.io/feed.xml`
- **Format**: Atom 1.0 with full post content
- **Auto-updates**: Regenerated on each build

## Credits

- [Jekyll](https://github.com/jekyll/jekyll) - Static site generator
- [Chirpy Theme](https://github.com/cotes2020/jekyll-theme-chirpy) - Beautiful Jekyll theme
- [Mermaid](https://mermaid.js.org/) - Diagram generation
- [GitHub Actions](https://github.com/features/actions) - CI/CD automation

## License

MIT License - feel free to use this for your own projects!