# Implementation Guide for Remaining Pages
## Coyote Agency ADA Compliance Refactoring

**Status:** 3 of 7 pages complete (43%)  
**Date:** December 12, 2024

---

## Overview

This guide provides step-by-step instructions for completing the ADA compliance refactoring of the remaining 4 pages. The pattern has been established across 3 completed pages, making the remaining work straightforward.

---

## Completed Pages (Reference Examples)

1. **index.html** - Hero + Services + Newsletter
2. **about.html** - Text-heavy content page
3. **services.html** - Grid layout with article cards

---

## Remaining Pages

### 1. meet-the-team.html (from 3meet-the-team.html)
### 2. blog.html (from 4blog.html)  
### 3. blueprint.html (from 6blueprint.html)
### 4. offthehook.html (from 7offthehook.html)

---

## Step-by-Step Process

### Step 1: Extract Content

For each original file, identify and extract:

```bash
# Search for main headings
grep -n "<h1\|<h2\|<h3" [original-file.html] | head -30

# Search for paragraphs with content
grep -n "white-space:pre-wrap" [original-file.html] | head -50

# Search for images
grep -n "<img" [original-file.html] | head -20

# Search for forms
grep -n "<form\|<input" [original-file.html]
```

### Step 2: Use the Template

Copy the structure from any completed page as your template. The basic structure is:

```html
<!DOCTYPE html>
<html lang="en-US">
<head>
    <!-- Standard meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    
    <!-- Page-specific title and description -->
    <title>[Page Title] | Coyote Agency</title>
    <meta name="description" content="[Page description]">
    
    <!-- Open Graph meta tags -->
    <meta property="og:type" content="website">
    <meta property="og:url" content="https://www.coyote.agency/[page-name]">
    <meta property="og:title" content="[Page Title] | Coyote Agency">
    
    <!-- Stylesheets -->
    <link rel="stylesheet" href="styles/main.css">
</head>
<body>
    <!-- Skip link -->
    <a href="#main-content" class="skip-link">Skip to main content</a>
    
    <!-- Header (copy from any completed page) -->
    <header role="banner" class="site-header">
        <!-- ... header content ... -->
    </header>
    
    <!-- Main content -->
    <main id="main-content" role="main">
        <!-- Your page-specific content here -->
    </main>
    
    <!-- Footer (copy from any completed page) -->
    <footer role="contentinfo" class="site-footer">
        <!-- ... footer content ... -->
    </footer>
    
    <!-- Scripts (copy from any completed page) -->
    <script>
        <!-- Mobile menu and year scripts -->
    </script>
</body>
</html>
```

### Step 3: Structure Your Content

#### For Text-Heavy Pages (like About):
```html
<section class="about-section" aria-labelledby="main-heading">
    <div class="content-container">
        <h1 id="main-heading">Page Title</h1>
        
        <div class="about-content">
            <p>Content paragraphs...</p>
        </div>
    </div>
</section>
```

#### For Card/Grid Layouts (like Services):
```html
<section class="services-detail-section" aria-labelledby="section-heading">
    <div class="content-container">
        <h2 id="section-heading">Section Title</h2>
        
        <div class="services-grid">
            <article class="service-card">
                <h3>Card Title</h3>
                <p>Card content...</p>
            </article>
            <!-- More cards -->
        </div>
    </div>
</section>
```

#### For Team Member Profiles:
```html
<section class="team-section" aria-labelledby="team-heading">
    <div class="content-container">
        <h2 id="team-heading">Meet the Team</h2>
        
        <div class="team-grid">
            <article class="team-member">
                <img src="[image-url]" 
                     alt="[Name], [Role] at Coyote Agency"
                     width="300"
                     height="300">
                <h3>[Name]</h3>
                <p class="role">[Role]</p>
                <p>[Bio]</p>
            </article>
            <!-- More team members -->
        </div>
    </div>
</section>
```

### Step 4: Apply ADA Best Practices

#### Always Include:

1. **Skip Link** (first element in body)
```html
<a href="#main-content" class="skip-link">Skip to main content</a>
```

2. **Proper ARIA Labels**
```html
<nav role="navigation" aria-label="Main navigation">
<button aria-label="Toggle navigation menu" aria-expanded="false">
<section aria-labelledby="heading-id">
```

3. **Descriptive Alt Text**
```html
<!-- Good -->
<img src="logo.png" alt="Coyote Agency - Digital Marketing Agency Logo">

<!-- Bad -->
<img src="logo.png" alt="logo">
```

