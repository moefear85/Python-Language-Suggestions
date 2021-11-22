# Python-Language-Suggestions
My Suggestions to improve the Python Language. All these suggestions can be configurable options instead.

1- Variables referenced for read the first time should be None by default, without requiring defining them in advance. This can be a configurable option.

2- Global functions/variables are to a module what class members are to a class. If globals are bad practice, then members that have global scope within a class are also bad practice. See the catch-22 here? IE, the keyword "global" shouldn't be forced, rather complemented/replaced with a "local" keyword when one explicitly wants to reference a local variable if it has the same name as a global one.
