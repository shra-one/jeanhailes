## Bootstrap Documenation for YumpCraft Frontend
Overall, we should be aiming to minimise using our own custom variables and mixins and instead rely on Bootstrap inbuilt mixins and variables. Where we do use our custom variables, we should use them as much as possible at the block level. This will retain the portability of each matrix block. 

You should override the Bootstrap defaults in base/bs-variables. ONLY bs variables should exist in this folder's files. 

## Including other Library' styles globally
- npm install [library] --save-dev
- Then you need to include the path in the gulpfile.js in the sass settings -> includePaths
- Finally, import that into src/styles/base/config.scss using the node module folder name

## Including another Library's JS globally
- npm install [library] --save-dev
- Add the include path to the gulp file paths -> scripts -> src
- Finally, import the path into src/scripts/project/main.js or into its own file in using the node module folder name

## Bootstrap Tips
- Try to avoid using grid classes in html. Instead use the functions to apply a grid to a block. 
	- @include make-col(6) will apply the width using flex
	- @include make-col-ready() will add the padding to the left and right

## Including Styles or JS at the Block Level
- Use {% js at [position] %}{% endjs %} or {% css %}
	- See https://docs.craftcms.com/v3/dev/tags/js.html#parameters for list of valid positions

## Grid Guide
WARNING: Please avoid using the make-container() or make-container-max-widths() mixin on individual neo block template or anything which can potentially go nested inside a .container. Use .container in HTML instead. The reason is: we want to avoid child / decendant blocks having left and right paddings given by .container, or the make-container mixins. To avoid that, the easiest solution is using this one css rule: .container .container {padding-left: 0; padding-right: 0}. But if mixin is used, it's very hard to do this, except for apply the padding rule to each one of the occurances. Other than this kind of situation, you can use the mixins if you want:

- To make a container and set it to the default container widths:
	- @include make-container(); - this will set it to 100% width
	- @include make-container-max-widths(); - this will add media queries to define width according to the grid breakpoints (default BS ones if you haven't overridden them)
- See https://gist.github.com/anschaef/d7552885c0e1f127cf8830d3bbf6e4b1 for a mixins cheatsheet.