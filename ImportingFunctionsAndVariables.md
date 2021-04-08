## Importing functions and variables in other scripts

Functions and variables declared in script A could be used in script B if two conditions are met:
1. Script B is located below script A in the list of scripts;
2. These functions and variables are correctly exported/imported.

**NOTE:** Room and Dialog scripts can use functions and variables from all the regular script modules, but not from other rooms or dialogs.

### Exporting and importing a function

All script functions are exported automatically, so they only need an import declaration to let other scripts know that they exist. This is done by declaring a function with an [import](ScriptKeywords#import) keyword somewhere where script B can "see" it. The best practice is to place them in script A's header.

For example, suppose you have following function in script A:

    function ScriptAFunction(int param1, int param2)
    {
        // some actions here
    }

Then import declaration in the script A header will looks like:

    import function ScriptAFunction(int param1, int param2);

The name, type and arguments of the function must be the same ofcourse, otherwise there will be errors either during compilation or at runtime.

### Exporting and importing a variable

Script variables are not exported by default, so that has to be done explicitly inside the script which has them declared, using [export](ScriptKeywords#export) keyword.

Suppose you have following variable declaration inside script A:

    int public_variable;

If you want to export this variable for use in other scripts, you put following `export` statement *inside the same script where you declared the variable* (script A):

    export public_variable;

The `export` statement needs only variable's name and nothing else.

Then declare variable's import for other scripts to see, presumably *in the script A header*:

    import int public_variable;

Both the name and type must match the variable's own declaration exactly.<br>
This bit is important. If variable is `int` it should be imported as `int`, if it's of type `Character*` then import should also be declared as `Character*`.<br>
Imported arrays must have correct size, for example if you have `int arr[10];` then import declaration must be `import int arr[10];`, otherwise there will be errors.

Most commonly import declarations are put in the header of the same script where these variables are defined. But in theory you may instead not do that and place imports inside each particular script where you intend to use these variables.

To sum up, the import declaration lets other scripts see this variable, and the export command actually connects existing variable to that declaration.

**NOTE:** AGS Editor has a special menu "Global Variables" meant for easier creation of public variables which could be accessible everywhere. This may be a better alternative for beginners, as it takes care of all this import/export stuff behind the scenes.