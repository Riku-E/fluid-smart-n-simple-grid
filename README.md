# Fluid Smart 'N Simple Grid
Smart, light, easily customisable responsive grid – SASS configuration.


## To develop
Load the repository to your local environment. 

To watch sass file modifications run;

`$ sass --watch --scss --sourcemap ./src/style.scss:./example/style.css`

In the root of the folder.

## Folder structure
```
./ 
|- README.md
|- LICENSE 
|
|– example/ 
|   |– index.html              			# HTML Structure example
|   |– style.css               			# Complided css from scss folder
|   |– style.css.map           			# Automatically generated mapping file from scss
| 
|– src/ 
|   – style.scss             			# Main file that combines the helpers, and grid together
|
|	|– helpers/ 
|	|   |– functions.scss      			# Contains function to calculate width of elements for given column count
|	|   |– grid-configurations.scss     # Settings for grid; Breakpoints, how many columns for each break point, prefix, spacing, max-width
|	|   |– placeholder.scss             # Common styles for more than 1 element
|	|   
|	|– layout/   
|	|   |– grid.scss              		# Pulls the configuration file and builds the grid based on it
```

## Simple grid settings

Open _grid-configurations.scss_ if here you can see following code;

```sass
// Grid confs
$grid-prefix: col !default;

$grid-spacing:1%;
$gird-max-width: 1240px;

$gird-break-to-eight: 40em;
$gird-break-to-twelve: 60em;

$grid-col-count-plus-breakpoints: (
    4:  '(max-width: #{$gird-break-to-eight})', 
    8:  '(min-width: #{$gird-break-to-eight}) and (max-width: #{$gird-break-to-twelve})',
    12: '(min-width: #{$gird-break-to-twelve})'
)
```

Grid prefix is the string that every class name will start with.

Grid spacing means the gutter between grid items. Each element have gutter on left and right side so its the gridspacing * 2.

Grid max width is the width grid will stop expanding, you can easily override this by changing the *row* to *row-full*

`$gird-break-to-eight: 40em;` Is just here to make the updating of media queries faster and simplier
`$gird-break-to-twelve: 60em;` Same as above


`$grid-col-count-plus-breakpoints`
Is setup for the value on the left the "key" is the amount of columns you want to display and its value (the media query) is the rule when it should be displayed.

In my example I show 4 columns until 40em, then 8 between 40 and 60em and after 60em user will get 12 column grid. You can easily add just new keys and new media queries to display X amount of grid at X screensize. The _functions.scss_ has function to calculate the width for elements for any column amount.

## HTML

```html

<!-- To make this full with you can change "row" to "row-full" -->
<div class="row"> 
    <div class="col-1-12 col-2-8 col-2-4">#1</div>
    <div class="col-1-12 col-2-8 col-2-4">#2</div>
    <div class="col-1-12 col-1-8 col-3-4">#3</div>
    <div class="col-1-12 col-2-8 col-1-4">#4</div>
    <div class="col-1-12 col-1-8">#5</div>
    <div class="col-1-12 col-2-8 col-1-4">#6</div>
    <div class="col-1-12 col-2-8 col-3-4">#7</div>
    <div class="col-1-12 col-1-8 col-1-4">#8</div>
    <div class="col-1-12 col-3-8 col-1-4">#9</div>
    <div class="col-1-12 col-3-8 col-2-4">#10</div>
    <div class="col-1-12 col-5-8 col-2-4">#11</div>
    <div class="col-1-12 col-2-4">#12</div>
</div>
<!-- If you want full width background with centerized grid, you can wrap the "row" div inside "row-full" div -->

```

Each column set in `$grid-col-count-plus-breakpoints` variable will get CSS for class with naming 'prefix-colsize-colcount' e.g. col-1–12 means 1/12 sized grid item.

`<div class="col-1-12 col-2-8 col-2-4">#1</div>` This element for example will be 1/12 in desktop, 2/8 in tablet and 2/4 in mobile. If you don't set size for X column count it will default to 100%.


