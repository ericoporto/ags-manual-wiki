## Dynamic Arrays

Suppose that you're writing a script that you want people to be able to
use in their games. You need to store the Health for every character in
the game, but you don't know how many characters there will be. What do
you do?

Dynamic Arrays are designed for just this purpose. You can declare an
array like this:

`int characterHealth[];`

in your script file. This special notation tells AGS that you don't yet
know how large you want the array to be. Now, before you use the array
(so probably in game_start), you can do this:

`characterHealth = new int[Game.CharacterCount];`

If you forget to do this `new` command, you'll get a Null Pointer Error
if you try to access the array. You can change the size of an array by
simply using another `new` command with a different size; but this will
erase the contents of the array in the process.

You may create dynamic arrays of basic types (int, char, etc), built-in types (String,
Character, etc), and custom structs declared as `managed`. But currently you cannot have dynamic arrays of regular (non-managed) custom structs.

On another hand, you cannot have dynamic arrays inside "managed" structs as their members, but can have them anywhere else.

See Also: [Arrays](ScriptKeywords#arrays), [Structs](ScriptKeywords#struct)
