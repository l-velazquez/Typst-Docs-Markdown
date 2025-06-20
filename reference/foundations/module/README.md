
# Module

A collection of variables and functions that are commonly related to a
single theme.

A module can

- be built-in
- stem from a [file import](/reference/scripting/#modules)
- stem from a [package import](/reference/scripting/#packages) (and thus
  indirectly its entrypoint file)
- result from a call to the [plugin](/reference/foundations/plugin/)
  function

You can access definitions from the module using [field access
notation](/reference/scripting/#fields) and interact with it using the
[import and include syntaxes](/reference/scripting/#modules).
Alternatively, it is possible to convert a module to a dictionary, and
therefore access its contents dynamically, using the [dictionary
constructor](/reference/foundations/dictionary/#constructor).

## Example

<div class="previewed-code">

    #import "utils.typ"
    #utils.add(2, 5)

    #import utils: sub
    #sub(1, 4)

<div class="preview">

![Preview](/assets/8ad38f6a26a534e6fad80f3544716fff.png)

</div>

</div>


## Definitions

