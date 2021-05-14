## Why?

The current ADS (Bumblebee), despite attempts to mitigate, still suffers from slowness. This is due to several complicating factors:

- Outdated (require.js) module system
  - Only one bundling option, a mono-bundle -- without custom configurations (brittle)
  - Conceptually separates JS modules from other types of files (e.g. cannot load images, svg, etc. without plugins)
  - Bumblebee utilizes inline requires, making build-time bundling more difficult with modern tools
- Complex templating and rendering system (using Backbone.js)
  - Nested templates and dynamic rendering make it difficult to see what will be outputted
  - Bumblebee uses custom page rendering implementation, which works, but hard to debug and maintain
- Implementations causing memory leaks or other bugs creating slowness (especially on low-powered devices)
  - Large refactors needed to fix issues
- Complex client-side business logic
  - Several areas that have a large amount of logic which is performed client side, which could be offloaded to the server

Bumblebee also is a SPA (single page application), meaning it is completely rendered on the client device. This is fine in most cases, but hurts SEO and users that don't use JavaScript for some reason.

Development on Bumblebee is also complicated:

- Mixing of old and new frameworks/libraries
  - Difficult to maintain
  - Increases overall code weight
- Build system
  - Modules must be explictly processed and loaded
  - Developers are responsible for controlling all third-party libraries and how they are loaded, processed, and bundled
