## TITLE: Extensions

- Bitwarden PM
- Dark Reader
- DeArrow
- DuckDuckGo
- GoFullPage
- Mouse Pinch-To-Zoom
- PDF Viewer [pending check]
- Return YouTube Dislike
- Reverso Context
- Shazam
- SponsorBlock YouTube
- Stylus
- uBlock Origin
- Unhook Youtube
- Vimium C

## TITLE: Stylus

- Websites:

```
/* Everything */
/* ========== */

/* Make scrollbar thinner */
* {
   scrollbar-width: thin;
}
```

```
/* URLs on the domain: github.com */
/* ============================== */

/* Fix avatar position & status badge */
.js-profile-editable-replace {
   margin-top: -7.5px;
}
.user-status-circle-badge {
   display: none !important;
}

/* Remove contributions section */
.js-yearly-contributions,
#year-list-container {
   display: none !important;
}
.col-lg-10 {
   width: 100% !important;
   max-width: 100% !important;
}
h2.f4.text-normal.tmp-mt-4.tmp-mb-3 {
   margin-top: 0 !important;
}
h2.f4.mb-2.text-normal {
   margin-top: 27px !important;
}
```

```
/* URLs on the domain: duckduckgo.com */
/* ================================== */

/* Remove DDG logo, feedback popup and footer */
[data-testid="header-logo"],
[data-testid="feedback-prompt"],
.footer {
   display: none !important;
}
```

## TITLE: Vimium C

- Custom Key Mappings

```
map v LinkHints.activateSelect
mapkey <c-e> <c-[>
```

- Custom CSS UI

```
/* #omni */
*,
*::before,
*::after,
[style*="border-radius"],
[class*="rounded"] {
   border-radius: 0 !important;
   box-shadow: none !important;
   font: 11pt Inter !important;
}

body {
   margin: 9px auto 10px;
   width: min(650px, calc(100vw - 40px));
   color: #ffffffcc;
}

body::after {
   border: 1px solid #323232;
}

match {
   color: #FFFFFF;
   font-weight: 600 !important;
}

.title > match {
   text-decoration: none;
}

#bar {
   background-color: #323232;
   border-bottom: 1px solid #323232;
}

#input {
   background-color: #171717;
   color: #ffffffcc;
   border: none;
}

#list {
   background: #171717;
}

.item {
   border: none;
   border-bottom: 1px solid #323232;
}

.item:hover {
   background-color: #1b324f80;
   border: none;
}

.item.s {
   background-color: #1b324f;
   color: #ffffff;
   border: none;
}

#toolbar {
   display: none;
}
```
