# Jue Gong's Blog

A modern Jekyll blog built with 2025 best practices, featuring automated deployment, SEO optimization, and responsive design.

## Features

- **Modern Jekyll 4.3** with latest plugins
- **Automated GitHub Actions deployment**
- **SEO optimized** with jekyll-seo-tag
- **Responsive design** with dark mode support
- **Modern MathJax 3** for mathematical expressions
- **Pagination and archives** for better content organization
- **Performance optimized** with modern web standards
- **Accessibility compliant** (WCAG 2.1 AA)

## Prerequisites

- Ruby 3.1+ 
- Bundler gem
- Node.js 18+ (for development tools)

## Local Development

### 1. Clone and Install Dependencies

```bash
git clone https://github.com/gongjue/gongjue.github.io.git
cd gongjue.github.io
bundle install
npm install
```

### 2. Run Development Server

```bash
# Start Jekyll with live reload
npm run serve

# Or use bundle directly
bundle exec jekyll serve --livereload
```

Visit `http://localhost:4000` to see your site.

### 3. Build for Production

```bash
npm run build
```

## Writing Posts

Create new posts in the `_posts` directory with the format: `YYYY-MM-DD-title.md`

```markdown
---
layout: post
title: "Your Post Title"
categories: [category1, category2]
tags: [tag1, tag2]
---

Your content here...
```

### Adding Figures

Your blog supports professional figures with captions and multiple layout options. See `FIGURES.md` for complete documentation.

**Basic usage:**
```markdown
{% include figure.html 
   src="/images/your-image.jpg" 
   alt="Alt text" 
   caption="Your caption" %}
```

**Advanced usage with layouts:**
```markdown
{% include figure-advanced.html 
   src="/images/your-image.jpg" 
   alt="Alt text" 
   caption="Your caption"
   layout="left" 
   size="medium" %}
```

## Deployment

The site automatically deploys via GitHub Actions when you push to the main branch. The workflow:

1. Builds the Jekyll site
2. Runs tests and linting
3. Deploys to GitHub Pages

## Configuration

Key settings in `_config.yml`:

- **Site info**: Update `name`, `description`, `url`
- **Social links**: Configure `footer-links`
- **Analytics**: Add your Google Analytics ID
- **Comments**: Configure Disqus shortname

## Moar!

I've created a more detailed walkthrough, [**Build A Blog With Jekyll And GitHub Pages**](http://www.smashingmagazine.com/2014/08/01/build-blog-jekyll-github-pages/) over at the Smashing Magazine website. Check it out if you'd like a more detailed walkthrough and some background on Jekyll. :metal:

It covers:

- A more detailed walkthrough of setting up your Jekyll blog
- Common issues that you might encounter while using Jekyll
- Importing from Wordpress, using your own domain name, and blogging in your favorite editor
- Theming in Jekyll, with Liquid templating examples
- A quick look at Jekyll 2.0’s new features, including Sass/Coffeescript support and Collections

## Jekyll Now Features

✓ Command-line free _fork-first workflow_, using GitHub.com to create, customize and post to your blog  
✓ Fully responsive and mobile optimized base theme (**[Theme Demo](http://jekyllnow.com)**)  
✓ Sass/Coffeescript support using Jekyll 2.0  
✓ Free hosting on your GitHub Pages user site  
✓ Markdown blogging  
✓ Syntax highlighting  
✓ Disqus commenting  
✓ Google Analytics integration  
✓ SVG social icons for your footer  
✓ 3 http requests, including your avatar  

✘ No installing dependancies  
✘ No need to set up local development  
✘ No configuring plugins  
✘ No need to spend time on theming  
✘ More time to code other things ... wait ✓!  

## Questions?

[Open an Issue](https://github.com/barryclark/jekyll-now/issues/new) and let's chat!

## Other forkable themes

You can use the [Quick Start](https://github.com/barryclark/jekyll-now#quick-start) workflow with other themes that are set up to be forked too! Here are some of my favorites:

- [Hyde](https://github.com/poole/hyde) by MDO
- [Lanyon](https://github.com/poole/lanyon) by MDO
- [mojombo.github.io](https://github.com/mojombo/mojombo.github.io) by Tom Preston-Werner
- [Left](https://github.com/holman/left) by Zach Holman
- [Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes) by Michael Rose
- [Skinny Bones](https://github.com/mmistakes/skinny-bones-jekyll) by Michael Rose

## Credits

- [Jekyll](https://github.com/jekyll/jekyll) - Thanks to its creators, contributors and maintainers.
- [SVG icons](https://github.com/neilorangepeel/Free-Social-Icons) - Thanks, Neil Orange Peel. They're beautiful. 
- [Solarized Light Pygments](https://gist.github.com/edwardhotchkiss/2005058) - Thanks, Edward.
- [Joel Glovier](http://joelglovier.com/writing/) - Great Jekyll articles. I used Joel's feed.xml in this repository.
- [David Furnes](https://github.com/dfurnes), [Jon Uy](https://github.com/jonuy), [Luke Patton](https://github.com/lkpttn) - Thanks for the design/code reviews.
- [Bart Kiers](https://github.com/bkiers), [Florian Simon](https://github.com/vermluh), [Henry Stanley](https://github.com/henryaj), [Hun Jae Lee](https://github.com/hunjaelee), [Javier Cejudo](https://github.com/javiercejudo), [Peter Etelej](https://github.com/etelej), [Ben Abbott](https://github.com/jaminscript), [Ray Nicholus](https://github.com/rnicholus) - Thanks for your [fantastic contributions](https://github.com/barryclark/jekyll-now/commits/master) to the project!


## Development Commands

```bash
# Install dependencies
bundle install && npm install

# Start development server
npm run serve

# Build for production
npm run build

# Run tests
npm run test

# Lint CSS
npm run lint:css
```

## 2025 Modernization Features

✅ **Jekyll 4.3** with modern plugin architecture  
✅ **GitHub Actions CI/CD** for automated deployment  
✅ **SEO optimization** with structured data and meta tags  
✅ **Responsive design** with CSS Grid and Flexbox  
✅ **Dark mode support** respecting system preferences  
✅ **Modern MathJax 3** for mathematical expressions  
✅ **Accessibility compliance** (WCAG 2.1 AA)  
✅ **Performance optimized** with lazy loading and compression  
✅ **Security headers** and Content Security Policy  
✅ **Modern development workflow** with linting and testing  

## License

MIT License - feel free to use this for your own projects!