4. **Form Labels**
```html
<label for="email" class="visually-hidden">Email Address</label>
<input type="email" 
       id="email" 
       name="email" 
       required
       aria-required="true">
```

5. **Current Page Indicator**
```html
<a href="current-page.html" aria-current="page">Current Page</a>
```

6. **External Link Indicators**
```html
<a href="https://external.com" 
   target="_blank" 
   rel="noopener noreferrer"
   aria-label="Link text (opens in new window)">
```

### Step 5: Add Page-Specific CSS

If your page needs custom styles, add them to `styles/main.css` following the pattern:

```css
/* Page-Name Specific Styles */
.page-specific-section {
    padding: var(--spacing-xl) 0;
    background-color: var(--color-background-dark);
}

.page-specific-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: var(--spacing-lg);
}

.page-specific-card {
    padding: var(--spacing-md);
    border: 2px solid var(--color-primary);
    border-radius: 8px;
}
```

### Step 6: Test for Accessibility

#### Keyboard Navigation Test:
1. Tab through all interactive elements
2. Verify focus indicators are visible
3. Test Escape key closes mobile menu
4. Verify skip link appears on focus

#### Screen Reader Test (if available):
1. NVDA (Windows) or VoiceOver (Mac)
2. Navigate by headings (H key in NVDA)
3. Navigate by landmarks (D key in NVDA)
4. Verify all images have alt text
5. Verify form labels are announced

#### Mobile Test:
1. Test on actual device or browser DevTools
2. Verify touch targets are adequate (44px minimum)
3. Test mobile menu functionality
4. Verify responsive layout works

---

## Page-Specific Guidelines

### meet-the-team.html

**Content Type:** Team member profiles with photos and bios

**Recommended Structure:**
```html
<main id="main-content">
    <section class="team-intro-section">
        <h1>Meet the Team</h1>
        <p>Introduction text</p>
    </section>
    
    <section class="team-section">
        <div class="team-grid">
            <article class="team-member">
                <img src="..." alt="[Name], [Role]">
                <h3>[Name]</h3>
                <p class="role">[Role]</p>
                <p>[Bio]</p>
            </article>
        </div>
    </section>
</main>
```

**CSS to Add:**
```css
.team-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: var(--spacing-lg);
}

.team-member {
    text-align: center;
}

.team-member img {
    border-radius: 50%;
    width: 200px;
    height: 200px;
    object-fit: cover;
    margin: 0 auto var(--spacing-sm);
}

.team-member .role {
    font-weight: 700;
    color: var(--color-accent);
    margin-bottom: var(--spacing-sm);
}
```

### blog.html

**Content Type:** Blog post listing or blog content

**Recommended Structure:**
```html
<main id="main-content">
    <section class="blog-section">
        <h1>Blog</h1>
        
        <div class="blog-posts">
            <article class="blog-post">
                <h2><a href="[post-url]">Post Title</a></h2>
                <p class="post-meta">
                    <time datetime="2024-01-01">January 1, 2024</time>
                    <span class="category">Category</span>
                </p>
                <p>Excerpt...</p>
                <a href="[post-url]" class="read-more">Read More</a>
            </article>
        </div>
    </section>
</main>
```

**CSS to Add:**
```css
.blog-posts {
    max-width: 800px;
    margin: 0 auto;
}

.blog-post {
    margin-bottom: var(--spacing-lg);
    padding-bottom: var(--spacing-lg);
    border-bottom: 1px solid var(--color-text-light);
}

.blog-post h2 {
    margin-bottom: var(--spacing-sm);
}

.post-meta {
    font-size: 0.875rem;
    color: var(--color-text-light);
    margin-bottom: var(--spacing-sm);
}

.post-meta time,
.post-meta .category {
    margin-right: var(--spacing-sm);
}

.read-more {
    font-weight: 700;
    text-decoration: underline;
}
```

### blueprint.html

**Content Type:** Brand positioning interactive tool/form

**Recommended Structure:**
```html
<main id="main-content">
    <section class="blueprint-intro">
        <h1>Brand Blueprint</h1>
        <p>Description of the tool</p>
    </section>
    
    <section class="blueprint-form-section">
        <form class="blueprint-form">
            <fieldset>
                <legend>Brand Information</legend>
                <!-- Form fields -->
            </fieldset>
        </form>
    </section>
</main>
```

