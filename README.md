## Single Page Smooth Scrolling + Navbar Redirect

This project uses **smooth scrolling** to different sections on the same page when clicking navbar links.

### Final Result
- Clicking a nav link (e.g. "Features", "About") → smoothly scrolls to the corresponding section
- Navbar stays fixed → sections are not hidden under it when scrolled to
- Works on both desktop and mobile

### 1. HTML Structure (main JSX/App component)

Add unique `id` attributes to each major section:

```jsx
<div>
  <nav>
    <Navbar />
  </nav>

  <section id="home">
    <HeroPage />
  </section>

  <section id="how-it-work">
    <HowItWork />
  </section>

  <section id="feature">
    <PowerfullFeature />
  </section>

  <section id="transparency">
    <Transparency />
  </section>

  <section id="privacy-security">
    <PrivacyAndSecurity />
  </section>

  <section id="about">
    <AboutPage />
  </section>

  <section id="contact">
    <ContactPaage /> {/* ← typo? maybe ContactPage */}
  </section>

  <section id="get-started">
    <PlaystoreDownloadPage />
  </section>

  <section>
    <Footer />
  </section>
</div>
```

### 2. Navbar – Scroll Handler Function
Add this function inside your Navbar component (or in a custom hook):
```jsx
const scrollToSection = (event, href) => {
  if (!href.startsWith('#')) return;

  event.preventDefault();

  const target = document.querySelector(href);
  if (!target) return;

  target.scrollIntoView({
    behavior: 'smooth',
    block: 'start',
  });

  // Optional: close mobile menu if you have one
  setMenuOpen?.(false);
};
```

### 3. How to use it in Nav Links
```jsx
<a
  href="#feature"
  onClick={(e) => scrollToSection(e, "#feature")}
  className="text-gray-600 text-sm md:text-md lg:text-lg font-medium hover:text-blue-600 transition-colors duration-200"
>
  Features
</a>

<!-- Do the same for other links -->
<a href="#about" onClick={(e) => scrollToSection(e, "#about")}>About</a>
<a href="#contact" onClick={(e) => scrollToSection(e, "#contact")}>Contact</a>
```

### 4. Important CSS (global / tailwind / css file)
```jsx
/* 1. Enables smooth scrolling behavior (most modern browsers) */
html {
  scroll-behavior: smooth;
}

/* 2. Prevents sections from being hidden under fixed navbar */
section[id] {
  scroll-margin-top: 96px;   /* ← adjust this value = your navbar height */
  /* Common values: 80px, 96px, 100px, 5rem, etc. */
}
```




