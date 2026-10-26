# yizhiweb.top — 102 privacy-first browser tools

**Live site:** <https://yizhiweb.top/>

yizhiweb.top is a static collection of 102 online tools for text, data, developers,
images, dates and everyday calculations. Every tool runs entirely in the browser:
input and files are processed locally, there is no account system, and there is no
server-side processing.

This repository is the public project page. The site source is private; the live
site and its [methodology page](https://yizhiweb.top/methodology/) describe what is
tested and where the limits are.

## Why browser-only

Most online tools are thin wrappers around a server. That means your input leaves
your device, and the tool stops working when the backend does. This project takes
the opposite approach:

- **Nothing is uploaded.** Image, CSV, SVG, subtitle and file-hash tools read local
  files in the browser; encryption and hashing happen in the page.
- **No account, no server-side storage.** The site is static HTML/CSS/JS served by
  nginx.
- **The method is public.** Each engine has unit, property, oracle and real-browser
  tests. The methodology page explains the four layers and the known limits.

## What's inside

- **Text & encoding** — text counter (characters, words, graphemes), case converter,
  base64, URL encoding, HTML entities, Unicode/UTF-8 inspectors, Morse, Braille,
  NATO alphabet, transliteration, diacritics.
- **Developer** — JSON/YAML/TOML/XML conversion, SQL formatter, regex tester, JWT
  decoder, cron expression generator, IPv4 subnet calculator, TOTP, hashes/HMAC,
  text diff, CSV/JSON/table conversion.
- **Images & files** — compressor with a target-size search, resizer, cropper, format
  converter, watermark, EXIF reader, favicon/ICO, QR and barcode generators, SVG
  optimizer and rasterizer.
- **Calculators** — loan, compound interest, savings, margin/markup, ROI, break-even,
  commission, GPA, age, date difference, percentage, unit and number-base converters.
- **Design** — color converter, palette generator, contrast checker, CSS gradients,
  box shadows, border radius and triangles.

## How it is tested

A static tool has no server to catch mistakes, so the test suite is the backend:

1. **Unit tests** — pure engine functions, bundled with esbuild and run in Node.
2. **Property / fuzz tests** — round-trips, invariants and malformed input. Base64,
   URL encoding, hashing, CSV quoting, numeric formatting and similar engines are
   exercised with generated inputs.
3. **Oracle tests** — results are compared against an independent reference: Node's
   `crypto` for hashes/HMAC/AES-GCM, Node's `punycode` implementation, RFC 6238
   vectors for TOTP, and separate string-based implementations for subnet maths.
4. **Real-browser E2E** — Chrome clicks every control on every tool page, checks
   Copy buttons, empty/invalid states, keyboard paths and mobile layouts.

A coverage gate fails the build if a control or Copy button has no browser test.
The full workflow and the known limits are published at
<https://yizhiweb.top/methodology/>.

## Tech

- Astro with `output: 'static'`; no client framework.
- Pure TypeScript engines with zero runtime dependencies.
- Heavy modules (image processing, WASM, PDF) are loaded lazily, outside the base
  page bundle.
- A per-page JavaScript budget is enforced in CI.
- Deployed as static files behind nginx.

## Links

- Site: <https://yizhiweb.top/>
- All tools: <https://yizhiweb.top/tools/>
- Methodology: <https://yizhiweb.top/methodology/>
- Guides: <https://yizhiweb.top/guides/>

## Status

Live and actively maintained. The public roadmap is about indexing, content depth
and real usage, not page count: the site already has 162 content pages and the next
milestone is getting them crawled and read.

## License

The site content and brand are © yizhiweb.top. This repository contains the public
project description only; no source code is licensed here.
