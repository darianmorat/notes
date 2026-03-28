<!-- ================================================================================ -->
<!-- Custom Key Mappings -->
<!-- ================================================================================ -->

```vim
map v LinkHints.activateSelect
mapkey <c-e> <c-[>
```

<!-- ================================================================================ -->
<!-- Custom CSS UI -->
<!-- ================================================================================ -->

```css
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
   color: #ffffff;
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
