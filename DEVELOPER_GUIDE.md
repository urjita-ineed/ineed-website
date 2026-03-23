# ineed - Developer Guide

Complete reference guide for developing and maintaining the ineed marketing website.

## 🎨 Design System

### Color Palette
```css
Primary: #000 (Black) - Main branding color
Accent:  #ff6b35 (Orange) - Highlight and CTAs
Text:    #333 (Dark Gray) - Primary text
Secondary: #666 (Medium Gray) - Secondary text
Background: #f8f8f8 (Light Gray) - Section backgrounds
White:   #fff - Card and surface backgrounds
Border:  #e0e0e0 - Borders and dividers
```

### Typography
- **Font Stack**: System fonts (no web fonts for performance)
  - `-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif`
- **Line Height**: 1.6 (general), 1.2 (headings), 1.8 (descriptive text)
- **Font Weights**: 400 (normal), 500 (medium), 600 (semi-bold), bold (700)

### Spacing Scale
```
0.25rem (4px)  - xs
0.5rem  (8px)  - sm
1rem    (16px) - md
1.5rem  (24px) - lg
2rem    (32px) - xl
3rem    (48px) - 2xl
4rem    (64px) - 3xl
5rem    (80px) - 4xl
6rem    (96px) - 5xl
```

### Breakpoints
```
Desktop:  1200px+ (primary targets: 1200px, 1400px, 1920px)
Tablet:   768px - 1199px
Mobile:   480px - 767px
Small:    < 480px
```

## 📁 Folder Structure Conventions

```
ineed_website/
├── index.html              # Main landing page
├── [page].html             # Individual page files
├── css/
│   └── styles.css         # All styling (single file for performance)
├── js/
│   └── main.js            # All JavaScript (minimal, vanilla JS only)
├── images/                # (Future) Image assets
├── assets/                # (Future) Fonts, icons, etc
├── README.md              # Project documentation
├── robots.txt             # SEO robots configuration
├── sitemap.xml            # XML sitemap for search engines
└── .htaccess              # Apache server configuration
```

## 🏗️ HTML Structure Conventions

### Page Template
Every HTML page should follow this structure:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="...">
    <title>Page Title - ineed</title>
    <link rel="stylesheet" href="css/styles.css">
</head>
<body>
    <!-- Navbar (copied from index.html) -->
    
    <!-- Main content sections -->
    
    <!-- Footer (copied from index.html) -->
    
    <script src="js/main.js"></script>
</body>
</html>
```

### Semantic HTML
Always use semantic elements:
- `<header>` for page headers
- `<nav>` for navigation
- `<main>` for main content
- `<section>` for content sections
- `<article>` for blog posts or standalone content
- `<aside>` for sidebars
- `<footer>` for page footer

### Heading Hierarchy
- `<h1>` - One per page (page title)
- `<h2>` - Section titles
- `<h3>` - Subsection titles
- `<h4>` - Minor headings
- Never skip heading levels

## 🎯 CSS Best Practices

### Naming Conventions
Use BEM (Block Element Modifier) for class names:
```css
/* Block */
.service-card { }

/* Element */
.service-card__icon { } /* or use .service-icon for simplicity */

/* Modifier */
.service-card--featured { }

/* Exception: Utility classes are simple */
.text-center { }
.mb-2 { }
```

### Selector Style
```css
/* ✅ Good - Class based, simple, fast */
.hero-title { }

/* ✅ Good - Element + class for specificity */
h1.hero-title { }

/* ❌ Avoid - ID selectors */
#hero-title { }

/* ❌ Avoid - Overly specific */
div.section.hero > h1.title { }
```

### CSS Organization
1. Global styles (*, :root, body)
2. Typography
3. Components (navbar, buttons, cards)
4. Layout sections (hero, services, etc.)
5. Utilities
6. Responsive design (media queries at end)

### Adding Responsive Styles
```css
/* Mobile first approach */
.service-card {
    grid-template-columns: 1fr;  /* Mobile default */
}

/* Tablet */
@media (min-width: 768px) {
    .service-card {
        grid-template-columns: repeat(2, 1fr);
    }
}

/* Desktop */
@media (min-width: 1200px) {
    .service-card {
        grid-template-columns: repeat(3, 1fr);
    }
}
```

## 🚀 JavaScript Best Practices

### Keep it Minimal
- Only use vanilla JavaScript (no jQuery, no frameworks)
- Maximum ~200 lines of code
- Focus on progressive enhancement
- Site must work even if JS fails to load

### Code Style
```javascript
// ✅ Good - Clear, simple, readable
document.addEventListener('DOMContentLoaded', function() {
    const hamburger = document.getElementById('hamburger');
    if (hamburger) {
        hamburger.addEventListener('click', toggleMenu);
    }
});

// ❌ Avoid - Overly complex or jQuery syntax
$('#hamburger').on('click', function() { /* ... */ });
```

### Event Delegation
```javascript
// ❌ Avoid - Adding listeners to multiple elements
document.querySelectorAll('.btn').forEach(btn => {
    btn.addEventListener('click', handleClick);
});

// ✅ Good - Event delegation on parent
document.addEventListener('click', function(e) {
    if (e.target.matches('.btn')) {
        handleClick();
    }
});
```

## 📝 Adding New Pages

### Step 1: Create HTML File
```bash
# Create contact-us.html (for example)
```

### Step 2: Use Template
Copy the structure from index.html or another page

### Step 3: Update Navigation
Add link to `navbar-menu` in all HTML files:
```html
<a href="/contact-us.html" class="nav-link">Contact Us</a>
```

### Step 4: Update Footer Links
Add to footer in all pages if needed

### Step 5: Add to Sitemap
Update `sitemap.xml`:
```xml
<url>
    <loc>https://ineed.com/contact-us.html</loc>
    <lastmod>2026-03-12</lastmod>
    <priority>0.8</priority>
