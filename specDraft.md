# GVG File Format Syntax

## Header
`gvg [dimensions] version:[version (optional)]`

## Command
`[command] [requiredParameters] [optionalParameters]`

### Optional Parameters
`[key]:[value]`

#### Parameter values
 - Vector

		x,y

 - List

		1_2_3

 - List of vectors

		x1,y1_x2,y2_x3,y3


&nbsp;


### Available Commands
 - shape

		shape [shapeType (required)] [optionalParameters]

	Draw a shape.

 - text

		text [string (required)] font:[fontFamily (optional)] mode:[fontRenderMode (optional)] [optionalParameters]

	Draw text.

 - group

		group [optionalParameters]
			# ...
		$

	Group elements together.

 - batch

		batch [shapeType (required)] [list of shapes???] [optionalParameters]

	Draw multiple of the same shape in a single draw call for maximum efficiency.

 - combine

		combine [function] [list of shapes???] [optionalParameters]

	Combine shapes using one of the following functions

 - alias

		alias id:[id (optional)] file:[path (optional)] [optionalParameters]

	Include element by id. Requires `id` or `file` or both. If `id` is defined but `file` is undefined, it assumes an element from the current file. If `file` is defined but `id` is undefined, it assumes the root of the file. If both are defined, it references an the specified id within the specified file.


&nbsp;


## Numbers
 - Integer `10`
 - Negative `-10`
 - Float `10.5`
 - Percentage `10%` ??? (probably not)
 - Units `10in` ???

### Supported Units ???
 - Pixels (no unit)
 - Percent `%` (of container) (probably not)
 - Milimeter `mm`
 - Centimeter `cm`
 - Meter `m`
 - Inch `in`
 - Foot `ft`
 - Yard `yd`


&nbsp;


## Comments
 - Single line

		# Single line comment

 - Multi-line

		< Multi-line
		comment >


&nbsp;

## Strings
`` `String text` ``

Strings are used only when specifying a filename, or an actual string such as in the `text` command. Element `id`'s are not strings and therefore do not allow spaces or other reserved characters.


&nbsp;


## Minification
Newlines can be replaced with the `|` (pipe) character.


&nbsp;


## Examples
#### Standard

	font labelfont file:`/path/to/Folder with a/font.ttf`
	shape circle x:5 y:5 radius:15
	group x:20 y:10
		# Single Line Comment
		< Multi
		Line
		Comment >
		shape polygon vertices:54,91_85,49
		alias file:`/path/to/Folder with a/file.gvg`
		text `Text` x:0 y:0 font:labelfont
	$



#### Minified

	font labelfont file:`/path/to/Folder with a/font.ttf`|shape circle x:5 y:5 radius:15|group x:20 y:10|# Single Line Comment|< Multi|Line|Comment >|shape polygon vertices:54,91_85,49|alias file:`/path/to/Folder with a/file.gvg`|text `Text` x:0 y:0 font:labelfont|$
