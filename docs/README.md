# Nectar (RFC)

Experimental server-side rendered implementation of ADS

Github: https://github.com/adsabs/Nectar

Use the sidebar to navigate around.

## Need

Since its creation in 2014, Bumblebee's current front-end tech stack has gotten more and more outdated making it difficult to develop, debug and maintain.
The current design could be improved to address issues related to accessibilty and user experience. SEO is also difficult, with search engines being unable to properly index pages, and non-js scrapers/users unable to access most features.
Finally, speed is a common complaint from users, improvements are needed to increase performance.

### Performance

Lighthouse report as of 5/18/2021: https://lighthouse-dot-webdotdevsite.appspot.com//lh/html?url=https%3A%2F%2Fui.adsabs.harvard.edu

This report was done on an emulated mobile device.

Performance is real issue on less-capable devices.

- Lots of unused code is downloaded, even with optimized bundles.
  - More modern tools like tree-shaking aren't used
- Minification is

### Accessibility

### SEO

### UX

### DX
