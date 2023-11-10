# Python-Language-Suggestions
My Suggestions to improve the Python Language. All these suggestions can be configurable options instead.

1- Variables referenced for read the first time should be None by default, without requiring defining them in advance. This can be a configurable option.

2- Global functions/variables are to a module what class members are to a class. If globals are bad practice, then members that have global scope within a class are also bad practice. See the catch-22 here? IE, the keyword "global" shouldn't be forced, rather complemented/replaced with a "local" keyword when one explicitly wants to reference a local variable if it has the same name as a global one. Alternately/Additionally, it can provide a "one up" symbol, (like git), such as someVar~, or someVar^, which can be nested several times, such as someVar^^^, to indiciate how many steps of parent scope to traverse before looking for the variable, and this would be relative to the current scope, and not depend on whether any variables are actually defined in the lower scopes or not (to avoid confusion).

3- The self keyword should be implicit ie the default, to avoid repetitive typing. IE, a keyword should be specified whenever one does NOT want to reference self within a class. Thus a "static" keyword is needed. This follows the same logic as suggestion No-2, in that the default/implicit case should always be the more common scenario, and any extra typing/keywords should only be done to differentiate when a less common scenario is intended.

4- Each python file can optionally take a shebang that identifies which exact (minimum) python interpreter version it expects, which can be treated as which exact dialect of python it expects. This allows every python version to (if desired) represent a wholly new syntax/language that in no way has to be backwards compatible with any other. Any python interpreter equal or newer can then interpret the file exactly the way it expects or throw an exception if it doesn't support that dialect (for example if it has been obsoleted or if the file expects a newer version than the actual interpreter). If this had been done during the switch from 2 to 3, none of the headache would have occurred, and the same single interpeter would be able of interpreting either version and allow mixing of versions during imports. When the exact dialect is not explicitly specified (and not detectable through file extension), it has to be assumed, and that assumption has to then be standardized and constant and always require backwards compatibility, thus inflexible, and you end up with the current situation. This concept actually benefits any language as well. Just as importantly, it benefits APIs too, or more specifically, each module can have an associated version number. Every module that calls another, must make a decision (which can be automatically implicitly chosen), as to which version of the module it expects. Then the python interpreter can be shipped with multiple versions (or separately installable), which avoids compatibility issues when the api is modified. It automatically loads the right version if it is installed.

5- C++-Style References: or atleast ability to pass objects by reference, so that no copies are made and the originals get modified. This is mostly useful for basic types. This isn't the same thing as memory pointers, and those are a bad idea.

6- Late Binding for Default Values (of function arguments): Early binding has its needs, but it would also be useful to have a syntax, some symbol, different than the "=", such as "::" that would indicate the desire for late-binding. This doesn't unnecessarily complicate the interpreter, nor lead to excessive execution, since the programmer would otherwise have to write alot more code with the same effect at the top of the function. This is not always a good idea, since the interpeter already knows upon function entry, whether that parameter is empty/None or not, hence knows what action to take, whereas the programmer would first have to test for every argument whether a value has been provided or not, and python does not have an efficient way to determine None-ness (to my knowledge), since "if isinstance(someVar,NoneType): ..." along with a necessary import at the top, is not really concise. Update: "if someVar is None:" seems to work now, although it didn't before. Guess I missed something.

7- A concise way to test for nullness, such as "ifn someVar:", where ifn means "if is None", and "ifd someVar:", where ifd means "if defined" or "if exists" or "if not none".

8- "finally" has uses, but it is limited to a more concise form of "except Exception: pass". Since both guarantee that the code after "except" or within "finally" and afterwards. It also has niche uses when one wants to include return statements within try/except rather than placing these after finally (or except Exception: pass). Perhaps a better alternative, or a complement, would be a statement that is guaranteed to run, but only if an exception occurs, irrespective whether it was handled by any except clause or not.

9- Sometimes, one wants to break a statement onto multiple lines, while adding spaces to maintain alignment, otherwise the code looks ugly and complicated. It would be nice, atleast if a \ is present at the end of the line (or another escape char, such as \\\\) that would cause python to forgive a bit with spurios whitespaces or act like none are there. Instead, I keep getting errors. Is it just me?

10- Late Binding for imports when imported like "from abc import xyz as foo": It would be nice when some global variable is imported from another module, any changes to it in the target module are reflected in the source module, so that any other modules that also import that variable, will see the changes. However, since early binding is still necessary, this feature should augment, not replace. Currently, if I import as stated above, the value of "foo" doesn't reflect itself in the source module and other modules that import it.

11- An easy way to look up the name of the constant that was assigned to some variable. If one has constants "X=0","Y=1","Z=2", and a variable "coord", to which one can assign "X", or "Y", "Z", and one later wants to know which axis is assigned to "coord", one has to write a reverse-lookup function with hard-coded numbers-to-names. This is error-prone and lengthy and accounts for a large portion of many projects. Having a built-in "name_of_assigned_const" that one can call like "name_of_assigned_const(coord)" and would return "X" or "Y" or "Z" as a string literal, would be nice. From the discusson at https://stackoverflow.com/questions/18425225/getting-the-name-of-a-variable-as-a-string, it seems this feature isn't available, atleast not well-known if it exists.

