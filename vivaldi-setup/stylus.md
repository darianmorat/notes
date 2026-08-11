## Stylus - Scrollbars

```css
/* Everything: */
/* Remove scrollbars */
::-webkit-scrollbar {
   display: none !important;
}
* {
   scrollbar-width: none !important;
}
```

## Stylus - Websites

```css
/* URLs on the domain: github.com */
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

```css
/* URLs on the domain: duckduckgo.com */
/* Remove DDG logo, feedback popup and footer */
[data-testid="header-logo"],
[data-testid="feedback-prompt"],
.footer {
   display: none !important;
}
```
