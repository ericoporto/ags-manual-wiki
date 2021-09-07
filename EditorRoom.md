## Room Editor

The Room Editor is where you can define the various properties and data that
make up a room. This includes:

- Objects
- Hotspots
- Walkable areas
- Walkbehinds
- Regions
- ...and more!

**NOTE:** Currently only one room can be open for editing at a time

![Editor Room](images/EditorRoom_1.png)

### Background

By selecting a background on the `Display Background` combo box, you can select
which background of a room to display: Main Background, frame 2, 3, 4, 5. With
one background selected, click `Change...` button to replace the background
image with a new image. If a room has more than one background, by default, they
are animated.

**NOTE:** If the background images are replaced with ones of a different size
this will clear all of the mask (hotspot, walkbehind, region, and walkable)
areas which have been are defined so far.

### Edit this room's control

This control allows you to view characters, objects, and edges, simultaneously
along with one of the room masks: hotspots, walkable areas, walk-behinds or
regions. Moving a character or object already in the room is done by clicking
and dragging it.

![Editor Room](images/EditorRoom_2.png)

You can select any element in the room by navigating on the bar using the down
arrows, which will reveal the available elements of the chosen category.

Characters and objects can also be selected directly in the room, by clicking on
them, as long as the corresponding layer is active.

To select any mask-type layer, first select the layer you are interested and
then use the Select area tool (picker icon on toolbar) to pick the specific
element.

**Placing a new object**

If you want to place a new object, you can do so by selecting Objects in the
layer menu and right clicking on the screen where you would like to create it. A
new context menu should open and you can choose the option "Place New Object
Here".

![Editor Room](images/EditorRoom_3.png)

**Placing a character**

Characters will only be shown if this room is their 'starting room'. You can
modify this by expanding the "Characters" node in the Explore Project tree, and
configuring the property `StartingRoom` for a particular character.

**Layer and element Visibility (eye icon)**

Each layer can be made visible/hidden by toggling its visibility button on and
off. In addition, for the object, character, and edge layers, each element in
the layer can also be made be hidden in the same way.

**NOTE:** This will only affect the editor, not the actual game

**Layer and element Locking (padlock icon)**

Each layer can be locked/unlocked by by toggling its locking button. In
addition, for each layer, each element in the layer can also be locked/unlocked
in a similar way. A locked element cannot be moved until it is unlocked, this is
useful to prevent accidentally moving something when designing the room.

**NOTE:** This will only affect the editor, not the actual game

### Properties control

The properties control will adapt to whichever element is selected on the
current layer. If no element is selected or the edges layer is selected, this
control will show the current Room properties and events.

The list button switches the control to show **Properties** and the button with
a lighting bolt on it switches the control to show **Events**. Both can be
navigated either in categorical order or alphabetical order.

Positional changes on the properties of an element (e.g. its x or y position)
will instantly be updated in the room area, which is useful for pixel
positioning.

### Edges

Edges are moved by clicking and dragging them, once their layer is selected. If
you have trouble locating them, the properties which correspond to each edge's
position are:

- `TopEdgeY`
- `BottomEdgeY`
- `LeftEdgeX`
- `RightEdgeX`

### Objects

As described above, right clicking on the room when the Object layer is active
allows you to create a new object. Objects can be freely positioned in the room,
and whilst an object is selected you can edit its properties within the
Properties control. While dragging an Object its x and y position will be shown
on screen. The anchor point for positioning is the object's bottom left corner.

### Characters

As described above, a character will only be available to show in a room if the
character is configured to start in this room. Whilst dragging a Character its
x and y position will be shown on screen. The anchor point for positioning is
at the bottom-middle point of the character - the position should roughly match
the middle of the characters feet.

### Room masks (Hotspot, Walkable areas, Walk-behinds and Regions)

AGS offers a simple drawing editor when one of these layers is selected, so that
you can directly edit these mask areas. The tools offered include a picker, a
line tool, a freehand tool, a rectangle tool, and an area fill tool.

Also available is a way to import and export all mask areas as a bitmap image.
These options are offered in-case you prefer to draw these areas in your
preferred external image editor.

**NOTE:** Mask images must be using a 16-color (4-bit) or 256-color (8-bit)
indexed color palette, where color 0 signifies transparency and colors 1-15 are
used as the respective hotspot/walk-behind/walkable area numbers

*See also:* [`Room`](Room)
