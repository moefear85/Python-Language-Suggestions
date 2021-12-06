# Python-Language-Suggestions
My Suggestions to improve the Python Language. All these suggestions can be configurable options instead.

1- Variables referenced for read the first time should be None by default, without requiring defining them in advance. This can be a configurable option.

2- Global functions/variables are to a module what class members are to a class. If globals are bad practice, then members that have global scope within a class are also bad practice. See the catch-22 here? IE, the keyword "global" shouldn't be forced, rather complemented/replaced with a "local" keyword when one explicitly wants to reference a local variable if it has the same name as a global one. Alternately/Additionally, it can provide a "one up" symbol, (like git), such as someVar~, or someVar^, which can be nested several times, such as someVar^^^, to indiciate how many steps of parent scope to traverse before looking for the variable, and this would be relative to the current scope, and not depend on whether any variables are actually defined in the lower scopes or not (to avoid confusion).

3- The self keyword should be implicit ie the default, to avoid repetitive typing. IE, a keyword should be specified whenever one does NOT want to reference self within a class. Thus a "static" keyword is needed. This follows the same logic as suggestion No-2, in that the default/implicit case should always be the more common scenario, and any extra typing/keywords should only be done to differentiate when a less common scenario is intended.

4- Each python file can optionally take a shebang that identifies which exact (minimum) python interpreter version it expects, which can be treated as which exact dialect of python it expects. This allows every python version to (if desired) represent a wholly new syntax/language that in no way has to be backwards compatible with any other. Any python interpreter equal or newer can then interpret the file exactly the way it expects or throw an exception if it doesn't support that dialect (for example if it has been obsoleted or if the file expects a newer version than the actual interpreter). If this had been done during the switch from 2 to 3, none of the headache would have occurred, and the same single interpeter would be able of interpreting either version and allow mixing of versions during imports. When the exact diealect is not explicitly specified (and not detectable through file extension), it has to be assumed, and that assumption has to then be standardized and constant and always require backwards compatibility, thus inflexible, and you end up with the current situation.

5- C++-Style References: or atleast ability to pass objects by reference, so that no copies are made and the originals get modified. This is mostly useful for basic types. This isn't the same thing as memory pointers, and those are a bad idea.

6- Late Binding for Default Values (of function arguments): Early binding has its needs, but it would also be useful to have a syntax, some symbol, different than the "=", such as "::" that would indicate the desire for late-binding. This doesn't unnecessarily complicate the interpreter, nor lead to excessive execution, since the programmer would otherwise have to write alot more code with the same effect at the top of the function. This is not always a good idea, since the interpeter already knows upon function entry, whether that parameter is empty/None or not, hence knows what action to take, whereas the programmer would first have to test for every argument whether a value has been provided or not, and python does not have an efficient way to determine None-ness (to my knowledge), since "if isinstance(someVar,NoneType): ..." along with a necessary import at the top, is not really concise.

7- A concise way to test for nullness, such as "ifn someVar:", where ifn means "if is None", and "ifd someVar:", where ifd means "if defined" or "if exists" or "if not none".

8- Sometimes, one wants to break a statement onto multiple lines, while adding spaces to maintain alignment, otherwise the code looks ugly and complicated. It would be nice, atleast if a \ is present at the end of the line (or another escape char, such as \\\\) that would cause python to forgive a bit with spurios whitespaces or act like none are there. Instead, I keep getting errors. Is it just me?
