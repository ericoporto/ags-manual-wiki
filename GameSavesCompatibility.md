## Game saves compatibility

AGS games have a built-in save system that is very convenient most of the time as it automatically writes down states of the game and all objects in it, allowing to restore saved game to exactly same condition it was saved in.

But it has one serious flaw. When game data is written to a save file the game objects and variables are written as lists, where separate items are not identified in any way rather than order in that list.
Because of that, if you, the author of the game, update your game adding or removing any objects, *all the saves made by previous version will become unusable*.
Simply changing IDs of game objects in the project tree or order of the variables in script will cause previous saves to glitch, as old data will be restored into wrong objects or variables.

This may not be the biggest issue while the game is in development, as you have multiple ways to make game "teleport" to necessary scene instead of using a save state. But it becomes a problem after you released your game to public, as any update or patch that involves adding new objects or variables will render player's saves unusable.

Following article explores which changes to game are safe and which are not in terms of keeping your game compatible with older saves, and which known methods exist to work around this problem.

### Changes in game that break saves

Changing number (adding or removing) of almost all game objects will break previous saved states. Following types of objects contribute to this:
* Audio Types,
* Characters,
* Dialogs (but not options in existing Dialog, for technical reasons),
* Global Variables,
* GUI and controls on existing GUI,
* Inventory items,
* Mouse cursor types,
* Views, loops and frames in them (because frames may be changed in script and their properties are added to save state),
* Script modules (number of them)

In addition to that, changing *total size* of variables declared in the global scope of each script (*NOT* local function variables) will break older save states.<br>
To elaborate on what "total size" is, imagine you have this declared in some script:
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

Changing number of Room Objects in existing rooms, while technically not preventing to restore old saves, still may lead to bugs. Because their real number is stored in saves players may end up having more or less objects in a room than supposed by the game. And because currently you cannot create or delete Room Objects with a script command you won't be able to fix this, only detect when this happens by checking [Room.ObjectCount](Room#roomobjectcount).

