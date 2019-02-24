## Preprocessor

Before the AGS Script compiler is ran, an AGS Preprocessor runs, which will modify the script file before it's passed on for the compiler.

### define

`#define DEFINED_NAME <value>`

Define is a way to tell the processor that, whenever the defined name is encountered, it should be replaced by the value that follows. It's similar to a variable with a set initial value, but this variable has no type.

### region

```
#region
  // some code
#endregion
```

You can wrap a code between lines containing `#region` and `#endregion` to create a section used for code folding. In the AGS Editor you can use this to hide sections of your code you don't need to see by using the `+` button at the left side of the script editor.



### ifdef 
```
#ifdef
```
```
#ifndef
```
Test if macro is defined


### ifver
```
#ifver
```
```
#ifnver
```
_See also:_ [Version Checking Keyword](ScriptKeywords#version-checking)


### error
```
#error
```
User defined compile-time error (with message)

### legacy commands
```
#sectionstart
```
```
#sectionend
```
These two preprocessor commands do nothing, they are ignored legacy commands from pre-3 era. 
They are valid keywords so there you have it.

 
 
 
_See:_ [Scripting Languange](ScriptingLanguage)
