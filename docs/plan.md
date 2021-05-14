# Plan

A rewrite of the current application to take advantage of modern tools/frameworks and to fix the issues present in Bumblebee.
In some cases, we get improvements automatically just by utilizing modern tools, but we'll mention our choices.

### Module system

We propose to use `Webpack` as our module module bundler of choice. It is battle-tested and supports several types of module systems automatically. As opposed to `Rollup` or `Parcel`, `Webpack` is more configuration-heavy, but most of that is hidden by the framework. `Webpack`, and any of the other bundlers provide some great benefits over require.js.

### User Interface

We propose using `React` for developing the user interface.

### Language

`TypeScript` is our candidate as the programming language to use to develop the new user interface. The language, maintained by Microsoft, extends JavaScript by adding types, which can save time catching errors and providing fixes with tools such as IDE IntelliSense or linters before running the code.

Pros:

- Type checking ensures code consistency
- The development tooling is better given that it can rely on the types to make suggestions (less time looking for API documentation)
- Types can expose certain errors at development time or compile time
- Access to latest language features (e.g., ES7 JavaScript)

Cons:

- Steep learning curve
- It costs time up front
- Occasionally type definition modules are unavailable, inaccurate, or out of date for third party libraries

### SSR

We propose a hybrid approach to hopefully get the best of both worlds. Utilizing server-side rendered (SSR) static templates which become SPA-like pages when loaded on the client.

Next.js is our candidate as the (typescript ready) front-end development web framework. It enables server-side rendering (SSR) for React based web applications.

Pros:

- It is an opinionated framework
- It has its own file-based route
- It does SSR out of the box.
- Quick to get up and running
- Good documentation, community and well supported by the team
- It doesn’t create a big static bundle, thus pages are lighter weight and faster to load

Cons:

- It is an opinionated framework
- Harder to use a different router
- Harder to integrate with redux (but doable: example)

Next.js has a file-system based router, when a file is added to the pages/ directory it's automatically available as a route. For instance, pages/abs/[id] would match https://ui.adsabs.harvard.edu/abs/2021ApJ...908....4V.

#### Why SSR? Why not SPA

It is the case that the JS community began implementing server-side rendered (hybrid) pages to solve the SEO problem with SPAs. That is the main driving force behind this change; especially with non-js users making up such a small minority.

I believe that using a framework, such as Next.js, provides several advantages you don't automatically get with using a templated approach -- such as Django.

- Same language (JS) on both server and client
- Routing is baked in
- Provides bundling and code-splitting (via webpack config) based on pages
- Dynamic imports (auto splits)
- Tools like PostCSS can extract only the CSS you actually use per page, cutting down on page weight

One of the reasons people love SPAs is the transition between pages, which is seamless and feels like a native application. Using an SSR setup however, we get flashes of white between pages, since they need to be pulled from the server each time.

This is still the case with Next.js, however there are always ways around it. We can use rewrites to create mini-SPAs -- like dashboards or small sub-apps.
see: https://colinhacks.com/essays/building-a-spa-with-nextjs

I don't think SPA makes sense for this application. It adds unnecessary complexity to the client like handling routing.
