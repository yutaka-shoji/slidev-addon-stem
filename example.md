---
theme: default
---

# slidev-addon-stem

Slidev addons for stem users.

---

# Component: `PlotlyFigure`

You can embed interactive Plotly figures in your slides!

<div grid="~ cols-2 gap-4">
<div>

```markdown
<PlotlyFigure
  src="/figure.json"
  caption="Figure N: Figure Caption."
  width="100%"
  height="320px"
  :fontSize="10"
/>
```

</div>
<div>

<PlotlyFigure
  src="/figure.json"
  caption="Figure N: Figure Caption."
  width="100%"
  height="320px"
  :fontSize="10"
/>

</div>
</div>

---

# Component: `ImageFigure`

Embed png/jpg with captions.

<div grid="~ cols-2 gap-4">
<div>

```markdown
<ImageFigure
  src="/figure.png"
  caption="Figure N: Figure Caption."
  width="100%"
  height="200px"
/>
```

</div>
<div>

<ImageFigure
  src="/figure.png"
  caption="Figure N: Figure Caption."
  width="100%"
  height="200px"
/>

</div>
</div>

---
layout: figure-side
figureUrl: /figure.png
figureCaption: "Figure N: Figure Caption."
---

::header::

# Layout: `figure-side`

Pre-defined layout with two columns, left for any content and right for the figure.

::content::

```markdown
---
layout: figure-side
figureUrl: /figure.png
figureCaption: "Figure N: Figure Caption."
---

::header::

# Title

Subtitle

::content::

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
```
