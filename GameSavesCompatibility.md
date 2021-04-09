## Game saves compatibility

AGS games have a built-in save system that is very convenient most of the time as it automatically writes down states of the game and all objects in it, allowing to restore saved game to exactly same condition it was saved in.

But has one serious flaw. When game data is written to a save file the game objects and variables are written as lists, where separate items are not identified in any way rather than order in that list.
Because of that, if you, the author of the game, update your game adding or removing any objects, *all the saves made by previous version will become unusable*.
Simply changing IDs of game objects in the project tree or order of the variables in script will cause previous saves to glitch, as old data will be restored into wrong objects or variables.

This may not be the biggest issue while the game is in development, as you have multiple ways to make game "teleport" to necessary scene instead of using a save state. But it becomes a problem after you released your game to public, as any update or patch that involves adding new objects or variables will render player's saves unusable.

Following article explores which changes to game are safe and which are not in terms of keeping your game compatible with older saves, and which known methods exist to help you keep your game compatible with previous saves.

### Changes in game that break saves

Changing number (adding or removing) of any game objects will break previous saved states. Following types of objects contribute to this:
* Audio Types,
* Characters,
* Dialogs (but not options in existing Dialog, for technical reasons),
* Global Variables,
* GUI and controls on existing GUI,
* Inventory items,
* Mouse cursor types,
* Views, loops and frames in them (because frames may be changed in script and their properties are added to save state),
* Script modules (number of them)

In addition to that, changing *total size* of variables declared in the global scope of each script (*NOT* local function variables) will similarily break older save states.
To elaborate, imagine you have this declared in some script:
<pre>
int a;
int b;
int c;
</pre>
This makes total size of script variables to be 3 integers (or 3 * 4 = 12 bytes). Now, if you change this to
<pre>
int vars[3];
</pre>
Even though there's now only one variable this also makes total size of 3 integers, and won't break save states.
(Here we omit a question whether it will still make sense to restore older save with such change in script.)

### Changes that DON'T break saves but are NOT SAFE

Changing number of certain things while technically not preventing to restore old saves, still may lead to bugs:
* Custom properties,
* Room Objects in existing rooms

### Changes that DON'T break saves and ARE SAFE

Parts of game which may be safely added or removed:
* Rooms, when they are added or removed in whole. Except loading state saved in a no longer existing room will crash the game.
* Room backgrounds in existing rooms.

Also adding or removing any kind of plain resources, such as
* Sprites,
* Fonts,
* Audio clips,
* Voice-over clips,
* Video files

In scripts:
* User types (structs) may be added; but if you change the size of a regular struct while having variables of that type in your script - that would also change the size of these variables, and may break saves. Managed structs *may* be changed in size without breaking a save, but this may still cause glitches (see below).
* Macros,
* Functions and attributes, and generally - function code itself,
* Local variables (inside functions), because they are not saved, because AGS does not allow to save game while inside a script function
* Any managed objects (of built-in type or user type) created dynamically (but not global pointers to them).

The latter may need further elaboration.

### An issue of dynamic objects

The pointers which are global variables are part of script's total variable size, and so adding or removing them in script will result in save break. However the *managed objects themselves* are saved and loaded differently and can't break saves.
Even changing sizes of them won't break saves, even though may lead to strange results in certain cases.

Consider a simple dynamic array:
<pre>
int dyn_arr[];
int arr_size;

function game_start() {
    dyn_arr = new int[100];
    arr_size = 100;
}
</pre>

Let's assume you had this in game version 1, made a save, then increased dynamic array's size in script to 200. What will happen if you now compile game version 2 and then restore old save?
It contains dynamic array of size 100, which will be safely read. And if you have its length in a variable, that length will also be restored, so your script will likely function correctly so long as you check that variable to get array's length, and not rely on hardcoded number (100 in game version 1 or 200 in version 2).

Now let's consider a custom managed struct. In game version 1 you have:
<pre>
managed struct MyStruct {
    int a;
    int b;
};

MyStruct* var;

function game_start() {
    var = new MyStruct;
}
</pre>

