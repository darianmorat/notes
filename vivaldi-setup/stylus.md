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
/* URLs on the domain: */
/* youtube.com - github.com - google.com - claude.ai - chatgpt.com - duckduckgo.com */
/* No rounded borders */
*,
*::before,
*::after,
[style*="border-radius"],
[class*="rounded"] {
   border-radius: 0 !important;
}

/* Restore rounded items */
[class*="avatar"],
img.avatar,
img.avatar-user,

/* Youtube */
.ytd-topbar-menu-button-renderer,
.ytd-active-account-header-renderer img,
.ytd-comment-simplebox-renderer img,
.ytd-video-owner-renderer img,
.ytd-comment-replies-renderer img,
.ytd-comment-view-model img,
.ytp-scrubber-button,
.ytd-creator-heart-renderer,

/* Github */
.prc-Avatar-Avatar-0xaUi,
.TimelineItem-badge,
.repo-language-color,

/* Google */
[aria-label*="Google Account"] img,
img[src*="googleusercontent.com/a/"],
.gb_be::after {
   border-radius: 50% !important;
   border: none !important;
   box-shadow: none !important;
}

/* =================================================================================== */
/* URLs on the domain: youtube.com */
/* Remove channel avatar from titles */
.ytLockupMetadataViewModelAvatar {
   display: none !important;
}

/* =================================================================================== */
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

/* =================================================================================== */
/* URLs on the domain: chatgpt.com */
/* Restore rounded items */
div:has(> img[alt="Profile image"]),
div.rounded-full.h-2.w-2 {
   border-radius: 50% !important;
   overflow: hidden !important;
}

/* =================================================================================== */
/* URLs on the domain: duckduckgo.com */
/* Remove DDG logo, feedback popup and footer */
[data-testid="header-logo"],
[data-testid="feedback-prompt"],
.footer {
   display: none !important;
}
```