**Important:** If there's an interactive tool, ensure:
- All form fields have labels
- Use `<fieldset>` and `<legend>` for grouped inputs
- Provide clear instructions
- Include error messaging
- Make submit button descriptive

### offthehook.html

**Content Type:** Call for writers / submission form

**Recommended Structure:**
```html
<main id="main-content">
    <section class="offthehook-intro">
        <h1>Off the Hook</h1>
        <p>Call for writers description</p>
    </section>
    
    <section class="submission-section">
        <h2>Submit Your Work</h2>
        <form class="submission-form">
            <!-- Submission form fields -->
        </form>
    </section>
</main>
```

---

## Common Pitfalls to Avoid

### ❌ Don't:
- Use `<div>` or `<span>` as buttons - use `<button>`
- Use `<div>` for navigation - use `<nav>`
- Skip heading levels (h1 → h3)
- Use placeholder as only label
- Use "click here" without context
- Forget `aria-current` on current page
- Use generic alt text like "image" or "logo"

### ✅ Do:
- Use semantic HTML5 elements
- Include ARIA attributes
- Provide descriptive labels
- Maintain heading hierarchy
- Test with keyboard only
- Use `visually-hidden` class for screen reader only text
- Include skip navigation link
- Mark external links appropriately

---

## CSS Variables Reference

Use these existing CSS custom properties:

```css
/* Colors */
--color-primary: #000000
--color-secondary: #ffffff
--color-accent: #e85d04
--color-text: #333333
--color-text-light: #666666
--color-background: #ffffff
--color-background-dark: #1a1a1a

/* Spacing */
--spacing-xs: 0.5rem
--spacing-sm: 1rem
--spacing-md: 2rem
--spacing-lg: 4rem
--spacing-xl: 6rem

/* Typography */
--font-primary: 'Poppins', sans-serif
--font-heading: 'Archivo Black', 'Poppins', sans-serif
```

---

## Testing Checklist

For each completed page, verify:

- [ ] Page has unique, descriptive title
- [ ] Skip link is present and functional
- [ ] All images have descriptive alt text
- [ ] Heading hierarchy is proper (h1 → h2 → h3)
- [ ] All form fields have labels
- [ ] Current page is marked with `aria-current="page"`
- [ ] External links marked with appropriate aria-label
- [ ] Mobile menu works with keyboard (Escape to close)
- [ ] Focus indicators visible on all interactive elements
- [ ] Page is responsive (mobile, tablet, desktop)
- [ ] No inline styles (all in main.css)
- [ ] Navigation consistent across pages
- [ ] Footer consistent across pages

---

## Estimated Time Per Page

Based on completed pages:

- **Content extraction:** 15-20 minutes
- **HTML structure:** 30-40 minutes
- **CSS styling:** 20-30 minutes
- **Testing & refinement:** 15-20 minutes

**Total per page:** ~1.5-2 hours

**Remaining pages:** 4 × 1.5 hours = ~6 hours total

---

## Resources

### Completed Files (Reference):
- `index.html` - Hero section example
- `about.html` - Text content example
- `services.html` - Grid layout example
- `styles/main.css` - All styles with comments

### Documentation:
- `ADA_COMPLIANCE_REPORT.md` - Full ADA audit and fixes
- `IMPLEMENTATION_GUIDE.md` - This file

### Testing Tools:
- **WAVE:** https://wave.webaim.org/
- **axe DevTools:** Browser extension
- **Screen Readers:** NVDA (Windows), VoiceOver (Mac/iOS)
- **Keyboard:** Test with Tab, Shift+Tab, Enter, Escape

---

## Questions?

If you encounter issues:

1. **Check completed pages** for similar patterns
2. **Review ADA_COMPLIANCE_REPORT.md** for solutions
3. **Test incrementally** - don't wait until page is complete
4. **Use browser DevTools** to inspect elements
5. **Validate HTML** at https://validator.w3.org/

---

## Final Steps

Once all pages are complete:

1. **Cross-browser test** (Chrome, Firefox, Safari, Edge)
2. **Mobile device test** (actual devices if possible)
3. **Screen reader test** (at least one page fully)
4. **Run WAVE** on each page
5. **Verify all navigation links work**
6. **Check form submissions**
7. **Update ADA_COMPLIANCE_REPORT.md** with completion status

---

**Good luck! The pattern is established - the remaining pages follow the same approach.**
