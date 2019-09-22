# Lesson: Introduction to Bootstrap

## Notes

- Bootstrap is an HTML, CSS, and JS framework for developing responsive, mobile first projects on the web.

**Benefits of Using Bootstrap**

- Responsive: Easily and efficiently scales your websites and applications with a single code base.
- Features: You get extensive and beautiful documentation for common HTML elements, dozens of custom HTML and CSS components, and awesome jQuery plugins.
- Flexible Styling: Ships with vanilla CSS but its source code utilizes the two most popular CSS preprocessors, Less and Sass so you can quickly get started with precompiled CSS or build on the source.
- Popular: Millions of sites across the web use Bootstrap, which increase the potential for sharing themes and troubleshooting issues.
- Open Source: It's hosted, developed, and maintained on GitHub.
- Build Quickly: Get up and running quickly with a lot of code written for you.

**Drawbacks of Using Bootstrap**

- Individuality: Many sites do not customize their styles beyond the defaults, making hundreds of sites that look the same.
- Non-Content-Driven Media Queries: Unless you use the source code version and set your own custom break points, the precompiled CSS sets breakpoints for you, which can affect the way your content looks as the screen size changes.
- Heavier Than Necessary: If you are not using all the features, the file size could be potentially heavier than if you wrote your own code.

### Bootstrap Grid System

- Columns are nested inside of rows, which are nested inside of containers.

#### Containers

- Bootstrap uses `class="container"` to wrap and center content.
  - `container` will set a fixed width for the element.
  - `container-fluid` will stretch the element to fill the screen.

#### Rows

- Bootstrap uses `class="row"` to create vertical separation.

#### Columns

- Bootstrap uses `class="col-"` to create horizontal separation, the default grid allowing for 12 columns.
- The class name `col-` is followed by either `xs`, `sm`, `md`, or `lg`. These indicate the sizes—extra-small, small, medium, or large-which affect the CSS media query break points, or at what size the columns will collapse so that they will no longer be positioned side-by-side.
  - You can use `-offset` class to shift columns over to the right (i.e. `col-sm-offset-4` will offset the column 4 spaces). Following columns will appear to the right of the offset column.
  - You can also use `-push` to push columns right or `-pull` to pull columns left instead of using `-offset`.
- The number after the second dash indicates the number of units we'd like to span within the 12-unit grid system.
- Columns can be nested inside one another by inserting a row inside a column adn then inserting additional columns inside of the inner row.