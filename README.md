<!-- Heading -->
# HTML Webpack

<!-- Description -->
This is my own **boilerplate** in making Front End Projects. I'm currently using **Laravel Mix** and **Webpack**. 

## Installation
```
npm install
```

## Running the Command
```
npm run watch
```
### Default structure
This boilerplate default setup uses the id `#wrapper` to wrap the `#main` which contains the content and `footer` for site additional info.

<!-- Markup -->
```HTML
<div id="main">
  <div id="wrapper">
    <!-- Content Goes Here -->
  </div>

  <footer>
    <!--Footer info goes here  -->
  </footer>
</div>
```

I'm using flex to have a sticky footer at the bottom. 
Making `#wrapper` as the flex container, `#main` to have a flex 1 and `footer` to shrink.
If you want to make some edits, you may find this in `4-layout/default-structure.scss`.

## :package: Vendor Folder 

### :small_blue_diamond: **reset.scss**
Contains all the reset css codes that gets rid of the default styling of html.

### :small_blue_diamond: **themename.scss**
For setting the themename for your front end project, commonly used for the Wordpress engine to read the name of your theme.

### :small_blue_diamond: **variables.scss**
Setup variables for the theme's **colors**, **font weights** and **device breakpoints**.

#### I. Adding theme colors or font weights
To add **colors** or **font weights** you just need to add key a value pair inside the Colors or Font Weights list.

Example:

```SCSS
"white": #ffffff
```

```SCSS
$theme-defaults: (
  /* Colors */
  'Colors' : (
    "primary": #073763, 
    "accent": #E4572E,
    //Add more colors here
  ),

  // Font Weights
  'Font weights' :(
    'light': 300,
    'normal': 400,
    'bold': 700,
    //Add more weights here
  ),
  
);
```
#### II. Hex to RGB function
The variables folder also contains the function `hexToRGB()` to convert Hex color values to RGB.

```SCSS
@function hexToRGB($hex) {
  @return red($hex), green($hex), blue($hex);
}
```

#### III. Installing Bootstrap
Folder contains the importing of the Bootstrap framework to your boilerplate. To activate the framework just uncomment the line of code. 
```SCSS
//@import 'node_modules/bootstrap/scss/bootstrap';
```
Go to `styles.scss` and add this code to top part of the file.
```SCSS
@import '1-vendor/bootstrap';
```
##### :bangbang: Warning
Make sure to comment these files on `styles.scss` so it doesn't conflict with your own framework.

```SCSS
@import '3-framework/breakpoint.scss';
//@import '3-framework/grid.scss';
//@import '3-framework/spacing.scss';
//@import '3-framework/wrappers.scss';
```

## :package: Base Folder
Base folder groups Sass functions, mixins, placeholders and other base code to be declared in one file.
### :small_blue_diamond: **animations.scss**
All animation classes, transitions and keyframes should be declared here.
### :small_blue_diamond: **colors.scss**
Any color related functionalities here.
### :small_blue_diamond: **functions.scss**
Sass functions are declared here.
### :small_blue_diamond: **mixins.scss**
File for creating mixins.
### :small_blue_diamond: **placeholders.scss**
File for creating placeholders.
### :small_blue_diamond: **typography.scss**
File where you can declare sizes for default typographic tags.

#### Creating Typographic elements
You can also create typographic elements here by declaring the **class name** or **tag name** and inputting the values for **size**, **mobile-size** and **weight** inside the `$text-elements` array.

Mobile size of the element you declared is triggered at a *840 breakpoint*.
```SCSS
//Sample of creating a new typographic element
'.custom-class':(
    size:3rem,
    mobile-size:1.5rem,
    weight:var(--light)
  )
```

```SCSS
$text-elements: (
  'h1':(
    size:3rem,
    mobile-size:2rem,
    weight:var(--bold)
  ),
  '.custom-class':(
    size:3rem,
    mobile-size:1.5rem,
    weight:var(--light)
  ),
  
);
```
## :package: Framework Folder
Your own framework for grids and spacings.

### :small_blue_diamond: **grids.scss**
Grids give you Default column count is *12*, and breakpoints are declared in the `$grid-breakpoints` array.
You may change it in the code below

```SCSS
$columns: 12;
$grid-breakpoints: (
  default:0,
  sm:576px,
  md:767px,
  lg:979px,  
  xl:1200px
);
```

You may also generate *gutter sizes* by modifying the values below. 

```SCSS
$gutters: (5, 10, 15, 20);
```

### :small_blue_diamond: **spacings.scss**
Spacings returns a result of assorted padding and margin values. Returning a `rem` unit value
If you ever want to change the values, you can change them here under the `$spaceamounts` variable.

```SCSS
$spaceamounts: (0.5, 1, 1.5, 2, 3); // Adjust this to include the pixel amounts you need.

$sides: (top, bottom, left, right); // Leave this variable alone

```

### :small_blue_diamond: **spacings-10s.scss**
This file returns spacings also, but with increments of 10. Starting from **10** - **120**.

### :small_blue_diamond: **wrappers.scss**
This file contains the `container` class as copied from **Bootstrap** and a container generator that generates a classname with `1366px` of width.

To use the container generator, you just need to add
add the class name of what you want to the `$classes` array.

```SCSS
/* ===================== */
/* Container generator */
/* ===================== */
// Loop through these classes to have max-width of 1366px
// And response to 900 px if it's in Laptop Mode

  $classes: (hero, grid-container, grid__custom);
```

## :package: Layout Folder
This folder just organizes your css files by **HTML page** or **Section layout**. 

You can create your files here like this:

`sidebar.scss` or `about.scss`

## :package: Modules Folder
You create re-usable components here like **Buttons**, **Accordions** or **Tabs**.

## :package: Responsive Folder
Organizes your mobile responsive coding of a *section* or *page* here. 

You can also create files.

``` SCSS
@media #{$device-lg}{
  /* Insert code Desktop size here */

}

@media #{$device-md} {
 /* Insert code laptop size here */

}


@media #{$device-sm} {
 /* Insert code tablet size here */

}

@media #{$device-xs} {
 /* Insert code mobile size here */

}
```