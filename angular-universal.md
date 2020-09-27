# Server-side rendering (SSR) with Angular Universal

## Intro
- A normal Angular application executes in the browser, rendering pages in the DOM in response to user actions.
- **Angular Universal** executes on the server, generating static application pages that later get bootstrapped on the client.

## Why angular universal

### 1. SEO

### 2. Social Media Crawlers

## When to use Static Pre-Rendering
- Your application itself is rather Static.
(or at least the Routes you’re trying to pre-render)
For example: homepage | about us | contact us
- Your application doesn’t update very often.
Whenever some changes are needed on the static routes, you can simply run the build script again and republish the /dist folder containing all of your pre-rendered files.
## When to use Dynamic SSR
- Your application (and the routes you need to SSR) are very dynamic 
- You have a list of “trending products” | “live data” | etc, that you need populated correctly for every server-side render.
- Your applications structure is rendered based on JSON files or a CMS where anything could change at any given moment.
## References
- Universal starter: https://github.com/angular/universal-starter
- What is angular universal: https://blog.angular-university.io/angular-universal/
- Anguar Universal deep dive: http://medium.com/@MarkPieszak/angular-universal-server-side-rendering-deep-dive-dc442a6be7b7#:~:text=Angular%20Universal%20is%20the%20process,-side%20rendering%20(CSR).
