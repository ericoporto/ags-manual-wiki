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