## Importing functions and variables in other scripts

Functions and variables declared in script A could be used in script B if two conditions are met:
1. Script B is located below script A in the list of scripts;
2. These functions and variables are correctly exported/imported.

**NOTE:** Room and Dialog scripts can use functions and variables from all the regular script modules, but not from other rooms or dialogs.

### Exporting and importing a function

All script functions are exported automatically, so they only need an import declaration to let other scripts know that they exist. This is done by declaring a function with an [import](ScriptKeywords#import) keyword somewhere where script B can "see" it. The best practice is to place them in script A's header.

For example, suppose you have the following function in script A:

    function ScriptAFunction(int param1, int param2)
    {
        // some actions here
    }

Then import the declaration in the script A header will looks like:

    import function ScriptAFunction(int param1, int param2);

The name, type and arguments of the function must be the same of course, otherwise there will be errors either during compilation or at runtime.

### Exporting and importing a variable

Script variables are not exported by default, so that has to be done explicitly inside the script which has them declared, using the [export](ScriptKeywords#export) keyword.

Suppose you have the following variable declaration inside script A:

    int public_variable;

If you want to export this variable for use in other scripts, you put the following `export` statement *inside the same script where you declared the variable* (script A):

    export public_variable;

The `export` statement must be placed outside of the function and needs _only the variable's name_ and nothing else. You can export several variables in one statement if you separate their names with commas.

Then declare the variable's import for other scripts to see, presumably *in the script A header*:

    import int public_variable;

Both the name and type must match the variable's own declaration exactly.<br>
This bit is important. If the variable is `int` it should be imported as `int`, if it's of the type `Character*` then the import should also be declared as `Character*`.<br>
Imported arrays must have the correct size, for example if you have `int arr[10];` then the import declaration must be `import int arr[10];`, otherwise there will be errors.
You can declare the import of several variables _of the same type_ in one statement if you separate them by commas:

    import int var1, var2;

Most commonly import declarations are put in the header of the same script where these variables are defined. But in theory you may not do that and instead place imports inside each particular script where you intend to use these variables.

So, for a final example, you have this in MyScript.asc:

    int public_int1, public_int2;
    float public_float;
    String public_str;
    export public_int1, public_int2, public_float, public_str;

And in MyScript.ash:

    import int public_int1, public_int2;
    import float public_float;
    import String public_str;

To sum this up, the import declaration lets other scripts see this variable, and the export command actually connects existing variables to that declaration.

**NOTE:** The AGS Editor has a special menu called "Global Variables" meant for easier creation of public variables which could are accessible everywhere. This may be a better alternative for beginners, as it takes care of all this import/export managing behind the scenes.

See Also: [import keyword](ScriptKeywords#import), [export keyword](ScriptKeywords#export)