12- Ability to suppress exceptions without skipping remaining statements. Python has a "with contextlib.suppress(Exception):" feature, but this still skips over the remaining statements once an exception happens. To my knowledge, this is not configurable. The only remaining unpythonic way is then to wrap each statement in its own try/except clause. A use case would be several os.remove() statements to remove a list of files. One doesn't care of any of the files don't already exist. It shouldn't be necessary to encode the needed functionality within the called function itself. I believe this project: https://github.com/ajalt/fuckitpy, sums up my sentiment. Exception handling, like so many features that shoudl assist you, end up nannying/forcing you unnecessarily. Even if complex branching isn't supportable with the envisioned variant of suppress(), one can require only simple calls be present, otherwise an exception is invariably raised.
  An even more flexible exception handling system, would be to be able to label exception handlers within the scope of a function, then specify the label in the try clause, such that if an exception is encountered in the try block, the labelled exception is executed, but the exception handler can specify whether code should continue after the exception handler, or jump back to the original statement and try it again, or skip to the following statement. All in all a counter is maintainable by the handler, to determine how many "retries" have been attempted and break the cycle if after several remedy attempts, the try block is still failing. Hence a try block doesn't need to be immediately followed by a (traditionally unlabelled) except block. IE exception-triggered/-controlled goto and goback functions that can be shared by different try blocks, are useful. Initially it should be limited to only function scope as an experimental feature, to detect any issues with this model, since the exception handler is not its own function and needs access to the same scope as the try block in order to be able to reference the same variables, and it needs to be able to do this in order to meaningfully/effectively resolve any problems.

13- Python needs version managing at the file level, such that any python script when importing a module, automatically imports the latest one, unless it specifies which version after the module name, that uses the same syntax as during installation of packages, such as using "!=" or "<". This then offloads the responsibility of version compatibility to the caller instead of the installer, which in turn allows pip to install several versions of a package concurrently, such that this no longer needs a separate virtual environment for every combination of package conflicts. Alternately, this versioning information should be encodable in a separate metafile that can accompany the script or module, and python uses this file if it is present. This keeps the original source file clean and avoids changes to the source file itself whenever the author decides to change the set of supported versions of imports. This way of version management isn't new, it is already used successfully for DLLs/SOs and kernels running on any system. It would be a nightmare if a system only supported one version of each library, such that every package that needs a specific set of versions of shared libraries, would be forced to create an entire separate "virtual system" to handle this. This also enables a user wanting to experiment with several different versions of a module to do so easily, without having to change virtual environments and reinstalling redundant packages.
  In other words, linux already solved this problem perfectly for C/C++ long ago by using different version suffixes for libraries. If that has caused anyone any headaches, its because the build tools/environments never provided an easy/clean/concise interface to the programmer to be able to configure the project as to which ranges of versions of each library it it is known to work with, and which it definately does not, thus leaving a range of unknown that a end-user may test. But this is already solved nicely in python.

14- Ability to use directional quotes in additional to undirectional ones. This might require keyboard modifications or atleast key mapping in order to support this, since for example, the quotes used in libreoffice are directional, ie there are opening quotes followed by closing quotes. The benefit of directional ones, is that these are parentheses-like, and so are indefinately nestable without ambiguity, whereas for undirectional ones, the only option is one level of double quotes within single quotes or vice versa. This then often requires complicated quote escaping for certain strings.

15- The pypi should use namespaces, like android/java such as "foo.bar.spam.eggs". This resolves naming conflicts especially when unrelated teams solve the same problem and give it the same most basic reasonable name. This also then enables globbing, allowing an end-user to type `pip install mf.*`, which would install all packages found under that sub-/namespace, which would then usually be related.

16- Killing threads is not bad practice, because it is already an inherent part of the language. If you really wanted to prevent bad practices you’d have to prevent everything that is equivalent to killing threads, and that would include exceptions. If an exception is raised, a thread also does not get a chance to close any opened resources through normal execution paths (it can get cut-off at any non-deterministic moment at any line of code just like with `kill()`), and any mechanisms existing to deal with such a case can also be used for explicitly killed threads. The `kill()` function is equivalent to raising an exception at an arbitrary point in the code’s execution, which can already happen anyways, be the thread running or blocking on some operation (such as timeout exceptions). The only difference is the conceptual reason as to why or who is responsible for triggering the exception hence killing of the thread, which is irrelevant from a programming point of view. So `kill()` can simply raise a `KilledException`, and the thread is responsible for implementing a `try/except/finally` or `with` statement to handle resources. Such a feature would greatly speed up python because it would make concurrent programming much easier. The only thing required, which is already done for exceptions, is to respect the `finally` and give it a chance to run (or any other thread code defined to explicitly run on a kill/termination/exception), rather than really hard-stop the thread, because that is equivalent to linguistically allowing exceptions to be raised, but forbidding exception handling whatsoever. If you wanted to simply not implement a linguistic feature to nanny people and prevent bad practice, you'd also have to forbid writing any function without exlicit `try/except` clauses. I believe practicality over purity should decide in this case.
  * If desired, there can be `enter_critical/exit_critical` statements to mark regions where a user-initiated exception should be held-back and deferred until the region is exited. Moreover these as well as the kill statement can take an argument that represents the urgency level. Then any kill level lower than the critical level can't kill the thread within that section.
