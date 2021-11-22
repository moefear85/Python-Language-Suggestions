# Python-Language-Suggestions
My Suggestions to improve the Python Language. All these suggestions can be configurable options instead.

1- Variables referenced for read the first time should be None by default, without requiring defining them in advance. This can be a configurable option.

2- Global functions/variables are to a module what class members are to a class. If globals are bad practice, then members that have global scope within a class are also bad practice. See the catch-22 here? IE, the keyword "global" shouldn't be forced, rather complemented/replaced with a "local" keyword when one explicitly wants to reference a local variable if it has the same name as a global one.

3- Each python file can optionally take a shebang that identifies which exact (minimum) python interpreter version it expects, which can be treated as which exact dialect of python it expects. This allows every python version to (if desired) represent a wholly new syntax/language that in no way has to be backwards compatible with any other. Any python interpreter equal or newer can then interpret the file exactly the way it expects or throw an exception if it doesn't support that dialect (for example if it has been obsoleted or if the file expects a newer version than the actual interpreter). If this had been done during the switch from 2 to 3, none of the headache would have occurred, and the same single interpeter would be able of interpreting either version and allow mixing of versions during imports. When the exact diealect is not explicitly specified (and not detectable through file extension), it has to be assumed, and that assumption has to then be standardized and constant and always require backwards compatibility, thus inflexible, and you end up with the current situation.
