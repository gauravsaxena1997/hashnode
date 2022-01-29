## Create a Custom Angular Material Theme

Angular Material's theming system lets us customize color and typography styles for components in our Angular applications. Angular Material's theming APIs are built with Sass. Sass is a superset of CSS. It let us define variables etc which later compile to plain CSS.

### Palettes

Palette is a collection of colors with similar shades. We can make our own Palette too but for this tutorial, we will use a pre-built color palette. We can check them [here](https://material.io/archive/guidelines/style/color.html#color-color-palette).

### Themes

A theme is a collection of color and typography options. It primarily consists of three main color palettes.
- A **primary** palette for the color that appears most frequently throughout our application
- An **accent**, or secondary, the palette is used to selectively highlight key parts of your UI.
- A **warn**, or error, the palette used for warnings and error states.

We can make our custom theme with SASS. We can use a light or dark theme or both with a button toggle. Let's create a new file under `src/` folder named `custom-theme.scss`. And update it with this content.

```
// Include Material
@use '@angular/material' as mat;

// Add the core mixin (Mixin is a SASS feature)
@include mat.core();

// Create three different variables for primary, accent and warn for light theme
$light-primary: mat.define-palette(mat.$indigo-palette);
$light-accent: mat.define-palette(mat.$pink-palette);
$light-warn: mat.define-palette(mat.$red-palette);

// Define a light theme with define-light-theme function and pass our variables
$light-theme: mat.define-light-theme((
  color: (
    primary: $light-primary,
    accent: $light-accent,
    warn: $light-warn
  )
));

// Similarly, Define a dark theme
$dark-primary: mat.define-palette(mat.$pink-palette);
$dark-accent: mat.define-palette(mat.$blue-gray-palette);
$dark-warn: mat.define-palette(mat.$red-palette);
$dark-theme: mat.define-dark-theme((
  color: (
    primary: $dark-primary,
    accent: $dark-accent,
    warn: $dark-warn
  )
));

// Apply the mentioned theme on all app components
@include mat.all-component-themes($dark-theme);
```

The file is self-explanatory. We define our color palettes and define a Dark and Light theme. For now, we apply the Dark theme which will auto-apply to all our components. But this works automatically.

In the last tutorial, we saw that Angular Material adds a stylesheet in the `angular.json` file which is an in-built theme. So what we need to do is remove that and add this custom theme instead.

```
            ...
            "styles": [
              "src/custom-theme.scss",
              "src/styles.scss"
            ],
            ...
```

Now, let's add some CSS and classes so our dark theme color i.e. dark background, etc will appear on the whole page.

Go to `app.component.html` and replace the content with the following.
```
<div class="mat-typography app-frame mat-app-background container">
    <mat-slider aria-label="unit(s)"></mat-slider>
</div>
```

Then, move `app.component.scss` and add these classes.
```
html, body, app-root, .app-frame {
  overflow: hidden;
  margin: 0;
  min-height: 100vh;
  height: auto;
  box-sizing: border-box;
  color: #e0e0e0;
}

.container{
  min-height: 100vh;
}
```

We need to restart our Angular server since made some changes in the `angular.json` file. Terminate the current server instance and again hit `ng s -o` on the terminal.

You should see the background gets dark and our Slider color is also changed. That's because Slider uses *accent* color by default. So the color we defined in the dark theme accent will appear here. With Angular Material, the benefit is we can now use any other we define like primary color or warn. Just need to add the `color` attribute in the Slider component inside our template.
```
<mat-slider color="primary" aria-label="unit(s)"></mat-slider>
```

Now it should adept the primary color, we can use `warn` too if we want.

That's enough for our Material setup. Let's move back to learning more about Angular.

***
Previous Blog [Integrating Angular Material as a Module](https://gauravsaxena.hashnode.dev/integrating-angular-material)

Next blog Coming soon...