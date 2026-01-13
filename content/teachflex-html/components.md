---
title: Components
weight: 70
type: docs
breadcrumbs: true
cascade:
  type: docs
---

Detailed guide for Teachflex interactive components: sliders, animations, icons, forms, and modals.

## Swiper Sliders (v12.0.3)

Teachflex uses Swiper for Logo carousels.

### Logo Carousel example

```html
<div
  class="swiper tf-carousel-logos"
  data-items="5"
  data-items-tablet="3"
  data-items-mobile="2"
  data-space-between="24"
  data-speed="1200"
  data-autoplay-delay="2000"
>
  <div class="swiper-wrapper">
    <div class="swiper-slide">
      <img src="assets/img/logoipsum-01.png" class="img-fluid" alt="Logo Client 01" />
    </div>
    <div class="swiper-slide">
      <img src="assets/img/logoipsum-02.png" class="img-fluid" alt="Logo Client 02" />
    </div>
    <div class="swiper-slide">
      <img src="assets/img/logoipsum-03.png" class="img-fluid" alt="Logo Client 03" />
    </div>
    <div class="swiper-slide">
      <img src="assets/img/logoipsum-04.png" class="img-fluid" alt="Logo Client 04" />
    </div>
    <div class="swiper-slide">
      <img src="assets/img/logoipsum-05.png" class="img-fluid" alt="Logo Client 05" />
    </div>
    <div class="swiper-slide">
      <img src="assets/img/logoipsum-06.png" class="img-fluid" alt="Logo Client 06" />
    </div>
    <div class="swiper-slide">
      <img src="assets/img/logoipsum-07.png" class="img-fluid" alt="Logo Client 07" />
    </div>
    <div class="swiper-slide">
      <img src="assets/img/logoipsum-08.png" class="img-fluid" alt="Logo Client 08" />
    </div>
    <div class="swiper-slide">
      <img src="assets/img/logoipsum-09.png" class="img-fluid" alt="Logo Client 09" />
    </div>
    <div class="swiper-slide">
      <img src="assets/img/logoipsum-10.png" class="img-fluid" alt="Logo Client 10" />
    </div>
    <div class="swiper-slide">
      <img src="assets/img/logoipsum-11.png" class="img-fluid" alt="Logo Client 11" />
    </div>
    <div class="swiper-slide">
      <img src="assets/img/logoipsum-12.png" class="img-fluid" alt="Logo Client 12" />
    </div>
  </div>
</div>
```

**Swiper Carousel** (assets/js/main.js):

```js
/*!
 * 02.2 Carousel Logos (Swiper)
 */
const initCarousel = () => {
  const carousels = document.querySelectorAll(".tf-carousel-logos");
  if (!carousels.length) return;
  carousels.forEach((el) => {
    const items = parseInt(el.dataset.items) || 5;
    const itemsTablet = parseInt(el.dataset.itemsTablet) || 3;
    const itemsMobile = parseInt(el.dataset.itemsMobile) || 2;
    const spaceBetween = parseInt(el.dataset.spaceBetween) || 30;
    const delay = parseInt(el.dataset.autoplayDelay) || 2500;
    const speed = parseInt(el.dataset.speed) || 800;
    if (typeof Swiper !== "undefined") {
      new Swiper(el, {
        slidesPerView: itemsMobile,
        spaceBetween,
        loop: true,
        speed,
        autoplay: { delay, disableOnInteraction: false },
        breakpoints: {
          768: { slidesPerView: itemsTablet },
          1024: { slidesPerView: items, slidesPerGroup: 1 },
        },
      });
    }
  });
};
```

## AOS Animations

Animate On Scroll (AOS) adds scroll-triggered animations.

### Basic usage

```html
<div data-aos="fade-up" data-aos-duration="800">Content that fades up on scroll</div>
```

**Common AOS effects:**

- fade-up, fade-down, fade-left, fade-right
- zoom-in, flip-left, flip-up
- slide-up, slide-left

**Initialization** (main.js):

```js
AOS.init({
  duration: 1000,
  easing: "ease",
  once: true,
  offset: 120,
});
```

## Bootstrap Icons (v1.13.1)

Over 2,000 icons included locally.

### Usage

```html
<i class="bi bi-play-fill text-primary"></i>
<i class="bi bi-person-circle"></i>
<i class="bi bi-star-fill text-warning"></i>
```

**Popular icons for education:**

```html
bi-play-fill, bi-person-circle, bi-star-fill, bi-clock, bi-calendar bi-book, bi-laptop, bi-phone, bi-envelope,
bi-check-circle
```

**Full list:** [bootstrap-icons.com](https://icons.getbootstrap.com/)

## Navbar mobile toggle

Mobile menu controlled by Bootstrap.

### Toggle behavior

```html
<!-- Mobile Toogler : Start here -->
<button
  class="navbar-toggler"
  type="button"
  data-bs-toggle="offcanvas"
  data-bs-target="#offcanvasNavbar"
  aria-controls="offcanvasNavbar"
  aria-label="Toggle navigation"
>
  <span class="navbar-toggler-icon"></span>
</button>
<!-- Mobile Toogler : End here -->
```

## Counters

Counter use custom JS.

### Counter example

```html
<span class="tf-counter" data-target="2.4" data-suffix="K Users" data-prefix="+" data-duration="2000">0</span>

<span
  class="tf-counter tf-heading tf-heading-xl"
  data-target="1200"
  data-suffix="+"
  data-duration="2000"
  data-delimiter="."
  >0</span
>
```

**Counter animation** (main.js):

```js
/*!
 * 02.1 Counter Animation
 */
const initCounter = () => {
  const counters = document.querySelectorAll(".tf-counter");
  if (!counters.length) return;

  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (!entry.isIntersecting) return;
      const el = entry.target;
      const target = parseFloat(el.dataset.target);
      const duration = Number(el.dataset.duration) || 1500;
      const prefix = el.dataset.prefix || "";
      const suffix = el.dataset.suffix || "";
      const useDelimiter = el.dataset.delimiter !== undefined;
      const hasDecimal = target % 1 !== 0;
      const startTime = performance.now();

      const formatNumber = (num) => {
        if (useDelimiter) {
          return num.toLocaleString("de-DE", {
            minimumFractionDigits: hasDecimal ? 1 : 0,
            maximumFractionDigits: hasDecimal ? 1 : 0,
          });
        }
        return hasDecimal ? num.toFixed(1) : Math.floor(num);
      };

      const animate = (now) => {
        const progress = Math.min((now - startTime) / duration, 1);
        const currentRawValue = progress * target;
        el.textContent = `${prefix}${formatNumber(currentRawValue)}${suffix}`;
        if (progress < 1) {
          requestAnimationFrame(animate);
        } else {
          el.textContent = `${prefix}${formatNumber(target)}${suffix}`;
        }
      };

      requestAnimationFrame(animate);
      observer.unobserve(el);
    });
  });

  counters.forEach((counter) => observer.observe(counter));
};
```

## Component troubleshooting

**Slider not working:**

- Check Swiper JS/CSS loaded in correct order
- Verify swiper-wrapper contains swiper-slide children

**Animations not showing:**

- Ensure AOS.init() called after DOM loads
- Check data-aos attributes on elements

**Icons missing:**

- Verify Bootstrap Icons CSS loaded before custom CSS
- Check font files in assets/fonts/

Continue to **Pages & Sections** for page-specific customization, or **Deployment Guide** for hosting instructions.
