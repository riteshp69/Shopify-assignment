\# Shopify Web Development Manager Assignment



\## Overview



Shopify theme implementation for the Web Development Manager technical assignment.



\## Test 1 — Landing Page



Test 1 is implemented as three independently reusable Shopify sections:



\- Hero

\- Drop Teaser

\- Display Text



Each section has its own Shopify schema and can be configured independently in the theme editor.



\## Test 2 — Product Card



Test 2 uses a reusable product-card snippet rendered from real Shopify product data inside a collection/product-grid section.



The card supports:



\- Colour swatches

\- Variant image switching

\- Variant-specific product links

\- AJAX quick add

\- Sold-out states

\- Compare-at pricing

\- Conditional vendor/state information

\- Clearance and Final Sale states

\- Products with different numbers of colour variants

\- Missing images

\- Long product titles



\## Responsive approach



The Figma specification is primarily desktop at 1440px.



The implementation uses:



\- Desktop: 901px and above

\- Tablet/mobile: below 901px

\- Small mobile: 480px and below



The Drop Teaser changes from its desktop two-column layout to a single-column layout below the desktop breakpoint. This prevents fixed desktop panel widths from causing horizontal overflow.



At small mobile widths, spacing and internal sizing are reduced where necessary while preserving the visual hierarchy and usability.



\## Typography



The Figma uses a script/accent treatment for prominent editorial copy. Pinyon Script is used as the script treatment.



General interface and body text use the theme's sans-serif font stack.



The script font is reserved for display/accent content rather than functional UI text.



\## Design decisions



\### Countdown



The Drop Teaser countdown uses a merchant-configurable target date and time and updates in real time. The completed state is handled rather than allowing the countdown to continue into negative values.



\### Drop Teaser image and caption



The image and overlay caption are kept as separate editable properties so the caption can be changed by the merchant.



\### Product states



Clearance and Final Sale are treated as product-data-driven states rather than being permanently displayed on every product card.



\### Vendor



The vendor line is conditional rather than being displayed as generic content on every card.



\### Variant selection



The selected variant is the source of truth for the card image, product URL and quick-add variant.



\## Accessibility



The implementation aims to provide:



\- Keyboard-accessible controls

\- Visible focus states

\- Meaningful image alt text

\- Sensible heading hierarchy

\- Accessible form labels

\- Reduced-motion handling



\## Shopify implementation



The implementation uses native Shopify theme architecture:



\- Liquid-driven product data

\- Shopify section schemas and presets

\- Shopify customer/newsletter form

\- Shopify cart AJAX behaviour

\- No jQuery

\- No CSS framework

\- No page-builder or section-builder app



\## Local development



```bash

shopify theme dev --store ocommerce-developer-assignment.myshopify.com

