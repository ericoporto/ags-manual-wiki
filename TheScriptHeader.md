## The script header

The script header in AGS works like this: its contents are copied verbatim to the script it belongs to, and to all the scripts below. This means that everything that's written in header will be treated as a part of all these scripts during compilation.

This allows you to include the same information into all your scripts. [User struct](ScriptKeywords#struct) declarations, [imports](ScriptKeywords#import), [enums](ScriptKeywords#enum) and [macros](Preprocessor#define) - are common things to place in a header and share them among the multiple scripts.

On the other hand, regular variable declarations should **not** be placed in a script header. That will declare a variable of identical name for every script this header is included to, but these in fact *will not be treated as same variable but as separate ones* (although of same name). This is a common beginner's mistake, and may cause strange program behavior, where you seem to change variable in one script but it does not appear to be changed in another.

It's also best to not place actual functions in headers, as this will create duplicates of such functions everywhere. This is less serious problem, but still not a very good thing. Place function imports in headers instead.

See Also: [Importing functions and variables in other scripts](ImportingFunctionsAndVariables)