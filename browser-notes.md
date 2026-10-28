## Fonts

- Standar font: Inter Display
- Serif font: Noto Serif
- Sans-serif font: Inter Display
- Fixed-width font: Noto Sans Mono
- Mathematical font: Noto Sans Math

## Extensions

- Bitwarden PM
- Dark Reader
- DeArrow
- DuckDuckGo
- GoFullPage
- Mouse Pinch-To-Zoom
- Return YouTube Dislike
- Reverso Context
- Shazam
- SponsorBlock YouTube
- Stylus
- uBlock Origin
- Unhook Youtube
- Vimium C

> Stylus - Configuration

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

> Vimium C - Configuration

- Custom Key Mappings

```
map <f1> Vomnibar.activate
map <f2> Vomnibar.activateInNewTab
mapKey <f4> <c-[>
map v LinkHints.activateSelect

unmap r
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
   font-family: "Inter Display" !important;
}

body {
   margin: 9px auto 10px;
   width: min(650px, calc(100vw - 40px));
   border: 1px solid rgba(128, 128, 128, 1) !important;
}

#input {
   font-size: 18px !important;
}
```
