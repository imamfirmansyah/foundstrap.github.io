---
title: FAQ & Troubleshooting
weight: 100
type: docs
breadcrumbs: true
cascade:
  type: docs
---

Frequently asked questions and solutions to common issues.

## General Questions

**Do I need coding knowledge?**
Basic HTML/CSS knowledge recommended. No programming required for content changes.

**Is this responsive?**
Yes, fully responsive with Bootstrap 5 mobile-first approach.

**What image sizes should I use?**
Keep original dimensions. Exp Hero: 1920x1080px, Course cards: 400x300px.

## Installation Issues

**Images not showing after upload**

```text
❌ Wrong path: /img/logo.png
✅ Correct: assets/img/logo.png
```

- Check relative paths
- Verify assets folder uploaded

**Sliders/carousels broken**

1. Open F12 → Console for JS errors
2. Verify assets/js/swiper-bundle.min.js exists
3. Check swiper-wrapper contains swiper-slide children

**Animations not working**

1. Verify assets/js/aos.js loaded
2. Check elements have data-aos="fade-up" attributes
3. Console: AOS.init() called?

## Customization Issues

**Colors not changing**

```text

1. Edit assets/css/main.css (not inline styles)
2. Clear browser cache (Ctrl+Shift+R)
3. Check !important overrides
```

**Fonts not loading**

```text

1. Google Fonts link in <head> correct?
2. Custom fonts in assets/fonts/ with @font-face?
3. F12 → Network tab → Failed requests?
```

**Layout broken after editing**

```text
✅ Keep Bootstrap row/col structure
✅ Don't delete required wrapper divs
✅ Maintain section padding classes
```

## Performance Issues

**Mobile menu not working**

```text

1. Verify bootstrap.bundle.min.js loaded
2. Check navbar-toggler data-bs-toggle="collapse"
3. Console errors?
```

## Browser Compatibility

**Supported browsers:**

- Chrome 90+, Firefox 88+, Safari 15+, Edge 90+
- Mobile: iOS Safari 15+, Chrome Android 90+

**Internet Explorer:** Not supported (use .ie-fallback classes if needed)

## Common Error Messages

**F12 Console errors:**

```text
"jQuery is not defined" → Check jquery-3.7.1.min.js load order
"Uncaught ReferenceError: Swiper is not defined" → Swiper JS missing
"AOS is not defined" → AOS JS missing
"Failed to load resource" → Check file paths
```

## Getting Help

**Still stuck?**

1. Check browser Console (F12)
2. Verify file structure matches documentation
3. Test locally first (Live Server)
4. Contact support with:
   - Screenshot of error
   - F12 Console errors
   - Hosting provider

## Version Updates

**To update to newer version:**

```text

1. Backup your customizations (main.css, main.js, images)
2. Download latest from ThemeForest
3. Replace HTML/assets files
4. Merge your customizations back
```

Continue to **Source & Credits** for licensing and attribution requirements.
