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

# :floppy_disk: DIST Files
The **dist** folder contains all the precompiled assets handled by webpack after running the `npm run watch` command. If you want to make changes in your directory and compilation settings. You go to `webpack.mix.js`.

## :package: app.js
Compiles all the javacsript files here. 
## :package: style.min.css
Compiles all the scss files here.

# :lipstick: SCSS Files

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
These generate font variables for you to use in your CSS. 
```CSS
:root {
  /*Colors */
  --primary: #073763 ;
  --accent: #E4572E ;
  --success: #9FD356 ;
  --black: #111111 ;
  --light: #ffffff ;
  --green: #228B22 ;
  /*Font weights */
  --light: 300 ;
  --normal: 400 ;
  --bold: 700 ;
}
```

To call them use the var css function and insert a parameter containing the variable. 
```CSS
var(--primary)
var(--bold)
```

If the css property for colors does not work try the color function I made.

```SCSS
color('success');
color('dark');
```

#### :computer: **Colors in the frontend**
You may use the colors you just setup in SASS by calling its class name `hex-` followed by the color name.

Example:
```HTML
<p class="hex-primary">I'm a primary color</p>
<p class="hex-white">I'm a white color</p>
<p class="hex-accent">I'm an accent color</p>
```

#### II. Hex to RGB function
The variables folder also contains the function `hexToRGB()` to convert Hex color values to RGB.

```SCSS
@function hexToRGB($hex) {
  @return red($hex), green($hex), blue($hex);
}
```

This will generate font variables like these:
```CSS
:root{
  --primary-rgb: 7, 55, 99;
  --success-rgb: 159, 211, 86;
  --white-rgb: 255, 255, 255;
  --green-rgb: 34, 139, 34;
}
```

Now everytime you want to use the color by manipulating its opacity you can just call it like this.


```CSS
.class{
  background:rgba(var(--primary-rgb), 0.5);
  background:rgba(var(--success-rgb), 0.5);
  background:rgba(var(--green-rgb), 0.5);
  background:rgba(var(--white-rgb), 0.5);
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
#### :computer: **Rem function in the CSS**

```SCSS
  h1{
    font-size: rem(24); //1.5rem (24px)
  }
```

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

#### Creating a triangle
In creating a triangle, you need to pass 4 arguments.
* **size** of the triangle 
* which **side** of the triangle you want it to point to
* position on the **left** side
* position on the **top** side
* **color** of the triangle

You use this like this.
`top`, `left`, and `color` can be empty values.
```SCSS
.important{
  color:#000000;
  @include triangulate(1rem, left, $left: -4rem, $color: blue);
}
```

#### :computer: **Typography in the frontend**
Sample code in displaying your custom text classes in HTML

```HTML
    <div class="head4">This is heading 4</div>
    <div class="head3">This is heading 3</div>
    <div class="head2">This is heading 2</div>
    <div class="head1">This is heading 1</div>
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

#### :computer: **Grids in the frontend**
The `grid__custom` is the class you generated in the Container generator, giving it a `container__flex` class which gives makes the class to be a flex display.

As you see, the grid system works like **Bootstrap** the only difference is that grid classes are named `col-md3` instead of `col-md-3`.

The sample below shows 4 columns with a division of 3 fractured lengths of the *12 column grid system.*

As it responds to mobile and tablet making it 2 columns then 1.

Note: Col classes with sizes like `md` or `lg` or etc., are read first before col only classes.
 
```HTML
<div class="grid__custom mt-1 container__flex">
  <!-- 1st DIV -->
 <div class="col-lg3 col-md6 col-sm3 grid__custom__content">
    <h3>Col LG 3 </h3>
    <div class="gut-15">
      <p>
        cols Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsa nobis obcaecati.
      </p>
    </div>
  </div>
  <!-- 2nd DIV -->
  <div class="col-lg3 col-md6 col-sm3 grid__custom__content">
    <h3>Col LG 3 </h3>
    <div class="gut-15">
      <p>
        cols Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsa nobis obcaecati.
      </p>
    </div>
  </div>
  <!-- 3rd Duv -->
  <div class="col-lg3 col-md6 col-sm3 grid__custom__content">
    <h3>Col LG 3 </h3>
    <div class="gut-15">
      <p>
        cols Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsa nobis obcaecati.
      </p>
    </div>
  </div>  
  <!-- 4th Div -->
  <div class="col-lg3 col-md6 col-sm3 grid__custom__content">
    <h3>Col LG 3 </h3>
    <div class="gut-15">
      <p>
        cols Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsa nobis obcaecati.
      </p>
    </div>
  </div>  
</div>
```

To input paddings around it you simply type in the word `gutter` followed by how much spacing you want.

```HTML
<div class="gut-5"></div>
<div class="gut-10"></div>
```

### :small_blue_diamond: **spacings.scss**
Spacings returns a result of assorted padding and margin values. Returning a `rem` unit value
If you ever want to change the values, you can change them here under the `$spaceamounts` variable.


```SCSS
$spaceamounts: (0.5, 1, 1.5, 2, 3); // Adjust this to include the pixel amounts you need.

$sides: (top, bottom, left, right); // Leave this variable alone

```

#### :computer: **Paddings and Margins in the frontend**
To call a padding or margin size in the front end. 
The convention starts with the:

1. type of spacing `m` or `p`
2. position `t`, `l` `r` or `b`
3. space amount from **1** to **5**.