Changing the size of the dynamic arrays and managed structs won't break saves, but may cause game to crash if script tries to access newer elements or variables in these arrays and structs after restoring older saves.<br>
Still this may be worked around and actually be used for your advantage in the bad situation: see [dedicated section below](#an-issue-of-dynamic-objects) for more information.

### Changes that DON'T break saves and ARE SAFE

Parts of game which may be safely added or removed:
* Dialog options in existing Dialogs.
* Rooms, adding new ones. Removing a room is *not* safe, as loading state saved in a no longer existing room will crash the game.
* Adding room backgrounds in existing rooms, but probably not removing them (*need to be checked*).
* Custom properties. If you remove existing ones, their values may still load from the older save but will not be accessible.

Adding or removing any kind of plain resources, such as
* Sprites
* Fonts,
* Audio clips,
* Voice-over clips,
* Video files,
* Translations

**IMPORTANT:** Removing sprites is only safe if you fix any objects that could have them assigned upon restoring a save. Same goes for clips assigned to View Frames, and fonts used on GUI.

In scripts:
* User types (structs) may be added; but if you change the size of a regular struct while having variables of that type in your script - that would also change the size of these variables, and may break saves. Managed structs *may* be changed in size without breaking a save, but this requires special approach ([see below]((#an-issue-of-dynamic-objects))).
* Macros,
* Functions and attributes, and generally - function code itself,
* For same reasons - changing existing dialog scripts,
* Local variables (inside functions) may be added and removed freely because they are not saved, because AGS does not allow to save game while inside a script function

### An issue of dynamic objects

The pointers which are global variables are part of script's total variable size, and so adding or removing them in script will result in save break.
The *managed objects themselves* are stored not in script's variable memory, but in their own memory pool. They are also written to save file awhole, and loading this save will restore original managed object with its original size. Therefore, changing their sizes in new version of the game don't break previous saves.
However, there's a number of potential problems with that and these has to be resolved if you like to maintain save compatibility.

Consider a simple dynamic array:
<pre>
int dyn_arr[];

function game_start() {
    dyn_arr = new int[100];
}
</pre>

Let's assume you had this in game version 1, made a save, then increased dynamic array's size in script to 200:
<pre>
    dyn_arr = new int[200];
</pre>

What will happen if you now compile game version 2 and then restore old save? The game will restore dynamic array of the previous size 100. This means that if your new script will try to access elements beyond 100 (thinking that array has 200 elements now), that would cause "index out of range" error.
Unfortunately at the time of writing dynamic arrays don't let you know their length in script. But you can store their length elsewhere, for example, in a variable:
<pre>
int dyn_arr[];
int arr_size;

function game_start() {
    dyn_arr = new int[100];
    arr_size = 100;
}
</pre>

There are other ways of course, for instance you may store array's length in its first element. That way you keep it within array itself, but will have to remember it's there when you work with array. Anyway, that's a different topic.
In any case, having array's length stored, if you ever change that array's size and restore older save, that length variable will be also restored and tell you correct array's size.
If you still need array to be exactly size 200 in the new version of the game you may resize it after restoring a save. This is explained further in ["Solutions" section](#solution-4-extending-dynamic-arrays-and-dictionary).

Less likely, but if you instead reduce array's size then the array restored from older save will be bigger in size than necessary, but that's much less of a problem and may be safely ignored.

As we are done with dynamic array, now let's consider a custom managed struct. Assume in game version 1 you have:
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

If you load older save from version 1 while running version 2, created objects of this type will load but will be one variable less in size. Trying to use this variable in script will result in error. This is similar to array case.
The solution then is likely similar: upon restoring older save recreate managed objects (they will be of correct size), copy valid contents from restored objects into them, and reassign pointers to these recreated objects. Again this is explained more in a ["Solutions" section](#solution-4-extending-dynamic-arrays-and-dictionary).

And again, if you remove a variable instead:
<pre>
managed struct MyStruct {
    int a;
};
</pre>

Here he older save will be restored, and old variants of MyStruct will also be loaded. They will contain all the removed variables, but you no longer will be able to access them in script because they are no longer declared so script is not aware they exist.

Finally, there's another potential problem. Let's look at this variant:
<pre>
managed struct MyStruct {
    int a;
    // int b;
    int c;
};
</pre>
The `b` variable was removed, so variable `c` now follows `a`. If you load older save however, the old MyStruct objects contain variable `b`, and its value will be assigned to `c` instead as it took its place in the struct.

For that reason, if save compatibility is essential, it's recommended to only *extend* managed types but not cut out existing data.

---

### Solution 0: Code your own save system

Yes, this may sound as a crazy suggestion, but it's a real opportunity. Depending on your requirements this solution may range from almost trivial to nearly impossible to accomplish in script. This is a whole separate topic though so we won't go into much detail here. But to give a heads up, if you would like to experiment:

* AGS supports writing and reading custom files. See [File functions](File) for the reference.
* Consider simplier save state, more like checkpoints. If you can live without restoring literally everything to a smallest bit, maybe you can only save most important game variables, items that player possess, state of puzzles.
* Learn to describe game state using just few variables and restore game and rooms from these. For example, if your variable sais that "puzzle A is solved", you may know that Room Objects A and B should be invisible, item C in player's inventory, and NPC character D moved to room 2. Such approach allows to rebuild game in script just from a few variables restored from a custom file. But of course you have to plan this ahead well.

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

int GameVersion;
int MyVariables[];

function game_start() {
    GameVersion = 2;
    MyVariables = new int[GAME_VER_002_LENGTH];
}

function on_event(EventType evt, int data) {
    if (evt == eEventRestoreGame) {
        // detect old save
        if (GameVersion == 1) {
            // allocate bigger array suited for latest version of the game
            int new_vars[] = new int[GAME_VER_002_LENGTH];
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
            GameVersion = 2;
        }
    }
}
</pre>

Similar solution may be used for managed structs, although it may be bit more complicated to script but essentially is same thing.
<pre>
managed struct MyStruct {
    // variables from version 1
    int a;
    int b;
    // variables from version 2
    int c;
    int d;
}

int GameVersion;
MyStruct MyObj;

function game_start() {
    GameVersion = 2;
    MyObj = new MyStruct;
}

function on_event(EventType evt, int data) {
    if (evt == eEventRestoreGame) {
        // detect old save
        if (GameVersion == 1) {
            // allocate new managed object suited for latest version of the game
            MyStruct new_obj = new MyStruct;
            // copy restored object with old data into our new object
            new_obj.a = MyObj.a;
            new_obj.b = MyObj.b;
            // set default values for the rest (replace with your code as appropriate)
            new_obj.c = 0;
            new_obj.d = 0;
            // finally replace pointer and version number
            MyObj = new_obj;
            GameVersion = 2;
        }
    }
}
</pre>

### Solution 5: Dictionary and Set

Since AGS 3.5.0 there's also a [Dictionary](Dictionary) and [Set](Set) types. Those may serve as an easier alternative to extending dynamic arrays or managed structs in this solution. It's easy to check which variables (keys) they contain. You can even store "game version" inside as one of the elements. They may be used as a universal global storage, for example, for story variables, expanding them between game updates.
