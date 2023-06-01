Inventory items represent things that a character may acquire and use: a physical object, an idea, a useable skill, and so forth, depending on game mechanics that you want to have. Each character in the game has their own overall "inventory" which is the set of items or skills they are carrying. They can be made visible in the game, or simply work behind the scenes.

In technical terms, inventory items are a built-in game object with a built-in corresponding script class.

Each inventory item has:

* a unique script name, used to refer to this item in scripts; (required)
* a textual name, for describing it to player;
* a graphic, for displaying it on screen;
* a cursor graphic, for setting a cursor when the item is selected.

What can you do with an inventory item?
* add it to a character's inventory
* display it in a character's inventory using a GUI (this can be done with the built-in Inventory Window, a list box, or a custom GUI).
* make the item "active" (selected for use by the player)
* use the item  on game components such as hotspots, room objects, characters, and other inventory items
* remove the item from a character's inventory

In the game script, character own "copies" or instances of inventory items, so any character may possess any number or amount of any particular item. Using or removing an item affects only the specific copy of the item referred to. Other copies of the item remain, and new copies can be created, re-added to a character's inventory, re-activated, or re-used whenever the game requires.

