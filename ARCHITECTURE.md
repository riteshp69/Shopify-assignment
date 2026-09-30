# Architecture Note

## 1. Section structure

The implementation keeps Test 1 as three independent Shopify sections: Hero, Drop Teaser, and Display Text. Each section owns its own merchant-facing settings, Liquid markup, CSS, and JavaScript behaviour so that sections can be added, removed, reordered, or reused independently in the theme editor.

Test 2 is split into a collection/product-grid section and a reusable product-card snippet. The grid is responsible for selecting and iterating over real Shopify products, while the card is responsible for rendering a single product, its variants, swatches, states, links, and quick-add behaviour. This separation allows the product card to be rendered from other collection/grid contexts without tying its markup to one specific page.

Real Shopify data is preferred wherever it exists: products, variants, images, prices, compare-at prices, inventory state, and vendor data. Presentation-specific settings remain in section schemas so merchants can configure the experience without editing code.

## 2. Conventions for a three-person team

I would standardise the theme around a predictable separation between sections, snippets, assets, and shared theme configuration.

- `sections/` contains independently addable Shopify sections.
- `snippets/` contains reusable UI fragments such as product cards.
- `assets/` contains section-specific JavaScript/CSS and other static assets.
- `config/` and `locales/` remain responsible for theme configuration and translation data.

Section and snippet names should use a consistent descriptive prefix for assignment-specific components. CSS should be scoped to the component root rather than relying on broad global selectors. JavaScript should initialise from a section root and use `data-*` attributes for section-specific state instead of relying on global IDs or assumptions about page order.

For parallel development, each component should own its markup, styles and behaviour as much as practical. Shared utilities should only be introduced when the same behaviour is genuinely used by multiple components. This reduces merge conflicts and makes it possible for developers to work on separate sections without modifying a shared monolithic stylesheet or script.

All merchant-facing settings should use names that describe their purpose rather than implementation details. Liquid should remain responsible for server-rendered product data, while JavaScript should enhance interaction such as variant selection, countdown updates, and asynchronous cart actions.

## 3. Design/implementation push-back

The first point I would clarify before development is the responsive behaviour because the Figma is primarily a desktop specification. I would establish explicit mobile and tablet rules before implementation rather than allowing desktop dimensions to collapse unpredictably.

I would also clarify image ownership in the Drop Teaser. The image, overlay caption, and headline/lockup should be separate merchant-editable properties where possible. This avoids baking editable text into an exported image and prevents duplicated text when an exported frame already contains typography.

For the product card, I would define the source of truth for state labels such as Clearance and Final Sale before implementation. These states should come from documented product/variant data conventions rather than visual or price heuristics that merchants cannot understand.

Finally, I would confirm the expected behaviour when a countdown reaches zero and when a selected variant becomes unavailable. Explicit state definitions make the implementation predictable and avoid silently leaving the interface in an invalid state.

The overall approach is deliberately componentised: sections own page-level configuration, snippets own reusable UI, Liquid owns real Shopify data, and JavaScript provides progressive enhancement for interactive behaviour.
