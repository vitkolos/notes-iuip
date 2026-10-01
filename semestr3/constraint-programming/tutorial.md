# Tutorial

- https://jbulin.github.io/teaching/fall/nopt042/

## Picat

- linked list (head & tail syntax) vs. array (can be indexed)
- variables start with capital letter or underscore
- a variable is free until instantiated
- primitive values: atom (quoted or starts with a lower-case letter), number (integer or real)
- compound values: list, string, struct, array (curly braces), map (like dictionary), set
- assignment
	- actually creates a new copy of the variable and updates the occurences so that they refer to the new variable
- dollar … makes sure that the expression is passed to the solver as it is