</url>
```

## 🛠️ Adding New Components

### Adding a Service Card
```html
<div class="service-card">
    <div class="service-icon">🔧</div>
    <h3>Service Name</h3>
    <p>Short service description</p>
</div>
```

### Adding a Button
```html
<button class="btn btn-primary">Click Me</button>
<button class="btn btn-secondary">Secondary</button>
```

### Adding a Hero Section
```html
<section class="hero">
    <div class="hero-content">
        <h1>Headline</h1>
        <p>Description</p>
        <button class="btn btn-primary">CTA</button>
    </div>
    <div class="hero-illustration">
        <!-- Image or SVG -->
    </div>
</section>
```

## 🔍 SEO Checklist

When adding new content:
- [ ] Write descriptive title (50-60 chars)
- [ ] Add meta description (150-160 chars)
- [ ] Use proper heading hierarchy
- [ ] Include alt text for images
- [ ] Use descriptive anchor text (not "click here")
- [ ] Add internal links when relevant
- [ ] Mobile-friendly content
- [ ] Fast page load
- [ ] No broken links

### Meta Tags Template
```html
<!-- For each page, customize these -->
<meta name="description" content="Unique, descriptive summary of page content. 150-160 characters.">
<meta name="keywords" content="relevant, keywords, here">

<!-- Open Graph for sharing -->
<meta property="og:title" content="Page Title">
<meta property="og:description" content="Page description">
<meta property="og:image" content="https://ineed.com/image.png">
<meta property="og:url" content="https://ineed.com/page.html">
```

## 🐛 Common Issues & Solutions

### Issue: Navbar menu doesn't toggle on mobile
**Solution**: Check that `js/main.js` is loading, verify hamburger ID matches

### Issue: Styles not applying
**Solution**: Clear browser cache (Ctrl+Shift+R or Cmd+Shift+R), verify CSS file path

### Issue: Links broken
**Solution**: Ensure paths are relative, use `/` for root-relative paths

### Issue: Form not submitting
**Solution**: Form needs backend integration or service like Formspree

### Issue: Images not loading
**Solution**: Create `images/` folder, use relative paths like `images/photo.png`

## 📊 Performance Tips

### Optimization Checklist
- [ ] Minify CSS properly (no build tools needed - it's already ~800 lines)
- [ ] Minify JS before deployment
- [ ] Optimize images (compress, use WebP where possible)
- [ ] Use CDN for assets if needed
- [ ] Enable GZIP compression (.htaccess handles this)
- [ ] Set appropriate cache headers (.htaccess handles this)
- [ ] Lazy load images (when adding many)
- [ ] Remove unused CSS

### Lighthouse Audit
Test your site with Google Lighthouse:
1. Open DevTools (F12)
2. Go to Lighthouse tab
3. Run audit
4. Target: 90+ on all metrics

### Page Speed Tools
- Google PageSpeed Insights
- GTmetrix
- WebPageTest
- Lighthouse

## 🔐 Security Best Practices

### Do's
- ✅ Keep dependencies updated (check annually)
- ✅ Use HTTPS in production
- ✅ Validate forms server-side
- ✅ Sanitize any dynamic content
- ✅ Include security headers (.htaccess includes these)

### Don'ts
- ❌ Store sensitive data in HTML
- ❌ Use unknown CDNs
- ❌ Expose API keys in frontend code
- ❌ Trust user input without validation
- ❌ Include comments with sensitive info

## 📱 Mobile Testing

### Devices to Test
- iPhone 12 Mini (small)
- iPhone 12 (medium)
- iPad (tablet)
- Android phone
- Android tablet

### Testing Tools
- Chrome DevTools device emulation
- Firefox Responsive Design Mode
- Real device testing
- BrowserStack for device cloud

### Mobile Checklist
- [ ] Touch targets at least 44x44px
- [ ] Text readable without zoom
- [ ] No horizontal scroll
- [ ] Forms easy to fill on mobile
- [ ] Navigation accessible on small screens
- [ ] Images scale properly

## 🚀 Deployment Checklist

Before going live:
- [ ] All links work (internal and external)
- [ ] Forms connected to backend
- [ ] SSL certificate installed
- [ ] Custom domain configured
- [ ] Email setup complete
- [ ] Analytics installed (if using)
- [ ] 404 page configured
- [ ] Sitemap.xml submitted to search engines
- [ ] Robots.txt optimized
- [ ] CDN configured (optional)
- [ ] Monitoring/uptime checks setup
- [ ] Backup system in place

## 📚 Additional Resources

### Learning Resources
- [MDN Web Docs](https://developer.mozilla.org/)
- [CSS Tricks](https://css-tricks.com/)
- [Web Dev by Google](https://web.dev/)
- [A11y Project](https://www.a11yproject.com/)

### Tools
- [Web Performance Analyzer](https://www.webpagetest.org/)
- [WAVE Accessibility Tool](https://wave.webaim.org/)
- [Lighthouse CI](https://github.com/GoogleChrome/lighthouse-ci)

## 📞 Support & Maintenance

### Monthly Tasks
- Check for broken links
- Verify form functionality
- Review analytics
- Update content if needed

### Quarterly Tasks
- Full responsive testing
- Performance audit
- SEO review
- Security check

### Annually Tasks
- Update SSL certificates
- Review and update privacy/terms
- Major design audit
- Technology stack review

---

**Last Updated**: March 12, 2026  
**Version**: 1.0  
**Maintained By**: ineed Dev Team
