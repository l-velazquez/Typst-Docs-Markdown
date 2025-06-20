
# sys

Module for system interactions.

This module defines the following items:

- The `sys.version` constant (of type
  [`version`](/reference/foundations/version/ "`version`")) that
  specifies the currently active Typst compiler version.

- The `sys.inputs`
  [dictionary](/reference/foundations/dictionary/ "dictionary"), which
  makes external inputs available to the project. An input specified in
  the command line as `--input key=value` becomes available under
  `sys.inputs.key` as <span class="typ-str">`"value"`</span>. To include
  spaces in the value, it may be enclosed with single or double quotes.

  The value is always of type [string](/reference/foundations/str/).
  More complex data may be parsed manually using functions like
  [`json.decode`](/reference/data-loading/json/#definitions-decode).
