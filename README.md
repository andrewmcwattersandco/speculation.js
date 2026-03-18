# speculation.js

Perceptually instant speculative page navigation

## Usage

Add `speculation.js` before `</body>` on every page of your site:

```html
    <script src="/speculation.js"></script>
  </body>
</html>
```

No configuration, no API. Navigation becomes instant automatically.

On Chrome, the browser's native [Speculation Rules API][spec] prerenders
pages immediately. On all other browsers, pages are fetched and cached on
hover, mousedown, or touch — then swapped into the current document on
click without a full navigation.

[spec]: https://developer.chrome.com/docs/web-platform/prerender-pages

### Opting out

Add `data-no-speculate` to any link that should not be preloaded or
prerendered:

```html
<a href="/logout" data-no-speculate>Log out</a>
```

Links with `target`, `download`, or a cross-origin `href` are
automatically excluded.

### Cache behavior

The fetch-swap path respects your server's `Cache-Control` headers. Pages
marked `no-store` or `no-cache` are never cached. Pages with `max-age`
are cached for that duration. Pages with no cache headers are not cached,
matching default browser behavior.

### Data saver

On connections with `navigator.connection.saveData` set, hover preloading
is disabled. Mousedown and touch preloading still work since those
represent clear user intent.

## Prior Art

- [InstantClick](http://instantclick.io) — the original fetch-swap
  library, written in 2014 by Alexandre Dieulot. speculation.js is a
  ground-up rewrite informed by InstantClick's approach, updated for
  2026 browser capabilities.
- [Speculation Rules API][specrules] — the W3C spec that defines native
  browser prerendering, which speculation.js uses as its primary path on
  supported browsers.
- [Turbo Drive](https://turbo.hotwired.dev) — Basecamp's fetch-swap
  library, part of the Hotwire toolkit. Informed the `<head>` diffing
  approach used here.
- [Quicklink](https://getquick.link) — Google's link prefetching library,
  which uses `IntersectionObserver` and `<link rel="prefetch">` rather
  than fetch-swap.

[specrules]: https://wicg.github.io/nav-speculation/speculation-rules.html

## License

GNU General Public License v2.0
