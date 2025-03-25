
___
```SCSS
body::-webkit-scrollbar {
  width: 12px;               /* ширина scrollbar */
}
body::-webkit-scrollbar-track {
  background: orange;        /* цвет дорожки */
}
body::-webkit-scrollbar-thumb {
  background-color: blue;    /* цвет плашки */
  border-radius: 20px;       /* закругления плашки */
  border: 3px solid orange;  /* padding вокруг плашки */
}
```

```SCSS
.root::-webkit-scrollbar {
  @apply w-3;
}
.root::-webkit-scrollbar-track {
  @apply bg-light-black-2;
}
.root::-webkit-scrollbar-thumb {
  @apply bg-primary rounded-2xl;
}

.posts {
  @apply flex flex-col gap-4;
}

```