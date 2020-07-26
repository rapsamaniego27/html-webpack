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

## Vendor Folder

### **reset.scss**
Contains all the reset css codes that gets rid of the default styling of html.

### **themename.scss**
For setting the themename for your front end project, commonly used for the Wordpress engine to read the name of your theme.

### **variables.scss**
Setup variables for the theme's **colors**, **font weights** and **device breakpoints**.

#### I. Adding colors
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