# TailwindCSS

## Install

```sh
npm i -D tailwindcss postcss autoprefixer prettier prettier-plugin-tailwindcss
npx tailwindcss init -p
```

Create `./src/app/globals.css`
```CSS
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Import into Root Layout:
```TypeScript
import "./globals.css";
```

Create `.prettierrc`
```JSON
{
  "plugins": ["prettier-plugin-tailwindcss"]
}
```

## Utilities
Utilities I do forgot to use.
### container
- A component for fixing an element's width to the current breakpoint
- [docs](https://tailwindcss.com/docs/container)
```HTML
<!-- center container with padding on sides -->
<div className="container mx-auto px-2"></div>
```

### divide
- Utilities for controlling the border width between elements
- [width](https://tailwindcss.com/docs/divide-width), [color](https://tailwindcss.com/docs/divide-color), [style](https://tailwindcss.com/docs/divide-style)
```HTML
<!-- border with color and style for all children -->
<div className="divide-x-2 divide-slate-500 divide-dotted">
  <div></div>
  <div></div>
  <div></div>
</div>
```

### space
- Utilities for controlling the space between child elements (when not using flex or grid)
- [docs](https://tailwindcss.com/docs/space)
```HTML
<!-- add space between children -->
<div className="space-x-2">
  <div></div>
  <div></div>
  <div></div>
</div>
```

### line-clamp
- Utilities for clamping text to a specific number of lines
- [docs](https://tailwindcss.com/docs/line-clamp)
```HTML
<!-- clamp to 3 lines -->
<div className="line-clamp-3">
  Lorem ipsum ...
</div>
```

### truncate
- Prevent text from wrapping (similar to line-clamp-1)
- [docs](https://tailwindcss.com/docs/text-overflow#truncate)
```HTML
<!-- clamp to 1 lines, truncate overflowing text -->
<div className="truncate">
  Lorem ipsum ...
</div>
```

### form styling
- [accent-color](https://tailwindcss.com/docs/accent-color): for controlling the accented color of a form control
- [caret-color](https://tailwindcss.com/docs/caret-color): for controlling the color of the text input cursor
- outline: [width](https://tailwindcss.com/docs/outline-width), [color](https://tailwindcss.com/docs/outline-color), [style](https://tailwindcss.com/docs/outline-style)
- ring: [width](https://tailwindcss.com/docs/ring-width), [color](https://tailwindcss.com/docs/ring-color)