Example:
```HTML
<!-- Padding Top -->
<div class="pt-1"></div>
<div class="pt-2"></div>
<div class="pt-3"></div>

<!-- Margin Bottom -->
<div class="mb-4"></div>
<div class="mb-5"></div>
```


### :small_blue_diamond: **spacings-10s.scss**
This file returns spacings also, but with increments of 10. Starting from **10** - **120**. 

It also includes breakpoint by calling the screensize acronym.

#### :computer: **Larger spacings in the frontend**
To call a larger padding or margin size in the front end. 
The convention starts with the:

1. type of spacing `m` or `p`
2. position `t`, `l`, `r` or `b`
2. breakpoint `xs`, `sm`, `md`, `lg` or nothing at all'.
4. space amount divisible by 10 from **10** to **120**.

Example:

```HTML

<!--A margin top of 90px that shrinks to 20px when in mobile -->
<div class="mt-90 mt-xs-20"></div>

<!-- A padding left of 60px on Laptop, shrinks to 30px on tablets  -->
<div class="pl-md-60 pl-sm-30"></div>

<!-- You can even use zero margins as long as you put two zero digits-->
<div class="mt-md-00"></div>
```

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
### :small_blue_diamond: **layout.scss**
This file contains pre-made display elements.

The available layouts: 

* `.layout-block`
* `.layout-inline`
* `.layout-inline-block`
* `.layout-flex`
* `.layout-grid`
* `.layout-table`
* `.layout-none`

```CSS
/* Basic layout */
.layout-block{
 display:block;
}

/* Layout with centering position */
/* This is also available for flex and absolute */
.layout-block__center{
 margin-left: auto;
 margin-right: auto;
 width: 50%;
 display: block;
}
```

#### :computer: **Layouts in the frontend**

```HTML
<div class="layout-block"> Element here ... </div>
```

You can also use it in responsive mode for example:

```HTML
<div class="layout-sm-block"> Element here ... </div>
<div class="layout-md-block"> Element here ... </div>
<div class="layout-lg-block"> Element here ... </div>
<div class="layout-xl-block"> Element here ... </div>
```

Now let's talk about flexes, you can use vertical or horizontal alignment and set it like this.

**Horizontal**:
* `.flex-h__start`
* `.flex-h__end`
* `.flex-h__center`
* `.flex-h__space-around`
* `.flex-h__space-between`
* `.flex-h__space-evenly`

**Vertical**:
* `.flex-v__start`
* `.flex-v__end`
* `.flex-v__center`
* `.flex-v__baseline`
* `.flex-v__stretch`

To make it display depending on the device width simply add the breakpoints **md**, **sm**, **lg** or **xl** in the middle of the class like this.

* `.flex-h-sm__space-around`
* `.flex-h-md__space-around`
* `.flex-h-lg__space-around`
* `.flex-h-xl__space-around`

#### :computer: **Wrappers in the frontend**
```HTML
<div class="hero"></div>

<div class="grid-container"></div>

<div class="container"></div>
```

## :package: Layout Folder
This folder just organizes your css files by **HTML page** or **Section layout**. 

You can create your files here like this:

`sidebar.scss` or `about.scss`

## :package: Modules Folder
You create re-usable components here like **Buttons**, **Accordions** or **Tabs**.

### :small_blue_diamond: **modal.scss**
This is a ready made basic modal for use.

* `.modal` is the parent container of the modal. 
* `.modal-close` is the close button.
* `.modal-guts` is the inner layer of the modal.
* `.modal-overlay` is located outside and just beside the modal, making sure its z-index is lower so that modal would stay upfront.
* `.modal--hide` is the modifier to have modal be hidden from the front end.
#### :computer: **Modal in the frontend**

```HTML
 <!-- Modal -->
      <div class="modal" id="modal">
        <a href="#" target="_blank" class="modal-close" id="modalClose">
          <i class="fas fa-times fa-2x"></i>
        </a>
        <!-- Modal Guts -->
        <div class="modal-guts">
          <div class="modal-content">
            <h3 id="bandName">Rap's Biography</h3>
            <p id="bandBio">
              Rap started to play the guitar at age 12. He started listening to New wave, Alternative and Punk music, which lead him to form his 1st band in High School. As he stepped into College, he joined a Pop/OPM band called 29th OF FEBRUARY where they won 3rd place in the 2015 SESSIONISTAS (Tiendesitas) and became Champion in the 2016 BAND CLASH (Trinity
              University).
              <br><br>
              Inspired by his musician uncles in Hong Kong, he dedicated his life into forming this Acoustic band, hoping to show the audiences the greatness of Folk, Country and Rock N Roll music. Aside from the Guitar, he also enjoys playing the Violin, DOTA and watch Comedic movies in his past time. He currently works for StraightArrow Corporation as a
              Web Specialist.
            </p>
          </div>
        </div>
      </div>
      
      <!-- Modal Overlay -->
      <div class="modal-overlay" id="modalOverlay">
      </div>
```

## :package: Responsive Folder
Organizes your mobile responsive coding of a *section* or *page* here. 

You can also create files here.

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

# :space_invader: JS Files
## :package: Classes Folder
Folder to store all your Javascript Classes.
## :package: Components Folder
Final output of your component, files where you can run javascript code thats not inside a class.
## :package: Misc Folder
Optional Folder, where you can put miscellaneous codes.
## :package: Vendors Folder
Folder where you put 3rd party javascript code or libraries.