Then in game version 2 you decided to add another variable:
<pre>
managed struct MyStruct {
    int a;
    int b;
    int c;
};
</pre>

If you load older save from version 1 while running version 2, created objects of this type will load, but the newer variable will not be initialized.
If on other hand you remove a variable:
<pre>
managed struct MyStruct {
    int a;
};
</pre>

Again, the older save will be restored, and old variants of MyStruct will also be loaded, but you obviously no longer will be able to access rest of the variables in script, because they are no longer declared.
Finally, let's look at this variant:
<pre>
managed struct MyStruct {
    int a;
    // int b;
    int c;
};
</pre>
The `b` variable was removed, so variable `c` now follows `a`. If you load older save however, the data of that save did contain variable `b`, and its value will be assigned to `c` instead as it took its place in the struct.

For that reason, if save compatibility is essential, it's recommended to only extend managed types but not cut out existing data.

---

### Solution 1: Reusing game objects

If you need to urgently patch your released game but realized you are going to break previous saves by doing that, you may try reusing existing game objects.

Characters may switch Views and play different roles in other rooms. Unused Room Objects are perhaps more rare, but they may be switched their Graphic or View too and act like something else. Characters may be used as room elements too, except they cannot be simply assigned a sprite, but require a View.
GUIs may be reconfigured on the fly, if you have enough suitable controls on them.
View Frames may be assigned different sprites, even DynamicSprite which you can paint upon to display something different.

Global variables may be reused for other purposes if you find a way to indicate what meaning they have at the moment and how they should be used in your script in various circumstances.

### Solution 2: Dummy object reserve

If you are planning ahead your game release, there's one very straightforward yet ugly solution: create a number of extra objects of every type (Characters, GUIs, and so on) that you don't use right now but which could be used in case of emergency for patching the game.

In terms of script, you can allocate big global arrays of ints or other types as a reserve for future fixes and updates, then use elements of those arrays whenever you need an extra variable.

### Solution 3: New rooms

If you must change room's contents but do not want to break saves at all costs you may create a duplicate room with a new number and updated contents, then script changing room if player restores a save made in the old room.

This is done like this, for example:
<pre>
function on_event(EventType evt, int data) {
    if (evt == eEventRestoreGame) {
        if (player.Room == OLD_ROOM_NUMBER) {
            player.ChangeRoom(NEW_ROOM_NUMBER);
        }
    }
}
</pre>

### Solution 4: Extending dynamic arrays and Dictionary

As mentioned earlier, any managed object is not restricted to change because its full contents are read from the save. This allows to use managed structs and dynamic arrays as infinite reserve for variables.
Upon loading an old save you would need to test a length or other kind of "version" of that array and resize it: create new one, copy old restored contents, fill in rest with default values, replace pointer variable.

Consider following example:
<pre>
#define GAME_VER_001_LENGTH 10
#define GAME_VER_002_LENGTH 20

int MyVarVersion;
int MyVariables[];

function game_start() {
    MyVarVersion = 2;
    MyVariables = new int[GAME_VER_002_LENGTH];
}

function on_event(EventType evt, int data) {
    if (evt == eEventRestoreGame) {
        // detect old save
        if (MyVarVersion == 1) {
            // allocate bigger array suited for latest version of the game
            int new_vars[] = new int[GAME_VER_002_LENGTH ];
            // copy restored array with old data into our new array
            for (int i = 0; i < GAME_VER_001_LENGTH; i++) {
                 new_vars[i] = MyVariables[i];
            }
            // set default values for the rest (replace with your code as appropriate)
            for (int i = GAME_VER_001_LENGTH; i < GAME_VER_002_LENGTH; i++) {
                 new_vars[i] = 0;
            }
            // finally replace pointer and version number
            MyVariables = new_vars;
            MyVarVersion = 2;
        }
    }
}
</pre>

Since AGS 3.5.0 there's also a [Dictionary](Dictionary) type. This may serve as an alternative to dynamic arrays in this solution. It's easy to extend and easy to check which variables (keys) it contains, so may be used as a universal global storage, for example, for story variables that's easy to expand between game versions.
