# Adding Figures to Your Jekyll Blog

This guide explains how to add figures (images with captions) to your Jekyll blog posts.

## Quick Start

### 1. Basic Images (Markdown)

The simplest way to add images:

```markdown
![Alt text]({{ site.baseurl }}/images/your-image.jpg)
```

### 2. Simple Figures with Captions

Use the basic figure include:

```markdown
{% include figure.html 
   src="/images/your-image.jpg" 
   alt="Alt text" 
   caption="Your figure caption here" %}
```

### 3. Advanced Figures with Layout Options

Use the advanced figure include for more control:

```markdown
{% include figure-advanced.html 
   src="/images/your-image.jpg" 
   alt="Alt text" 
   caption="Your figure caption here"
   layout="center" 
   size="medium" %}
```

## Layout Options

- **`center`** (default): Centered figure
- **`left`**: Float left with text wrapping
- **`right`**: Float right with text wrapping  
- **`full-width`**: Full width figure extending to page edges

## Size Options

- **`small`**: Max width 300px
- **`medium`**: Max width 500px
- **`large`**: Max width 700px
- **`full`**: Full container width

## Examples

### Centered Figure (Default)

```markdown
{% include figure.html 
   src="/images/architecture-diagram.png" 
   alt="System architecture diagram" 
   caption="Figure 1: Overall system architecture showing data flow" %}
```

### Left-Aligned Figure

```markdown
{% include figure-advanced.html 
   src="/images/logo.png" 
   alt="Company logo" 
   caption="Our company logo"
   layout="left" 
   size="small" %}
```

### Full-Width Figure

```markdown
{% include figure-advanced.html 
   src="/images/hero-image.jpg" 
   alt="Hero image" 
   caption="A stunning landscape photograph"
   layout="full-width" %}
```

### Numbered Figure

```markdown
{% include figure-advanced.html 
   src="/images/results-chart.png" 
   alt="Performance results chart" 
   caption="Performance comparison between different algorithms"
   number="2" %}
```

## Image Guidelines

### File Organization

- Store all images in the `/images/` directory
- Use descriptive filenames (e.g., `system-architecture-2024.png`)
- Use appropriate formats:
  - **PNG**: For screenshots, diagrams, images with text
  - **JPG**: For photographs
  - **SVG**: For logos, icons, and scalable graphics
  - **WebP**: For optimized web images

### Image Optimization

- Compress images before uploading
- Use appropriate dimensions (don't upload 4000px wide images for blog posts)
- Consider using WebP format for better compression

### Accessibility

- Always provide meaningful `alt` text
- Keep captions concise but descriptive
- Ensure sufficient color contrast

## Custom Styling

You can override figure styles by adding custom CSS to your `style.scss` file:

```scss
// Custom figure styles
.figure {
  &.my-custom-style {
    border: 2px solid #007acc;
    padding: 10px;
  }
}
```

## Troubleshooting

### Images Not Showing

1. Check the file path is correct
2. Ensure the image file exists in the `/images/` directory
3. Verify the filename case matches exactly

### Layout Issues

1. Clear your browser cache
2. Rebuild your Jekyll site: `bundle exec jekyll build`
3. Check for CSS conflicts

### Mobile Responsiveness

All figures are automatically responsive and will stack properly on mobile devices. 