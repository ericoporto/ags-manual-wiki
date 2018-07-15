Character functions and properties
----------------------------------

[AddInventory](#Character.AddInventory)\
[AddWaypoint](#Character.AddWaypoint)\
[Animate (character)](#Character.Animate)\
[ChangeRoom](#Character.ChangeRoom)\
[ChangeRoomAutoPosition](#Character.ChangeRoomAutoPosition)\
[ChangeView](#Character.ChangeView)\
[FaceCharacter](#Character.FaceCharacter)\
[FaceDirection](#Character.FaceDirection)\
[FaceLocation](#Character.FaceLocation)\
[FaceObject](#Character.FaceObject)\
[FollowCharacter](#Character.FollowCharacter)\
[GetAtScreenXY (character)](#Character.GetAtScreenXY)\
[GetProperty (character)](#Character.GetProperty)\
[GetTextProperty (character)](#Character.GetTextProperty)\
[SetProperty (character)](#Character.SetProperty)\
[SetTextProperty (character)](#Character.SetTextProperty)\
[HasExplicitLight property (character)](#Character.HasExplicitLight)\
[HasInventory](#Character.HasInventory)\
[IsCollidingWithChar](#Character.IsCollidingWithChar)\
[IsCollidingWithObject (character)](#Character.IsCollidingWithObject)\
[LightLevel property](#Character.LightLevel)\
[LockView](#Character.LockView)\
[LockViewAligned](#Character.LockViewAligned)\
[LockViewFrame](#Character.LockViewFrame)\
[LockViewOffset](#Character.LockViewOffset)\
[LoseInventory](#Character.LoseInventory)\
[Move (character)](#Character.Move)\
[PlaceOnWalkableArea](#Character.PlaceOnWalkableArea)\
[RemoveTint (character)](#Character.RemoveTint)\
[IsInteractionAvailable (character)](#Character.IsInteractionAvailable)\
[RunInteraction (character)](#Character.RunInteraction)\
[Say](#Character.Say)\
[SayAt](#Character.SayAt)\
[SayBackground](#Character.SayBackground)\
[SetAsPlayer](#Character.SetAsPlayer)\
[SetLightLevel (character)](#Character.SetLightLevel)\
[SetIdleView](#Character.SetIdleView)\
[SetWalkSpeed](#Character.SetWalkSpeed)\
[StopMoving (character)](#Character.StopMoving)\
[Think](#Character.Think)\
[Tint (character)](#Character.Tint)\
[TintBlue property (character)](#Character.TintBlue)\
[TintGreen property (character)](#Character.TintGreen)\
[TintRed property (character)](#Character.TintRed)\
[TintSaturation property (character)](#Character.TintSaturation)\
[TintLuminance property (character)](#Character.TintLuminance)\
[UnlockView](#Character.UnlockView)\
[Walk](#Character.Walk)\
[WalkStraight](#Character.WalkStraight)\
[ActiveInventory property](#Character.ActiveInventory)\
[Animating property (character)](#Character.Animating)\
[AnimationSpeed property](#Character.AnimationSpeed)\
[Baseline property (character)](#Character.Baseline)\
[BlinkInterval property](#Character.BlinkInterval)\
[BlinkView property](#Character.BlinkView)\
[BlinkWhileThinking property](#Character.BlinkWhileThinking)\
[BlockingHeight property (character)](#Character.BlockingHeight)\
[BlockingWidth property (character)](#Character.BlockingWidth)\
[Clickable property (character)](#Character.Clickable)\
[DestinationX property](#Character.DestinationX)\
[DestinationY property](#Character.DestinationY)\
[DiagonalLoops property](#Character.DiagonalLoops)\
[Frame property (character)](#Character.Frame)\
[HasExplicitTint property (character)](#Character.HasExplicitTint)\
[ID property (character)](#Character.ID)\
[IdleView property](#Character.IdleView)\
[IgnoreLighting property](#Character.IgnoreLighting)\
[IgnoreWalkbehinds property (character)](#Character.IgnoreWalkbehinds)\
[InventoryQuantity property](#Character.InventoryQuantity)\
[Loop property (character)](#Character.Loop)\
[ManualScaling property (character)](#Character.ManualScaling)\
[MovementLinkedToAnimation
property](#Character.MovementLinkedToAnimation)\
[Moving property (character)](#Character.Moving)\
[Name property (character)](#Character.Name)\
[NormalView property](#Character.NormalView)\
[PreviousRoom property](#Character.PreviousRoom)\
[Room property](#Character.Room)\
[ScaleMoveSpeed property](#Character.ScaleMoveSpeed)\
[ScaleVolume property](#Character.ScaleVolume)\
[Scaling property (character)](#Character.Scaling)\
[Solid property (character)](#Character.Solid)\
[Speaking property](#Character.Speaking)\
[SpeakingFrame property](#Character.SpeakingFrame)\
[SpeechAnimationDelay property](#Character.SpeechAnimationDelay)\
[SpeechColor property](#Character.SpeechColor)\
[SpeechView property](#Character.SpeechView)\
[Thinking property](#Character.Thinking)\
[ThinkingFrame property](#Character.ThinkingFrame)\
[ThinkView property](#Character.ThinkView)\
[Transparency property (character)](#Character.Transparency)\
[TurnBeforeWalking property](#Character.TurnBeforeWalking)\
[View property (character)](#Character.View)\
[WalkSpeedX property](#Character.WalkSpeedX)\
[WalkSpeedY property](#Character.WalkSpeedY)\
[x property (character)](#Character.x)\
[y property (character)](#Character.y)\
[z property (character)](#Character.z)\
[SetCharacterProperty](#SetCharacterProperty)

---

### AddInventory

*(Formerly known as global function AddInventory, which is now
obsolete)*\
*(Formerly known as global function AddInventoryToCharacter, which is
now obsolete)*

    Character.AddInventory(InventoryItem *item, optional int addAtIndex)

Adds the specified item to the character's inventory. This ensures that
the item gets added to the character's inventory list, and that any
on-screen inventory display gets updated if appropriate.

The first parameter is the inventory item's Script O-Name from the
editor (for example, *iPoster*).

By default, the new item is added to the end of the character's
inventory list. However, you can insert it in a particular position in
the list by supplying the second parameter. The new item is inserted
*before* the current item at *addAtIndex*. Indexes are numbered from 0,
so to add the item at the start of the list, pass 0 as the second
parameter.

Example:

    cEgo.AddInventory(iKey);

will give inventory item iKey to character EGO.

*See Also:* [Character.HasInventory](ags47#Character.HasInventory),
[Character.LoseInventory](ags47#Character.LoseInventory),
[UpdateInventory](ags54#UpdateInventory)

---

### AddWaypoint

*(Formerly known as MoveCharacterPath, which is now obsolete)*

    Character.AddWaypoint(int x, int y)

Tells the character to move to (X,Y) directly, after it has finished its
current move. This function allows you to queue up a series of moves for
the character to make, if you want them to take a preset path around the
screen. Note that any moves made with this command ignore walkable
areas.

This is useful for situations when you might want a townsperson to
wander onto the screen from one side, take a preset route around it and
leave again.

Example:

    cSomeguy.Walk(160, 100);
    cSomeguy.AddWaypoint(50, 150);
    cSomeguy.AddWaypoint(50, 50);

tells character SOMEGUY to first of all walk to the centre of the screen
normally (obeying walkable areas), then move to the bottom left corner
and then top left corner afterwards.

*See Also:* [Character.Move](ags47#Character.Move)
[Character.Walk](ags47#Character.Walk)

---

### Animate (character)

*(Formerly known as AnimateCharacter, which is now obsolete)*\
*(Formerly known as AnimateCharacterEx, which is now obsolete)*

    Character.Animate(int loop, int delay, optional RepeatStyle,
                      optional BlockingStyle, optional Direction)

Starts the character animating, using loop number LOOP of his current
view. The overall speed of the animation is set with DELAY, where 0 is
the fastest, and increasing numbers mean slower. The delay for each
frame is worked out as DELAY + FRAME SPD, so the individual frame speeds
are relative to this overall speed.

Before using this command, you should use
[LockView](ags47#Character.LockView) in order to select the view you
want to animate with and prevent any automatic animations (eg. walking
or idle animations) from playing.

The *RepeatStyle* parameter sets whether the animation will continuously
repeat the cycling through the frames. This can be *eOnce* (or zero), in
which case the animation will start from the first frame of LOOP, and go
through each frame in turn until the last frame, where it will stop. If
RepeatStyle is *eRepeat* (or 1), then when the last frame is reached, it
will go back to the first frame and start over again with the animation.

*direction* specifies which way the animation plays. You can either pass
eForwards (the default) or eBackwards.

For *blocking* you can pass either eBlock (in which case the function
will wait for the animation to finish before returning), or eNoBlock (in
which case the animation will start to play, but your script will
continue). The default is eBlock.

If the character is currently moving, it will be stopped.

Example:

    cEgo.LockView(5);
    cEgo.Animate(3, 1, 0, eBlock, eBackwards);
    cEgo.UnlockView();

will animate the character once using loop number 3 of view 5 backwards,
and wait until the animation finishes before returning.

*See Also:* [Object.Animate](ags68#Object.Animate)

---

### ChangeRoom

*(Formerly known as NewRoom, which is now obsolete)*\
*(Formerly known as NewRoomEx, which is now obsolete)*\
*(Formerly known as NewRoomNPC, which is now obsolete)*

    Character.ChangeRoom(int room_number, optional int x, optional int y, optional CharacterDirection direction)

Changes the room that the character is in.

If you call this on the player character, then the game will move into
the new room with them.

**IMPORTANT:** This command does not change the room immediately;
instead, it will perform the actual room change once your script
function has finished (This is to avoid problems with unloading the
script while it is still running). This means that you should not use
any other commands which rely on the new room (object positionings, and
so on) after this command within the same function.

If you call this on a non-player character, then they are instantly
transported to the new room number.

Optionally, you can include an X and Y co-ordinate (you must include
either both or neither). If you do so, then the character will also be
moved to the specified co-ordinates in the new room.

Optionally, you can also include direction parameter, that determines
which direction this character will be facing after room change.

Example:

    player.ChangeRoom(4, 100, 50, eDirectionRight);

will move the player character to room 4 and also place him at
coordinates 100,50. This will also mean that the game moves into room 4.

*Compatibility:* Optional *direction* parameter is supported only by
**AGS 3.4.0** and later versions.

*See Also:*
[Character.ChangeRoomAutoPosition](ags47#Character.ChangeRoomAutoPosition)

---

### ChangeRoomAutoPosition

    Character.ChangeRoomAutoPosition(int room_number, optional int newPosition)

Changes the room that the character is in, and positions him along one
of the room edges.

This command simulates the behaviour of the old "Go to room" interaction
command from AGS 2.72 and previous versions. If *newPosition* is not
specified or is 0, the character will be placed on the opposite side of
the new room, if he is within 10 pixels of a room edge in the current
room.

Altenatively, you can specify the position where he will get placed in
the new room. *newPosition* can be 1000 for the left edge, 2000 for the
right edge, 3000 for the bottom edge and 4000 for the top edge. Then,
add on the offset within that edge where you want to place the
character, in normal room co-ordinates.

**IMPORTANT:** This command does not change the room immediately;
instead, it will perform the actual room change once your script
function has finished (This is to avoid problems with unloading the
script while it is still running). This means that you should not use
any other commands which rely on the new room (object positionings, and
so on) after this command within the same function.

**NOTE:** This command can only be used with the player character.

Example:

    player.ChangeRoomAutoPosition(4, 2100);

will move the player character to room 4 and place him half way down the
right hand side of the screen. This will also mean that the game moves
into room 4.

*See Also:* [Character.ChangeRoom](ags47#Character.ChangeRoom)

---

### ChangeView

*(Formerly known as ChangeCharacterView, which is now obsolete)*

    Character.ChangeView(int view)

Changes the normal view number of the character to *view*. This is
useful if, for example, you want the character to change the clothes
they are wearing, and so permanently alter their view number.

**NOTE:** This command is **not** intended to change the view
temporarily to perform an animation. If you want to do that, use the
LockView command instead. This ChangeView command permanently changes
the character's normal walking view.

Example:

    cEgo.ChangeView(5);

will make the EGO character use view number 5 as his walking view.

*See Also:* [Character.LockView](ags47#Character.LockView),
[Character.NormalView](ags47#Character.NormalView)

---

### FaceCharacter

*(Formerly known as global function FaceCharacter, which is now
obsolete)*

    Character.FaceCharacter(Character* toFace, optional BlockingStyle)

Turns the graphic of the character so that it looks like he is facing
character TOFACE. This involves changing the current loop to the
appropriate loop number, and setting the frame number to 0 (standing).

If the character has Turning enabled (ie. the "Characters turn to face
direction" game option is turned on, and the character does not have the
"Do not turn before walking" option checked), then the character will
turn on the spot in order to face the new direction. In this case, the
BlockingStyle parameter determines whether the script waits for the
character to finish turning (eBlock, the default) or whether the script
continues immediately and the character finishes turning later on
(eNoBlock).

If the character does not have Turning enabled, he will immediately turn
to face the new direction and the BlockingStyle parameter has no effect.
In this case, the screen will not be refreshed straight away -- if you
want to see the character facing his new direction immediately, call
Wait(1);

Example:

    cEgo.FaceCharacter(cMan);

will make the character EGO face the character MAN

*See Also:*
[Character.FaceDirection](ags47#Character.FaceDirection),
[Character.FaceLocation](ags47#Character.FaceLocation),
[Character.FaceObject](ags47#Character.FaceObject),
[Character.Walk](ags47#Character.Walk)

---

### FaceDirection

    Character.FaceDirection(CharacterDirection direction, BlockingStyle=eBlock)

Turns the graphic of the character so that it looks like he is facing
direction *direction*. This involves changing the current loop to the
appropriate loop number, and setting the frame number to 0 (standing).

If the character has Turning enabled (ie. the "Characters turn to face
direction" game option is turned on, and the character does not have the
"Do not turn before walking" option checked), then the character will
turn on the spot in order to face the new direction. In this case, the
BlockingStyle parameter determines whether the script waits for the
character to finish turning (eBlock, the default) or whether the script
continues immediately and the character finishes turning later on
(eNoBlock).

If the character does not have Turning enabled, he will immediately turn
to face the new direction and the BlockingStyle parameter has no effect.
In this case, the screen will not be refreshed straight away -- if you
want to see the character facing his new direction immediately, call
Wait(1);

Example:

    cEgo.FaceDirection(eDirectionUpRight);

will make the character EGO face up-right.

*Compatibility:* Supported by **AGS 3.4.0** and later versions.

*See Also:*
[Character.FaceCharacter](ags47#Character.FaceCharacter),
[Character.FaceLocation](ags47#Character.FaceLocation),
[Character.FaceObject](ags47#Character.FaceObject),
[Character.Walk](ags47#Character.Walk)

---

### FaceLocation

*(Formerly known as global function FaceLocation, which is now
obsolete)*

    Character.FaceLocation(int x, int y, optional BlockingStyle)

Similar to the FaceCharacter function, except that this faces the
character to room co-ordinates (X,Y). This allows him to face not only
other characters, but also hotspots or anything else as well (you can
get co-ordinates by watching the co-ordinates displayed in the Room
Settings mode as you move the mouse over the room background).

If the character has Turning enabled (ie. the "Characters turn to face
direction" game option is turned on, and the character does not have the
"Do not turn before walking" option checked), then the character will
turn on the spot in order to face the new direction. In this case, the
BlockingStyle parameter determines whether the script waits for the
character to finish turning (eBlock, the default) or whether the script
continues immediately and the character finishes turning later on
(eNoBlock).

If the character does not have Turning enabled, he will immediately turn
to face the new direction and the BlockingStyle parameter has no effect.
In this case, the screen will not be refreshed straight away -- if you
want to see the character facing his new direction immediately, call
Wait(1);

Example:

    cEgo.FaceLocation(cEgo.x + 50, cEgo.y);

will make the character face to the east.

*See Also:*
[Character.FaceCharacter](ags47#Character.FaceCharacter),
[Character.FaceDirection](ags47#Character.FaceDirection),
[Character.FaceObject](ags47#Character.FaceObject),
[Character.Walk](ags47#Character.Walk)

---

### FaceObject

    Character.FaceObject(Object* object, optional BlockingStyle)

Similar to the FaceCharacter function, except that this faces the
character to object OBJECT in the current room.

If the character has Turning enabled (ie. the "Characters turn to face
direction" game option is turned on, and the character does not have the
"Do not turn before walking" option checked), then the character will
turn on the spot in order to face the new direction. In this case, the
BlockingStyle parameter determines whether the script waits for the
character to finish turning (eBlock, the default) or whether the script
continues immediately and the character finishes turning later on
(eNoBlock).

If the character does not have Turning enabled, he will immediately turn
to face the new direction and the BlockingStyle parameter has no effect.
In this case, the screen will not be refreshed straight away -- if you
want to see the character facing his new direction immediately, call
Wait(1);

Example:

    player.FaceObject(object[2]);

will make the player character face object 2.

*See Also:*
[Character.FaceCharacter](ags47#Character.FaceCharacter),
[Character.FaceDirection](ags47#Character.FaceDirection),
[Character.FaceLocation](ags47#Character.FaceLocation),
[Character.Walk](ags47#Character.Walk)

---

### FollowCharacter

*(Formerly known as global function FollowCharacter, which is now
obsolete)*\
*(Formerly known as global function FollowCharacterEx, which is now
obsolete)*

    Character.FollowCharacter(Character* chartofollow, optional int dist,
                              optional int eagerness)

Tells the character to follow CHARTOFOLLOW around, wherever he goes. You
could use this command to have a group of main characters who go around
together, or for example when the hero has rescued someone from the bad
guy, they can follow the hero home.

Pass CHARTOFOLLOW as *null* to stop the character following.

There are a couple of extra optional parameters:

DIST sets how far away from CHARTOFOLLOW that CHARID will stand. If DIST
is 1, they will try to stand very close; if DIST is for example 20, they
will stand about 20 pixels away.

EAGERNESS sets on average how long the character will stand around
before checking if he needs to move again. Setting this to 0 means that
he will always be on the move until he reaches CHARTOFOLLOW; setting
this to 99 means that he will pause and think for a while on route.
Values in between specify different lengths of idle time.

The default values are DIST=10 and EAGERNESS=97.

As a special case, setting DIST=0 and EAGERNESS=0 makes CHARID behave as
if it is chasing CHARTOFOLLOW - it will try and get there as quickly as
possible. Setting EAGERNESS=0 also tells the character not to stop when
they reach CHARTOFOLLOW, but instead to randomly wander around the
character - useful perhaps for a very energetic dog or something.

There is also another special use for this command. You can pass the
special value FOLLOW\_EXACTLY as the DIST parameter rather than passing
a number. If you do this, then CHARID will always remain at exactly the
same X and Y co-ordinates as CHARTOFOLLOW. This might be useful for
effects such as a temporary halo over the character and so forth.

If you use FOLLOW\_EXACTLY, then EAGERNESS has another meaning. If you
pass 0, CHARID will be drawn in front of CHARTOFOLLOW; if you pass 1, it
will be drawn behind.

Example:

    cMan.FollowCharacter(cEgo, 5, 80);

will make character MAN follow character EGO standing about 5 pixels
near him and waiting for a while before he makes his move.

---

### GetAtScreenXY (character)

*(Formerly known as global function GetCharacterAt, which is now
obsolete)*

    static Character* Character.GetAtScreenXY(int x, int y)

Checks if there is a character at SCREEN co-ordinates (X,Y). Returns the
character if there is, or null if there is not. See the description of
GetLocationName for more on screen co-ordinates.

NOTE: Any characters with the "Clickable" property set to false will not
be seen by this function.

Example:

    if (Character.GetAtScreenXY(mouse.x, mouse.y) == cEgo) {
      Display("The mouse is over the main character");
    }

will display the message if the mouse cursor is over the EGO character

*See Also:* [Hotspot.GetAtScreenXY](ags63#Hotspot.GetAtScreenXY),
[Object.GetAtScreenXY](ags68#Object.GetAtScreenXY),
[Game.GetLocationName](ags54#Game.GetLocationName)

---

### GetProperty (character)

*(Formerly known as GetCharacterProperty, which is now obsolete)*

    Character.GetProperty(string property)

Returns the custom property setting of the PROPERTY for the specified
character.

This command works with Number properties (it returns the number), and
with Boolean properties (returns 1 if the box was checked, 0 if not).

Use the equivalent GetTextProperty function to get a text property.

Example:

    if (cEgo.GetProperty("Value") > 200)
      Display("EGO's value is over 200!");

will print the message if EGO has its "Value" property set to more than
200.

*See Also:*
[Character.GetTextProperty](ags47#Character.GetTextProperty)

---

### GetTextProperty (character)

*(Formerly known as GetCharacterPropertyText, which is now obsolete)*\
*(Formerly known as Character.GetPropertyText, which is now obsolete)*

    String Character.GetTextProperty(string property)

Returns the custom property setting of the PROPERTY for the specified
character.

This command works with Text properties only. The property's text will
be returned from this function.

Use the equivalent GetProperty function to get a non-text property.

Example:

    String description = cEgo.GetTextProperty("Description");
    Display("EGO's description: %s", description);

will retrieve EGO's "description" property and display it.

*See Also:* [Character.GetProperty](ags47#Character.GetProperty)

---

### SetProperty (character)

    bool Character.SetProperty(const string property, int value)

Sets the new *value* for the custom *property* for the specified
character. Returns TRUE if such property exists and FALSE on failure.

This command works with Number properties (it sets the numeric value),
and with Boolean properties (sets FALSE is value is equal to 0, or TRUE
otherwise).

Use the equivalent SetTextProperty function to set new text property
value.

Example:

    cEgo.SetProperty("XPLevel", 10);

will change EGO character's "XPLevel" custom property to 10.

*Compatibility:* Supported by **AGS 3.4.0** and later versions.

*See Also:*
[Character.SetTextProperty](ags47#Character.SetTextProperty)

---

### SetTextProperty (character)

    bool Character.SetTextProperty(const string property, const string value)

Sets the new *value* text for the custom *property* for the specified
character. Returns TRUE if such property exists and FALSE on failure.

This command works with Text properties only. The property's text will
be changed to new value.

Use the equivalent SetProperty function to set a non-text property.

Example:

    cEgo.SetTextProperty("Description", "I am handsome!");

will change EGO's "description" property.

*Compatibility:* Supported by **AGS 3.4.0** and later versions.

*See Also:* [Character.SetProperty](ags47#Character.SetProperty)

---

### HasExplicitLight property (character)

    readonly bool Character.HasExplicitTint

Returns *true* if the character has a light set explicitly with the
[Character.SetLightLevel](ags47#Character.SetLightLevel) command.

Returns *false* if the character has no explicit light level, but it may
still be lighted by
[SetAmbientLightLevel](ags54#SetAmbientLightLevel) or a region
light.

*Compatibility:* Supported by **AGS 3.4.1** and later versions.

*SeeAlso:* [Character.SetLightLevel](ags47#Character.SetLightLevel)

---

### HasInventory

    bool Character.HasInventory(InventoryItem *item)

Checks whether the character currently has the specified inventory item.
Returns *true* if they do, or *false* if they don't.

The parameter is the inventory item's Script O-Name from the editor (for
example, *iPoster*).

Example:

    if (player.HasInventory(iKey))
    {
      Display("The player has the key!!");
    }

will display a message if the player has the key.

*Compatibility:* Supported by **AGS 3.1.0** and later versions.

*See Also:* [Character.AddInventory](ags47#Character.AddInventory),
[Character.InventoryQuantity](ags47#Character.InventoryQuantity),
[Character.LoseInventory](ags47#Character.LoseInventory)

---

### IsCollidingWithChar

*(Formerly known as AreCharactersColliding, which is now obsolete)*

    Character.IsCollidingWithChar(Character* otherChar)

Checks if the character is touching OTHERCHAR. This function just checks
the baseline of both characters, so if one is standing a fair distance
behind the other, it will not be marked as colliding.

Returns 1 if the characters feet are touching, 0 otherwise.

Example:

    if (cEgo.IsCollidingWithChar(cMan) == 1)
       { colliding code here }

will execute the colliding code only if the characters EGO and MAN are
colliding.

*See Also:*
[Character.IsCollidingWithObject](ags47#Character.IsCollidingWithObject),
[Object.IsCollidingWithObject](ags68#Object.IsCollidingWithObject),
[AreThingsOverlapping](ags73#AreThingsOverlapping)

---

### IsCollidingWithObject (character)

*(Formerly known as AreCharObjColliding, which is now obsolete)*

    Character.IsCollidingWithObject(Object* obj)

Checks whether the character's feet (ie. the bottom third of the
character) are touching OBJ. This can be used to determine if the
character is standing on the object.

Returns 1 if they are, and 0 if they are not.

Example:

    if (cEgo.IsCollidingWithObject(object[3]) == 1) {
      // colliding code here
    }

will execute the colliding code only if the character EGO and the object
number 3 are colliding.

*See Also:*
[Character.IsCollidingWithChar](ags47#Character.IsCollidingWithChar),
[Object.IsCollidingWithObject](ags68#Object.IsCollidingWithObject),
[AreThingsOverlapping](ags73#AreThingsOverlapping)

---

### LightLevel property

    readonly int Character.LightLevel

If the character has an individual light set explicitly with the
[Character.SetLightLevel](ags47#Character.SetLightLevel) command,
this property returns the light level value. Otherwise it returns 0.

**NOTE:** without individual light level set, Character.LightLevel
returns 0 even if the character is affected by the ambient or region's
light.

*Compatibility:* Supported by **AGS 3.4.1** and later versions.

*SeeAlso:* [Character.SetLightLevel](ags47#Character.SetLightLevel),
[SetAmbientLightLevel](ags54#SetAmbientLightLevel)

---

### LockView

*(Formerly known as SetCharacterView, which is now obsolete)*

    Character.LockView(int view, optional StopMovementStyle)

Sets the character's view to VIEW. This can be used to perform
animations with characters, for example bending down to pick something
up, which don't use the default view.

*StopMovementStyle* determines what to do if character was moving when
this function is called. You can pass either eStopMoving (in which case
the walking character will stop), or eKeepMoving (in which case the
character will keep moving). The default is eStopMoving.

**NOTE:** This function locks the character's view to the specified
view, so that it can only be changed by other script commands (ie. it
won't automatically be changed by AGS on walkable areas, screen changes,
etc). When you are done with the animation, call UnlockView to allow AGS
to take control back.

Example:

    cEgo.LockView(12);
    cEgo.Animate(0, 0, eOnce, eBlock, eForwards);
    cEgo.UnlockView();

will change the character's EGO view to view 12, perform an animation
using loop 0, wait until the animation finishes and then return the
character to his normal view.

*Compatibility:* Optional *StopMovementStyle* parameter is supported
only by **AGS 3.4.1** and later versions.

*See Also:* [Character.Animate](ags47#Character.Animate),
[Character.ChangeView](ags47#Character.ChangeView),
[Character.SpeechView](ags47#Character.SpeechView),
[Character.LockViewAligned](ags47#Character.LockViewAligned),
[Character.LockViewOffset](ags47#Character.LockViewOffset)
[Character.UnlockView](ags47#Character.UnlockView),

---

### LockViewAligned

*(Formerly known as SetCharacterViewEx, which is now obsolete)*

    Character.LockViewAligned(int view, int loop, Alignment, optional StopMovementStyle)

Sets the character's view to VIEW, and sets the character's current
frame to the first frame in LOOP of VIEW.

The main purpose of this command is that it can align the new frame to
the previous one. This is particularly useful if you want to go from the
character's normal walking view to a specific animation - since
characters have the central point as their 'axis', if you have a wider
animation then it can be difficult to stop yourself getting a jumping
effect when the animation starts.

*Alignment* can have one of the following values:

---
  **align**      **Description**
  eAlignLeft     Moves the new frame so that the left hand side is at exactly the same X co-ordinate as the old one was.
  eAlignCentre   Leaves the frames centred in the middle. This is the default and using this is equivalent to just calling LockView.
  eAlignRight    Moves the new frame so that the right hand side is at exactly the same X co-ordinate as the old one was.
---

Note that this only aligns the first frame of the animation, so to get
the full benefit all your frames in the animation loop should be the
same width. All following frames will be shifted by the same amount,
until UnlockView is called.

*StopMovementStyle* determines what to do if character was moving when
this function is called. You can pass either eStopMoving (in which case
the walking character will stop), or eKeepMoving (in which case the
character will keep moving). The default is eStopMoving.

**NOTE:** This function locks the character's view to the specified
view, so that it can only be changed by other script commands (ie. it
won't automatically be changed by the program on regions, screen
changes, etc). When you are done with the animation, call UnlockView to
allow the program to take control back.

Example:

    cEgo.LockViewAligned(12, 1, eAlignLeft);
    cEgo.Animate(1, 5, eOnce, eBlock, eForwards);
    cEgo.UnlockView();

will change the character's EGO view to view 12, perform an animation
using loop 1, wait until the animation finishes and then return the
character to his normal view.

*Compatibility:* Optional *StopMovementStyle* parameter is supported
only by **AGS 3.4.1** and later versions.

*See Also:* [Character.LockView](ags47#Character.LockView),
[Character.LockViewOffset](ags47#Character.LockViewOffset),
[Character.UnlockView](ags47#Character.UnlockView)

---

### LockViewFrame

*(Formerly known as SetCharacterFrame, which is now obsolete)*

    Character.LockViewFrame(int view, int loop, int frame, optional StopMovementStyle)

Sets the character's graphic to frame FRAME of loop LOOP of view number
VIEW. This is useful if you don't want an animation, but just want to
change the character to display a specific frame.

The frame will be locked to the one you specify until you call
UnlockView.

*StopMovementStyle* determines what to do if character was moving when
this function is called. You can pass either eStopMoving (in which case
the walking character will stop), or eKeepMoving (in which case the
character will keep moving). The default is eStopMoving.

Example:

    cEgo.LockViewFrame(AGHAST, 2, 4);
    Wait(40);
    cEgo.UnlockView();

will change EGO to have frame 4 of loop 2 in the AGHAST view, wait for a
second, then return him to normal.

*Compatibility:* Optional *StopMovementStyle* parameter is supported
only by **AGS 3.4.1** and later versions.

*See Also:* [Character.Animate](ags47#Character.Animate),
[Character.LockView](ags47#Character.LockView),
[Character.UnlockView](ags47#Character.UnlockView)

---

### LockViewOffset

*(Formerly known as SetCharacterViewOffset, which is now obsolete)*

    Character.LockViewOffset(int view, int xOffset, int yOffset, optional StopMovementStyle)

Sets the character's view to VIEW, in the same way as LockView does.
However, it also adds a specified offset to all the character's frames
until UnlockView is called.

The XOFFSET and YOFFSET parameters specify **in actual game resolution
units** how much to move the character's sprite. Positive values for X
move right, for Y move down; negative values do the opposite.

This command is designed to allow you to cope with those niggly
situations where animations don't quite line up with the standing frame,
assuming all the frames of the animation are the same size. Note that
LockViewAligned is easier to use if your frames will align at the left
or right hand side.

*StopMovementStyle* determines what to do if character was moving when
this function is called. You can pass either eStopMoving (in which case
the walking character will stop), or eKeepMoving (in which case the
character will keep moving). The default is eStopMoving.

**NOTE:** You should only use this command for minor adjustments, since
the offsets do not affect the clickable area of the character, what
walkable area he is in, and so forth. You should limit the use of this
command to in-game cutscenes where the player has no control.

**NOTE:** This function locks the character's view to the specified
view, so that it can only be changed by other script commands (ie. it
won't automatically be changed by AGS on walkable areas, screen changes,
etc). When you are done with the animation, call UnlockView to allow AGS
to take control back.

Example:

    cEgo.LockViewOffset(12, 1, -1);
    cEgo.Animate(1, 5, eOnce, eBlock, eForwards);
    cEgo.UnlockView();

will change EGO's view to view 12 and animate using loop 1, meanwhile
all frames will be shifted 1 pixel right and 1 pixel up.

*Compatibility:* Optional *StopMovementStyle* parameter is supported
only by **AGS 3.4.1** and later versions.

*See Also:* [Character.LockView](ags47#Character.LockView),
[Character.LockViewAligned](ags47#Character.LockViewAligned),
[Character.UnlockView](ags47#Character.UnlockView)

---

### LoseInventory

*(Formerly known as global function LoseInventory, which is now
obsolete)*\
*(Formerly known as LoseInventoryFromCharacter, which is now obsolete)*

    Character.LoseInventory(InventoryItem *item)

Removes the specified inventory item from the character's inventory. If
they do not have the item, nothing happens.

The parameter is the inventory item's Script O-Name from the editor.

Example:

    cEgo.LoseInventory(iKey);

will make the character EGO lose the inventory item iKey from the
inventory tab

*See Also:* [Character.AddInventory](ags47#Character.AddInventory)

---

### Move (character)

    Character.Move(int x, int y, optional BlockingStyle,
                                 optional WalkWhere);

Starts the character moving from its current location to (X,Y), but does
not play the character's walking animation.

The parameters to this command are identical to the
[Character.Walk](ags47#Character.Walk) command -- see that page for
more details. The only difference is that *Walk* plays the walking
animation whereas *Move* does not.

In the vast majority of cases, you will use **Character.Walk** instead.

Example:

    cEgo.Move(155, 122, eBlock);

will make the character move to 155,122 without playing his walking
animation. The script will not continue until the character has reached
his destination.

*Compatibility:* Supported by **AGS 3.1.0** and later versions.

*See Also:* [Character.AddWaypoint](ags47#Character.AddWaypoint),
[Character.FaceCharacter](ags47#Character.FaceCharacter),
[Character.Walk](ags47#Character.Walk),
[MoveCharacterToObject](ags54#MoveCharacterToObject),
[Object.Move](ags68#Object.Move),
[Character.StopMoving](ags47#Character.StopMoving)

---

### PlaceOnWalkableArea

*(Formerly known as MoveToWalkableArea, which is now obsolete)*

    Character.PlaceOnWalkableArea()

Places the character in the nearest walkable area to its current
location. If the character is already on a walkable area, nothing
happens.

This is useful for example in the Player Enters Room event of a room, to
make sure the character can move if a ChangeRoom with co-ordinates has
been issued to get there. You could also use this in on\_event for
eEventEnterRoomBeforeFadein to use whenever a player enters a room.

Example:

    cEgo.x = Random(320);
    cEgo.y = Random(200);
    cEgo.PlaceOnWalkableArea();

will move character EGO to a random position but make sure that he is on
a walkable area.

---

### RemoveTint (character)

    Character.RemoveTint()

Undoes the effects of calling Tint, and returns the character to using
the room's ambient tint.

Example:

    player.Tint(0, 250, 0, 30, 100);
    Wait(40);
    player.RemoveTint();

will tint the player character green for a second, then turn it back to
normal.

*See Also:*
[Character.HasExplicitTint](ags47#Character.HasExplicitTint),
[Character.Tint](ags47#Character.Tint)

---

### IsInteractionAvailable (character)

    Character.IsInteractionAvailable(CursorMode)

Checks whether there is an event handler defined for activating the
character in cursor mode MODE.

This function is very similar to RunInteraction, except that rather than
run the event handler script function, it simply returns *true* if
something would have happened, or *false* if unhandled\_event would have
been run.

Example:

    if (cNPC.IsInteractionAvailable(eModeTalkto) == 0)
      Display("speaking with this character would not do anything.");

*Compatibility:* Supported by **AGS 3.4.0** and later versions.

*See Also:* [IsInteractionAvailable](ags54#IsInteractionAvailable),
[Character.RunInteraction](ags47#Character.RunInteraction)

---

### RunInteraction (character)

*(Formerly known as RunCharacterInteraction, which is now obsolete)*

    Character.RunInteraction(CursorMode)

Fires the event script as if the player had clicked the mouse on the
character in the specified cursor mode. This is one of the mouse cursor
modes, as defined in your Cursors tab in the editor.

Example:

    cMan.RunInteraction(eModeTalk);

will execute the code defined in the MAN's "TALK TO CHARACTER" event.

*See Also:* [Room.ProcessClick](ags73#Room.ProcessClick),
[Character.IsInteractionAvailable](ags47#Character.IsInteractionAvailable),
[Hotspot.RunInteraction](ags63#Hotspot.RunInteraction),
[InventoryItem.RunInteraction](ags64#InventoryItem.RunInteraction)

---

### Say

*(Formerly known as DisplaySpeech, which is now obsolete)*

    Character.Say(string message)

Displays the text MESSAGE as speech above the character's head. The text
will remain on screen for a limited time, and the user may or may not be
able to click it away depending on the setting of "Player can't skip
speech text". The text displayed by this function looks identical to
that used by the dialog system.

You can insert the value of variables into the message. For more
information, see the [string formatting](ags34#StringFormats)
section.

Example:

    cEgo.Say("My name is ego");

will display the message above the character's EGO head like the LEC
games, whilst playing the character's talking animation.

*See Also:* [Display](ags78#Display),
[Character.SayAt](ags47#Character.SayAt),
[Character.SayBackground](ags47#Character.SayBackground),
[Character.Think](ags47#Character.Think)

---

### SayAt

*(Formerly known as DisplaySpeechAt, which is now obsolete)*

    SayAt(int x, int y, int width, string message)

Similar to [Say](ags47#Character.Say), except that the text is
displayed with its top left corner at (X,Y), in an area WIDTH wide.

You can use this function to write the character's speech text anywhere
you like, and AGS will still play the character's talking animation and
so on if appropriate.

**NOTE:** This function does not support Whole-Screen speech.

Example:

    cEgo.SayAt(220, 20, 100, "My name is ego");

will display the message in the top right corner of the screen, whilst
playing the character's talking animation.

*See Also:* [Character.Say](ags47#Character.Say),
[Character.SayBackground](ags47#Character.SayBackground)

---

### SayBackground

*(Formerly known as DisplaySpeechBackground, which is now obsolete)*

    Overlay* Character.SayBackground(string message)

Similar to Say, except that this function returns immediately and the
game continues while the character is talking. This allows you to have
characters talking in the background while the player does other things.
Note that the character's talking animation is not played if this
function is used.

This command works by creating a text overlay with an automatic removal
time delay. The overlay is returned by this command, so you can save it
for use later with Overlay.IsValid and Overlay.Remove, if you want to
remove the text prematurely.

If background speech is already on-screen for the character, it will be
removed and replaced with the new MESSAGE.

All background speech is automatically removed when a normal Say command
is used (unless you set the global variable
[game.bgspeech\_stay\_on\_display](ags39#Gamevariables) to 1).

Example:

    cMan.SayBackground("Hey, why won't you talk to me?");

will display the message above character MAN's head without pausing the
game.

*See Also:* [Character.Say](ags47#Character.Say)

---

### SetAsPlayer

*(Formerly known as SetPlayerCharacter, which is now obsolete)*

    Character.SetAsPlayer()

Changes the character which the player controls to the specified
character. This function will also cause the room to change to the room
which the chosen character is currently in (though as with ChangeRoom,
the change won't happen until the end of the script).

Additionally, calling this command will cause the "player" variable to
be updated to point to the specified character.

Example:

    cMan.SetAsPlayer();

will change the character that the player controls to character MAN and
also change to the room that MAN is in, if he is not in the current
room.

*See Also:* [Character.ID](ags47#Character.ID),
[Character.ChangeRoom](ags47#Character.ChangeRoom)

---

### SetLightLevel (character)

    void Character.SetLightLevel(int light_level)

Sets individual light level for this character.

The light level is from **-100 to 100**.

In 8-bit games you cannot use positive light level for brightening
effect, but you may still use negative values to produce darkening
effect.

To disable character lighting and tinting effects, call
[RemoveTint](ags47#Character.RemoveTint).

**NOTE**: Setting a light level will disable any RGB tint set for the
character.

**NOTE:** Character's individual light level OVERRIDES both ambient
light level and local region light level.

Example:

    cEgo.SetLightLevel(100);

This will give character EGO maximal individual brightness.

*Compatibility:* Supported by **AGS 3.4.0** and later versions.

*See Also:* [Character.Tint](ags47#Character.Tint),
[SetAmbientLightLevel](ags54#SetAmbientLightLevel),
[Object.SetLightLevel](ags68#Object.SetLightLevel),
[Region.LightLevel](ags72#Region.LightLevel)

---

### SetIdleView

*(Formerly known as SetCharacterIdle, which is now obsolete)*

    Character.SetIdleView(int idleview, int delay)

Changes the character's idle view to IDLEVIEW, with a timeout of DELAY
seconds of inactivity before it is played. Inactivity is defined as when
the character is not moving and not being animated.

Setting DELAY to 0 causes the idle view to be looped continuously when
the character is not moving - this is useful when for example the
character is swimming and they need to tread water when idle.

Pass IDLEVIEW as -1 to disable the idle view completely.

**NOTE:** The DELAY is actually relative to the game speed. Setting this
to 1 means a one second delay at the default 40 fps, but if you have
adjusted the game speed then the delay will be adjusted accordingly.

**NOTE:** Due to a quirk in AGS, you cannot set the Idle View to view 1.
In the unlikely event that you created your idle view in View 1, you'll
need to move it to another view number.

Example:

    cEgo.SetIdleView(12, 30);

will change/set the character EGO's idle view to 12. The idle view will
be played if the character is idle for 30 seconds.

---

### SetWalkSpeed

*(Formerly known as SetCharacterSpeed, which is now obsolete)*\
*(Formerly known as SetCharacterSpeedEx, which is now obsolete)*

    Character.SetWalkSpeed(int x_speed, int y_speed)

Changes the character to have a walking speed of X\_SPEED in the
horizontal direction and Y\_SPEED in the vertical direction. The values
used for X\_SPEED and Y\_SPEED are identical to those set in the AGS
Editor for walking speed.

X\_SPEED and Y\_SPEED can be identical, in which case the character
moves with the same speed in any direction. (the editor calls this
"Uniform movement speed")

**NOTE:** This function CANNOT be called while the character is moving,
so you must stop him first.

Example:

    cEgo.SetWalkSpeed(10, 10);

will change the character EGO's speed to 10.

*See Also:*
[Character.AnimationSpeed](ags47#Character.AnimationSpeed),
[Character.StopMoving](ags47#Character.StopMoving),
[Character.Walk](ags47#Character.Walk),
[Character.WalkSpeedX](ags47#Character.WalkSpeedX),
[Character.WalkSpeedY](ags47#Character.WalkSpeedY)

---

### StopMoving (character)

*(Formerly known as global function StopMoving, which is now obsolete)*

    Character.StopMoving()

Stops the character moving and sets its graphic to the standing frame of
the current loop.

Example:

    if (cEgo.x > 299)
    {
      cEgo.StopMoving();
    }

will stop the character when he reaches the coordinate x=300.

*See Also:* [Character.Walk](ags47#Character.Walk),
[Object.StopMoving](ags68#Object.StopMoving)

---

### Think

*(Formerly known as DisplayThought, which is now obsolete)*

    Character.Think(string message, ...)

Displays the text MESSAGE as a thought above the specified character's
head. The text will remain on screen for a limited time, and the user
may or may not be able to click it away depending on the setting of
"Player can't skip speech text".

How this function displays the text depends on a few things: the Speech
Style setting, the 'Thought uses bubble GUI' setting, and whether the
character has a thinking animation or not.

If the "Thought uses bubble GUI" setting is not checked, then the
thought will be displayed in the same way as normal speech - the
difference being that the character's thinking animation will play (or
no animation if they don't have one).

If you are using Sierra-style speech and the character doesn't have a
thinking animation, the thought bubble will be displayed in
lucasarts-style.

If the "Thought uses bubble GUI" setting has been set, then the thought
will be displayed like normal speech, except that the bubble GUI will be
used for the window background. In Lucasarts-style speech this means
above the character's head, in Sierra-style it will be done along the
top of the screen as normal.

If the character has a thinking animation, it will just loop through
once (it won't repeat).

You can insert the value of variables into the message. For more
information, see the [string formatting](ags34#StringFormats)
section.

Example:

    cEgo.Think("I wonder what's for dinner.");

will display the message above EGO's head and play the character's
thinking animation.

*See Also:*
[Character.BlinkWhileThinking](ags47#Character.BlinkWhileThinking),
[Character.Say](ags47#Character.Say),
[Character.Thinking](ags47#Character.Thinking),
[Character.ThinkingFrame](ags47#Character.ThinkingFrame),
[Character.ThinkView](ags47#Character.ThinkView),
[game.speech\_bubble\_width](ags39#Gamevariables)

---

### Tint (character)

    Character.Tint(int red, int green, int blue,
                   int saturation, int luminance)

Tints the character on the screen to (RED, GREEN, BLUE) with SATURATION
percent saturation.

This function applies a tint to a specific character. For the meaning of
all the parameters, see [SetAmbientTint](ags54#SetAmbientTint).

The tint set by this function overrides any ambient tint set for the
room. For this reason, passing the SATURATION as 0 to this function does
not turn it off - rather, it ensures that no tint is applied to the
character (even if an ambient tint is set).

To remove the tint set by this function and return to using the ambient
tint for this character, call
[RemoveTint](ags47#Character.RemoveTint).

**NOTE:** This function only works in hi-colour games and with hi-colour
sprites.

Example:

    cEgo.Tint(0, 250, 0, 30, 100);

will tint the EGO character green.

*See Also:*
[Character.HasExplicitTint](ags47#Character.HasExplicitTint),
[Character.RemoveTint](ags47#Character.RemoveTint),
[SetAmbientTint](ags54#SetAmbientTint)

---

### TintBlue property (character)

    readonly int Character.TintBlue

Gets the *Blue* setting for the character's current tint.

This property is read-only; to change it, use the
[Character.Tint](ags47#Character.Tint) command.

**NOTE:** If the
[Character.HasExplicitTint](ags47#Character.HasExplicitTint)
property is false, then this value is meaningless.

*Compatibility:* Supported by **AGS 3.4.1** and later versions.

*See Also:* [Character.Tint](ags47#Character.Tint),
[Character.HasExplicitTint](ags47#Character.HasExplicitTint),
[Character.TintGreen](ags47#Character.TintGreen),
[Character.TintRed](ags47#Character.TintRed),
[Character.TintLuminance](ags47#Character.TintLuminance)

---

### TintGreen property (character)

    readonly int Character.TintGreen

Gets the *Green* setting for the character's current tint.

This property is read-only; to change it, use the
[Character.Tint](ags47#Character.Tint) command.

**NOTE:** If the
[Character.HasExplicitTint](ags47#Character.HasExplicitTint)
property is false, then this value is meaningless.

*Compatibility:* Supported by **AGS 3.4.1** and later versions.

*See Also:* [Character.Tint](ags47#Character.Tint),
[Character.TintBlue](ags47#Character.TintBlue),
[Character.TintRed](ags47#Character.TintRed),
[Character.TintSaturation](ags47#Character.TintSaturation),
[Character.TintLuminance](ags47#Character.TintLuminance)

---

### TintRed property (character)

    readonly int Character.TintRed

Gets the *Red* setting for the character's current tint.

This property is read-only; to change it, use the
[Character.Tint](ags47#Character.Tint) command.

**NOTE:** If the
[Character.HasExplicitTint](ags47#Character.HasExplicitTint)
property is false, then this value is meaningless.

*Compatibility:* Supported by **AGS 3.4.1** and later versions.

*See Also:* [Character.Tint](ags47#Character.Tint),
[Character.TintBlue](ags47#Character.TintBlue),
[Character.TintGreen](ags47#Character.TintGreen),
[Character.TintSaturation](ags47#Character.TintSaturation),
[Character.TintLuminance](ags47#Character.TintLuminance)

---

### TintSaturation property (character)

    readonly int Character.TintSaturation

Gets the *saturation* setting for the character's current tint.

This property is read-only; to change it, use the
[Character.Tint](ags47#Character.Tint) command.

**NOTE:** If the
[Character.HasExplicitTint](ags47#Character.HasExplicitTint)
property is false, then this value is meaningless.

*Compatibility:* Supported by **AGS 3.4.1** and later versions.

*See Also:* [Character.Tint](ags47#Character.Tint),
[Character.TintBlue](ags47#Character.TintBlue),
[Character.TintGreen](ags47#Character.TintGreen),
[Character.TintRed](ags47#Character.TintRed),
[Character.TintLuminance](ags47#Character.TintLuminance)

---

### TintLuminance property (character)

    readonly int Character.TintLuminance

Gets the *luminance* setting for the character's current tint.

This property is read-only; to change it, use the
[Character.Tint](ags47#Character.Tint) command.

**NOTE:** If the
[Character.HasExplicitTint](ags47#Character.HasExplicitTint)
property is false, then this value is meaningless.

*Compatibility:* Supported by **AGS 3.4.1** and later versions.

*See Also:* [Character.Tint](ags47#Character.Tint),
[Character.TintBlue](ags47#Character.TintBlue),
[Character.TintGreen](ags47#Character.TintGreen),
[Character.TintRed](ags47#Character.TintRed),
[Character.TintSaturation](ags47#Character.TintSaturation)

---

### UnlockView

*(Formerly known as ReleaseCharacterView, which is now obsolete)*

    Character.UnlockView(StopMovementStyle=eStopMoving)

Allows the engine to automatically control the character's view, as
normal. Use this once you have finished doing the animation which you
started with the LockView command.

*StopMovementStyle* determines what to do if character was moving when
this function is called. You can pass either eStopMoving (in which case
the walking character will stop), or eKeepMoving (in which case the
character will keep moving). The default is eStopMoving.

Example:

    cEgo.LockView(12);
    cEgo.Animate(0, 0, eOnce, eBlock, eForwards);
    cEgo.UnlockView();

will play an animation using loop 0 of view 12, then return the
character to its normal view.

*Compatibility:* Optional *StopMovementStyle* parameter is supported
only by **AGS 3.4.1** and later versions.

*See Also:* [Character.LockView](ags47#Character.LockView)

---

### Walk

*(Formerly known as MoveCharacter, which is now obsolete)*\
*(Formerly known as MoveCharacterBlocking, which is now obsolete)*\
*(Formerly known as MoveCharacterDirect, which is now obsolete)*

    Character.Walk(int x, int y, optional BlockingStyle,
                                 optional WalkWhere);

Starts the character moving from its current location to (X,Y), whilst
playing his walking animation.

If *blocking* is eNoBlock (the default) then control returns to the
script immediately, and the character will move in the background.

If *blocking* is eBlock then this command will wait for the character to
finish moving before your script resumes.

If *walkWhere* is eWalkableAreas (the default), then the character will
attempt to get as close a possible to (X,Y) by using the room's walkable
areas.

If *walkWhere* is eAnywhere, then the character will simply walk
directly from its current location to (X,Y), ignoring the room walkable
areas.

If you don't want the character's walking animation to play, you can use
the [Move](ags47#Character.Move) command instead.

**NOTE:** this function only works with characters which are on the
current screen.

**NOTE:** if you need to find out when the character has reached its
destination, use the [Moving](ags47#Character.Moving) property.

Example:

    cEgo.Walk(155, 122, eBlock);

will make the character walk to 155,122. The script will not continue
until the character has reached his destination.

*See Also:* [Character.AddWaypoint](ags47#Character.AddWaypoint),
[Character.FaceCharacter](ags47#Character.FaceCharacter),
[Character.Move](ags47#Character.Move),
[MoveCharacterToObject](ags54#MoveCharacterToObject),
[Object.Move](ags68#Object.Move),
[Character.StopMoving](ags47#Character.StopMoving)

---

### WalkStraight

*(Formerly known as MoveCharacterStraight, which is now obsolete)*

    Character.WalkStraight(int x, int y, optional BlockingStyle);

Moves the character from its current location towards (X,Y) in a
straight line as far as is possible before hitting a non-walkable area.
This is useful for use with the arrow keys for character movement, since
it guarantees that the character will move in a straight line in the
direction specified.

*blocking* determines whether the function waits for the character to
finish moving before your script resumes. eNoBlock is the default (which
means your script resumes straight away, and the character moves in the
background). You can also pass eBlock, in which case your script will
not resume until the character finishes moving.

Example:

    cEgo.WalkStraight(166, 78);

will move the character EGO in a straight line towards co ordinates
166,78 until he hits a non walkable area.

*See Also:* [Character.Walk](ags47#Character.Walk)

---

### ActiveInventory property

*(Formerly known as SetActiveInventory, which is now obsolete)*\
*(Formerly known as character\[\].activeinv, which is now obsolete)*

    InventoryItem* Character.ActiveInventory

Gets/sets the character's current active inventory item. Setting it will
update the mouse cursor if appropriate.

This property is useful in "Use inventory on hotspot/character/etc"
events, to find out which inventory item the player is trying to use on
the target.

To deselect the current inventory, set it to *null*.

Example:

    cEgo.ActiveInventory = iKey;

will make the inventory item iKey active (before you use it make sure
that the player has the inventory item)

---

### Animating property (character)

*(Formerly known as character\[\].animating, which is now obsolete)*

    readonly bool Character.Animating

Returns 1 if the character is currently animating.\
Returns 0 if the character has finished its animation.

This property is read-only. To change character animation, use the
[Animate](ags47#Character.Animate) command.

Example:

    cEgo.Animate(5, 0);
    while (cEgo.Animating) Wait(1);

will animate EGO and wait until the animation finishes.

In reality, you would simply use the Blocking parameter of Animate so
you wouldn't need to do this.

*See Also:* [Character.Animate](ags47#Character.Animate),
[Character.Moving](ags47#Character.Moving),
[Character.Speaking](ags47#Character.Speaking),
[Character.Thinking](ags47#Character.Thinking)

---

### AnimationSpeed property

*(Formerly known as character\[\].animspeed, which is now obsolete)*

    int Character.AnimationSpeed;

Gets/sets the character's animation delay, as set in the editor.

Example:

    player.AnimationSpeed = 4;

will change the player character's animation speed to 4.

*See Also:* [Character.SetWalkSpeed](ags47#Character.SetWalkSpeed),
[Character.SpeechAnimationDelay](ags47#Character.SpeechAnimationDelay)

---

### Baseline property (character)

*(Formerly known as SetCharacterBaseline, which is now obsolete)*

    int Character.Baseline

Gets/sets the character's baseline. This allows you to set a specific
base line for the character, which works similarly to walk-behind area
and object baselines.

The baseline can be from 1 to the height of the room (normally 200), or
set it to 0 to go back to using the character's feet as the baseline.

Example:

    cEgo.Baseline = 120;

will move the character's baseline (which can be used for testing
collisions, or for walk-behinds) to a line positioned at y coordinate =
120.

*See Also:* [Object.Baseline](ags68#Object.Baseline),
[SetWalkBehindBase](ags73#SetWalkBehindBase)

---

### BlinkInterval property

*(Formerly part of SetCharacterBlinkView, which is now obsolete)*

    int Character.BlinkInterval

Gets/sets the character's blinking interval, which specifies how long
the game waits between playing the blinking animation. This is specified
in game loops - an interval of 80 would play the blinking animation
about every 2 seconds.

This property has no effect if no
[BlinkView](ags47#Character.BlinkView) has been set.

Example:

    cEgo.BlinkView = 10;
    cEgo.BlinkInterval = 160;

will change the character EGO's blink view to view 10, and play the
animation every 4 seconds.

*See Also:* [Character.BlinkView](ags47#Character.BlinkView),
[Character.SpeechView](ags47#Character.SpeechView)

---

### BlinkView property

*(Formerly part of SetCharacterBlinkView, which is now obsolete)*

    int Character.BlinkView

Gets/sets the character's blinking view. To stop the character from
blinking, set this to -1.

The [BlinkInterval](ags47#Character.BlinkInterval) property sets how
often the blinking animation is played.

Example:

    cEgo.BlinkView = 10;
    cEgo.BlinkInterval = 160;

will change the character EGO's blink view to view 10, and play the
animation every 4 seconds.

*See Also:*
[Character.BlinkInterval](ags47#Character.BlinkInterval),
[Character.SpeechView](ags47#Character.SpeechView)

---

### BlinkWhileThinking property

    bool Character.BlinkWhileThinking

Gets/sets whether the character can blink while thinking. By default
this is set to true, but if your blinking animation only goes with the
talking animation and not the thinking one, you can stop the character
from blinking while Thinking by setting this to false.

Example:

    cEgo.BlinkWhileThinking = false;

will stop EGO from blinking while his thinking animation is playing.

*See Also:* [Character.BlinkView](ags47#Character.BlinkView),
[Character.Think](ags47#Character.Think)

---

### BlockingHeight property (character)

    int Character.BlockingHeight

Gets/sets the character's blocking height.

The blocking height determines how large of a blocking rectangle the
character exerts to stop other characters walking through it. If this is
set to 0 (the default), then the blocking rectangle is automatically
calculated to be the character's width, and 5 pixels high.

You can manually change the setting by entering a blocking height in
pixels, which is the size of walkable area that the character
effectively removes by standing on it.

**NOTE:** This property has no effect unless the
[Solid](ags47#Character.Solid) property is set to *true*.

Example:

    cEgo.BlockingHeight = 20;

will make EGO block 20 pixels high (10 above and 10 below his baseline)

*See Also:*
[Character.BlockingWidth](ags47#Character.BlockingWidth),
[Character.Solid](ags47#Character.Solid)

---

### BlockingWidth property (character)

    int Character.BlockingWidth

Gets/sets the character's blocking width.

The blocking width determines how large of a blocking rectangle the
character exerts to stop other characters walking through it. If this is
set to 0 (the default), then the blocking rectangle is automatically
calculated to be the character's width, and 5 pixels high.

You can manually change the setting by entering a blocking width in
pixels, which is the size of walkable area that the character
effectively removes by standing on it.

**NOTE:** This property has no effect unless the
[Solid](ags47#Character.Solid) property is set to *true*.

Example:

    cEgo.BlockingWidth = 50;

will make EGO block 50 pixels wide (25 pixels to the left of his X
co-ordinate, and 25 to the right)

*See Also:*
[Character.BlockingHeight](ags47#Character.BlockingHeight),
[Character.Solid](ags47#Character.Solid)

---

### Clickable property (character)

*(Formerly known as SetCharacterClickable, which is now obsolete)*

    bool Character.Clickable

Gets/sets whether the character is recognised as something which the
player can interact with. This allows you to modify the "Clickable"
property set initially in the Editor.

If you set this to *true* then the player can look at, speak to, and so
on the character (as with the old Sierra games). If you set this to
*false*, then if the player clicks on the character it will activate
whatever is behind them (as with the old Lucasarts games).

Example:

    cMan.Clickable = 0;

will make the game ignore clicks on the character MAN.

*See Also:* [Object.Clickable](ags68#Object.Clickable),
[Character.Move](ags47#Character.Move),
[Character.Moving](ags47#Character.Moving),
[Character.Walk](ags47#Character.Walk)

---

### DestinationX property

    readonly int Character.DestinationX

Gets the X coordinate of the character's final moving destination. If
character is not walking or moving it is equal to its current position.

*Compatibility:* Supported by **AGS 3.4.0** and later versions.

*See Also:* [Character.DestinationY](ags47#Character.DestinationY),
[Character.Move](ags47#Character.Move),
[Character.Moving](ags47#Character.Moving),
[Character.Walk](ags47#Character.Walk)

---

### DestinationY property

    readonly int Character.DestinationY

Gets the Y coordinate of the character's final moving destination. If
character is not walking or moving it is equal to its current position.

*Compatibility:* Supported by **AGS 3.4.0** and later versions.

*See Also:* [Character.DestinationX](ags47#Character.DestinationX),
[Character.Move](ags47#Character.Move),
[Character.Moving](ags47#Character.Moving),
[Character.Walk](ags47#Character.Walk)

---

### DiagonalLoops property

*(Formerly part of SetCharacterProperty, which is now obsolete)*

    bool Character.DiagonalLoops

Gets/sets whether diagonal walking loops are used for the character. If
this is set to *true*, then loops 4-7 will be used as diagonal walking
loops. If this is set to *false*, then the character will only face in 4
directions and you can use loops 4-7 for other purposes.

Example:

    cEgo.DiagonalLoops = true;

will enable diagonal walking loops for character EGO.

---

### Frame property (character)

*(Formerly known as character\[\].frame, which is now obsolete)*

    int Character.Frame

Gets/sets the character's current frame number. Usually you won't change
this directly, but will use the Animate command to play an animation.

Example:

    Display("EGO currently using frame %d.", cEgo.Frame);

displays EGO's current frame number within his view.

*SeeAlso:* [Character.Animate](ags47#Character.Animate),
[Character.Loop](ags47#Character.Loop),
[Character.View](ags47#Character.View)

---

### HasExplicitTint property (character)

    readonly bool Character.HasExplicitTint

Returns *true* if the character has a tint set explicitly with the
[Character.Tint](ags47#Character.Tint) command.

Returns *false* if the character has no explicit tint, but it may still
be tinted by [SetAmbientTint](ags54#SetAmbientTint) or a region
tint.

Example:

    if (player.HasExplicitTint)
    {
      player.RemoveTint();
    }

removes the player's tint if it currently has one.

*Compatibility:* Supported by **AGS 3.1.0** and later versions.

*SeeAlso:* [Character.Tint](ags47#Character.Tint),
[Character.RemoveTint](ags47#Character.RemoveTint)

---

### ID property (character)

    readonly int Character.ID

Gets the character's ID number. This is the character's number from the
editor, and is useful if you need to interoperate with legacy code that
uses the character's number rather than name.

Example:

    MoveCharacter(cEgo.ID, 100, 50);

uses the obsolete MoveCharacter function to move EGO to (100, 50)

---

### IdleView property

    readonly int Character.IdleView

Gets the character's current idle view. If the character doesn't have
one, returns -1.

This property is read-only; to change the view, use the
[SetIdleView](ags47#Character.SetIdleView) function.

Example:

    Display("EGO's idle view is currently view %d.", cEgo.IdleView);

will display EGO's current idle view number.

*SeeAlso:* [SetIdleView](ags47#Character.SetIdleView)

---

### IgnoreLighting property

*(Formerly known as SetCharacterIgnoreLight, which is now obsolete)*

    bool Character.IgnoreLighting

Allows you to dynamically modify the "ignore lighting" checkbox for the
character. If this is set to 0, the character will be affected by region
light levels and tints; if this is set to 1, then the character will
ignore all region lighting.

Example:

    cEgo.IgnoreLighting = 1;

will make the character look the same no matter if he stands on regions
with different light levels.

---

### IgnoreWalkbehinds property (character)

*(Formerly known as SetCharacterIgnoreWalkbehinds, which is now
obsolete)*

    bool Character.IgnoreWalkbehinds

Gets/sets whether the character is affected by walkbehind areas. Passing
*false* (the default setting) means that the character will be placed
behind walk- behind areas according to the relevant baselines.

Passing *true* means that the character will never be placed behind a
walk-behind area. This is useful if for example you want to use the
character as an overlay to display rain or snow onto a scene.

**NOTE:** enabling this property does not currently work properly when
using the Direct3D driver.

Example:

    cEgo.IgnoreWalkbehinds = true;

will make the character EGO ignore walk-behinds.

*See Also:* [Character.Baseline](ags47#Character.Baseline),
[Object.IgnoreWalkbehinds](ags68#Object.IgnoreWalkbehinds)

---

### InventoryQuantity property

*(Formerly known as character\[\].inv, which is now obsolete)*

    int Character.InventoryQuantity[]

Gets/sets the quantity of the specified inventory item that the
character currently has. The array index is the inventory item number,
from the Inventory pane in the editor.

Usually, you should use the AddInventory and LoseInventory functions to
modify the character's inventory; however, if you need to add or remove
a large number of items in one go, directly changing this array can be
an easier method.

If you change this array directly, the on-screen inventory will not be
updated. In this case, you must call UpdateInventory to see any new or
removed items.

If you just want to quickly check whether the character has a particular
item or not, use the [HasInventory](ags47#Character.HasInventory)
function instead.

Example:

    Display("The player has $%d.", player.InventoryQuantity[iCash.ID]);

will display how many inventory items of type iCash the player has.

*See Also:* [UpdateInventory](ags54#UpdateInventory),
[Character.AddInventory](ags47#Character.AddInventory),
[Character.HasInventory](ags47#Character.HasInventory),
[Character.LoseInventory](ags47#Character.LoseInventory)

---

### Loop property (character)

*(Formerly known as character\[\].loop, which is now obsolete)*

    int Character.Loop

Gets/sets the character's current loop number. Usually you won't change
this directly, but will use the Animate command to play an animation.

Example:

    Display("EGO currently using loop %d.", cEgo.Loop);

displays EGO's current loop number within his view.

*SeeAlso:* [Character.Animate](ags47#Character.Animate),
[Character.Frame](ags47#Character.Frame),
[Character.View](ags47#Character.View)

---

### ManualScaling property (character)

*(Formerly known as Character.IgnoreScaling, which is now obsolete)*\
*(Formerly part of SetCharacterProperty, which is now obsolete)*

    bool Character.ManualScaling

Gets/sets whether the character's scaling level is determined by the
walkable area that he is walking on, or whether it is set manually by
the script. This is equivalent to the "Ignore room area scaling"
checkbox in the editor.

If this is set to *true*, then the character's scaling level is set
manually by the [Scaling](ags47#Character.Scaling) property (by
default this is `100%`). If it is set to *false*, then the character
will be stretched or shrunk automatically as appropriate on walkable
areas.

Example:

    cEgo.ManualScaling = true;
    cEgo.Scaling = 50;

will tell EGO to ignore walkable area scaling levels and be fixed to
`50%` zoom level.

*SeeAlso:* [Character.Scaling](ags47#Character.Scaling)

---

### MovementLinkedToAnimation property

    bool Character.MovementLinkedToAnimation

Gets/sets whether the character's movement is linked to their animation.
By default this is *true*, which means that when the character is
walking their movement across the screen will be kept in sync with their
animation frame changing. Without this, the character can appear to
"glide" across the screen.

In some special cases you may wish to turn this off though, and to do so
you can set this property to *false*.

In previous versions of AGS, this setting was known as "Anti-glide mode"
and was a game-wide setting.

Example:

    player.MovementLinkedToAnimation = false;
    player.Walk(50, 100, eBlock);
    player.MovementLinkedToAnimation = true;

will turn off movement-linked animation for the player character, walk
him to (50,100), then turn it back on again.

*Compatibility:* Supported by **AGS 3.1.1** and later versions.

*See Also:* [Character.Move](ags47#Character.Move),
[Character.Moving](ags47#Character.Moving),
[Character.Walk](ags47#Character.Walk)

---

### Moving property (character)

*(Formerly known as character\[\].walking, which is now obsolete)*

    readonly bool Character.Moving

Returns *true* if the character is currently moving, or *false* if not.

This property is read-only; to change the character's movement, use the
[Walk](ags47#Character.Walk), [Move](ags47#Character.Move) and
[StopMoving](ags47#Character.StopMoving) commands.

Example:

    cEgo.Walk(125, 40);
    while (cEgo.Moving) Wait(1);

will move EGO to 125,40 and return control to the player when he gets
there.

*See Also:* [Character.Animating](ags47#Character.Animating),
[Character.Move](ags47#Character.Move),
[Character.Speaking](ags47#Character.Speaking),
[Character.StopMoving](ags47#Character.StopMoving),
[Character.Thinking](ags47#Character.Thinking),
[Character.Walk](ags47#Character.Walk)

---

### Name property (character)

*(Formerly known as character\[\].name, which is now obsolete)*

    String Character.Name

Gets/sets the name of the character, as set in the AGS Editor. This is
the full name, not the script name.

Note that character names are limited to 40 characters, so if you set
the name it will be truncated to that length.

Example:

    Display("You are controlling %s.", player.Name);

will display the name of the player character

---

### NormalView property

*(Formerly known as character\[\].defview, which is now obsolete)*

    readonly int Character.NormalView

Gets the character's normal view. This is the character's standard
walking view, that is used when his view is not locked to something
else.

This property is read-only; to change it, use the
[ChangeView](ags47#Character.ChangeView) command.

Example:

    if (cEgo.View == cEgo.NormalView) {
      Display("EGO is not animating, not talking and not idle.");
    }

will display a message if EGO is currently displayed using his normal
view.

*See Also:* [Character.ChangeView](ags47#Character.ChangeView),
[Character.View](ags47#Character.View)

---

### PreviousRoom property

*(Formerly known as character\[\].prevroom, which is now obsolete)*

    readonly int Character.PreviousRoom

Gets the room number that the character was previously in. If the
character is still in the room that they started in, this will be -1.
Otherwise, it will be the room number of the room that they were last
in.

This is a read-only property. It is set automatically by
[ChangeRoom](ags47#Character.ChangeRoom).

Example:

    Display("EGO's previous room was %d.", cEgo.PreviousRoom);

will display the EGO character's previous room.

---

### Room property

*(Formerly known as character\[\].room, which is now obsolete)*

    readonly int Character.Room

Gets the room number that the character is currently in.

This is a read-only property. It is set by
[ChangeRoom](ags47#Character.ChangeRoom).

Example:

    Display("EGO is in room %d.", cEgo.Room);

will display the EGO character's current room.

---

### ScaleMoveSpeed property

*(Formerly part of SetCharacterProperty, which is now obsolete)*

    bool Character.ScaleMoveSpeed

Gets/sets whether the character's movement speed is adjusted in line
with his current scaling level. This allows you to modify the "Adjust
speed with scaling" option from the editor.

If you set this to *true*, the character's movement speed will be
adjusted so that he walks at a speed relative to his current scaling
level. If you set this to *false*, the character will always just move
at his normal speed.

Example:

    cEgo.ScaleMoveSpeed = true;

will mean that EGO's speed is adjusted in line with his scaling

*See Also:* [Character.ScaleVolume](ags47#Character.ScaleVolume)

---

### ScaleVolume property

    bool Character.ScaleVolume

Gets/sets whether the character's volume is adjusted in line with his
current scaling level. This allows you to modify the "Adjust volume with
scaling" option from the editor.

By default, this is *false*. If you set it to *true*, then any
frame-linked sounds for the character (for example, footstep sounds)
will have their volume automatically adjusted in line with the
character's scaling level. At the normal `100%` zoom level the sounds
will be played at normal volume, but will then get quieter and louder as
appropriate in scaled walkable areas.

Example:

    cEgo.ScaleVolume = true;

will mean that EGO's footstep sounds are adjusted in line with his
scaling

*See Also:*
[Character.ScaleMoveSpeed](ags47#Character.ScaleMoveSpeed)

---

### Scaling property (character)

    int Character.Scaling

Gets/sets the character's current scaling level.

This property can always be read, and returns the character's current
zoom level, which will be between 5 and 200 (the default being 100 if
they are not currently scaled).

You can only set the value of this property if
[ManualScaling](ags47#Character.ManualScaling) is enabled for the
character; otherwise, the scaling is determined automatically based on
the walkable area that the character is on.

Example:

    cEgo.ManualScaling = true;
    cEgo.Scaling = 50;

will tell EGO to ignore walkable area scaling levels and be fixed to
`50%` zoom level.

*SeeAlso:* [Character.ManualScaling](ags47#Character.ManualScaling)

---

### Solid property (character)

*(Formerly part of SetCharacterProperty, which is now obsolete)*

    bool Character.Solid

Gets/sets whether the character can be walked through by other
characters.

If this is set to *true*, then the character is solid and will block the
path of other characters. If this is set to *false*, then the character
acts like a hologram, and other characters can walk straight through
him.

Example:

    cEgo.Solid = true;

will mean that EGO blocks the path other characters.

*See Also:*
[Character.BlockingHeight](ags47#Character.BlockingHeight),
[Character.BlockingWidth](ags47#Character.BlockingWidth)

---

### Speaking property

    readonly bool Character.Speaking

Returns true if the character is currently talking, or false if not.

This property is read-only. It will **only** return true for the active
talking character; that is, it will not return true for any characters
talking with the SayBackground command.

Since this property will only be true while the character is speaking,
and speaking is a blocking command, this property will probably only be
useful to access from the (late\_)repeatedly\_execute\_always handler.

Example:

    if ((cEgo.Speaking) && (!cEgo.Animating)) {
      cEgo.Animate(3, 5, eRepeat, eNoBlock);
    }

will animate the character using loop 3 while they are talking (only
useful with Sierra-style speech).

*See Also:* [Character.Animating](ags47#Character.Animating),
[Character.Moving](ags47#Character.Moving),
[Character.Say](ags47#Character.Say),
[Character.SpeakingFrame](ags47#Character.SpeakingFrame),
[Character.Thinking](ags47#Character.Thinking)

---

### SpeakingFrame property

    readonly int Character.SpeakingFrame

Returns the current frame number of the character's talking animation.
This is useful when using Sierra-style speech, if you want to
synchronize events with the progress of the close-up face talking
animation.

This property is read-only. It is only accessible while the character is
speaking; if you attempt to call it when
[Character.Speaking](ags47#Character.Speaking) is *false* then it
will raise an error.

Since speaking is a blocking command, this property will probably only
be useful access from the (late\_)repeatedly\_execute\_always handler.

Example:

    if (cEgo.Speaking) {
      if (cEgo.SpeakingFrame == 0) {
        cMan.Move(cMan.x + 10, cMan.y, eNoBlock, eAnywhere);
      }
    }

will move cMan to the right every time the talking animation loops back
to Frame 0.

*See Also:* [Character.Say](ags47#Character.Say),
[Character.Speaking](ags47#Character.Speaking)

---

### SpeechAnimationDelay property

    int Character.SpeechAnimationDelay;

Gets/sets the character's speech animation delay, as set in the editor.
This specifies how many game loops each frame of the character's speech
animation is shown for.

**NOTE:** This property is ignored if lip sync is enabled.

**NOTE:** This property **cannot** be used if the
Speech.UseGlobalSpeechAnimationDelay is set to **true**. In that case,
the Speech.GlobalSpeechAnimationDelay property value is used instead.

Example:

    player.SpeechAnimationDelay = 4;

will change the player character's speech animation speed to 4.

*Compatibility:* Supported by **AGS 3.1.2** and later versions.

*See Also:*
[Character.AnimationSpeed](ags47#Character.AnimationSpeed),
[Character.SpeechView](ags47#Character.SpeechView),
[Game.TextReadingSpeed](ags54#Game.TextReadingSpeed),
[Speech.GlobalSpeechAnimationDelay](ags75#Speech.GlobalSpeechAnimationDelay),
[Speech.UseGlobalSpeechAnimationDelay](ags75#Speech.UseGlobalSpeechAnimationDelay),

---

### SpeechColor property

*(Formerly known as SetTalkingColor, which is now obsolete)*

    int Character.SpeechColor

Gets/sets the character's speech text color. This is set by default in
the editor.

NEWCOLOR is the colour slot index from the Palette Editor. This can be
0-255 for a 256-colour game, or one of the hi-colour indexes available
from the Palette Editor.

Example:

    cEgo.SpeechColor = 14;

will change the character's EGO talking color to yellow.

*See Also:* [Character.SpeechView](ags47#Character.SpeechView)

---

### SpeechView property

*(Formerly known as SetCharacterSpeechView, which is now obsolete)*\
*(Formerly known as character\[\].talkview, which is now obsolete)*

    int Character.SpeechView

Gets/sets the character's talking view. If you change it, the new view
number will be used as the character's talking view in all future
conversations.

You can set this to -1 to disable the character's speech view.

Example:

    cEgo.SpeechView = 10;

will change the character EGO's speech view to view 10.

*See Also:* [Character.ChangeView](ags47#Character.ChangeView),
[Character.BlinkView](ags47#Character.BlinkView),
[Character.SpeechAnimationDelay](ags47#Character.SpeechAnimationDelay),
[Character.SpeechColor](ags47#Character.SpeechColor)

---

### Thinking property

    readonly bool Character.Thinking

Returns true if the character is currently thinking, or false if not.

This property is read-only. It will **only** return true for the active
thinking character.

Since this property will only be true while the character is thinking,
and thinking is a blocking command, this property will probably only be
useful to access from the (late\_)repeatedly\_execute\_always handler.

Example:

    function repeatedly_execute_always()
    {
      if (cEgo.Thinking) {
        cEgo.Transparency = 50;
      else
        cEgo.Transparency = 0;
    }

this will keep character semi-transparent while he is thinking.

*Compatibility:* Supported by **AGS 3.3.4** and later versions.

*See Also:* [Character.Animating](ags47#Character.Animating),
[Character.Moving](ags47#Character.Moving),
[Character.Speaking](ags47#Character.Speaking)
[Character.Think](ags47#Character.Think),
[Character.ThinkingFrame](ags47#Character.ThinkingFrame),

---

### ThinkingFrame property

    readonly int Character.ThinkingFrame

Returns the current frame number of the character's thinking animation.
This is useful when using Sierra-style speech, if you want to
synchronize events with the progress of the close-up face talking
animation.

This property is read-only. It is only accessible while the character is
thinking; if you attempt to call it when
[Character.Thinking](ags47#Character.Thinking) is *false* then it
will raise an error.

Since thinking is a blocking command, this property will probably only
be useful access from the (late\_)repeatedly\_execute\_always handler.

Example:

    if (cEgo.Thinking) {
      if (cEgo.ThinkingFrame == 0) {
        cMan.Move(cMan.x + 10, cMan.y, eNoBlock, eAnywhere);
      }
    }

will move cMan to the right every time the thinking animation loops back
to Frame 0.

*Compatibility:* Supported by **AGS 3.3.4** and later versions.

*See Also:* [Character.Think](ags47#Character.Think),
[Character.Thinking](ags47#Character.Thinking)

---

### ThinkView property

*(Formerly known as character\[\].thinkview, which is now obsolete)*

    int Character.ThinkView

Gets/sets the character's thinking view. This is used to animate the
character when a thought is being displayed.

Example:

    cEgo.ThinkView = 14;

will change the character EGO's thinking view to 14.

*See Also:* [Character.Think](ags47#Character.Think)

---

### Transparency property (character)

*(Formerly known as SetCharacterTransparency, which is now obsolete)*

    int Character.Transparency

Gets/sets the character's transparency. This is specified as a
percentage, from 0 to 100. 100 means fully transparent (ie. invisible),
and 0 is totally opaque (fully visible). Numbers in between represent
varying levels of transparency.

**NOTE:** Transparency only works in 16-bit and 32-bit colour games.

**NOTE:** When using the DirectX 5 driver, a large transparent character
can significantly slow down AGS.

Some rounding is done internally when the transparency is stored --
therefore, if you get the transparency after setting it, the value you
get back might be one out. Therefore, using a loop with
`cEgo.Transparency++;` is not recommended as it will probably end too
quickly.

In order to fade a character in, the best approach is shown in the
example below:

Example:

    int trans = cEgo.Transparency;
    while (trans < 100) {
      trans++;
      cEgo.Transparency = trans;
      Wait(1);
    }

will gradually fade out the character from its current transparency
level to being fully invisible.

*See Also:* [Object.Transparency](ags68#Object.Transparency)

---

### TurnBeforeWalking property

*(Formerly part of SetCharacterProperty, which is now obsolete)*

    bool Character.TurnBeforeWalking

Gets/sets whether the character turns to face his new direction before
walking. This is equivalent (though opposite) to the editor "Do not turn
before walking" tick-box.

If you set this to 1, the character will turn on the spot to face his
new direction before setting off on a walk. If you set this to 0, the
character will instantly face in the correct direction and start
walking.

Example:

    cEgo.TurnBeforeWalking = 1;

will tell EGO to turn to face his new direction before setting off,
whenever he walks.

---

### View property (character)

    readonly int Character.View

Gets the view that the character is currently displayed using.

This property is read-only; to change the view, use the ChangeView and
LockView functions.

Example:

    Display("EGO's view is currently view %d.", cEgo.View);

will display EGO's current view number.

*SeeAlso:* [Character.ChangeView](ags47#Character.ChangeView),
[Character.Frame](ags47#Character.Frame),
[Character.LockView](ags47#Character.LockView),
[Character.Loop](ags47#Character.Loop),
[Character.NormalView](ags47#Character.NormalView)

---

### WalkSpeedX property

    readonly int Character.WalkSpeedX;

Gets the character's walking speed in the X direction. If using uniform
movement, this will be the same as the Y walking speed.

This property is read-only. To change the walking speed, use the
SetWalkSpeed function.

Example:

    Display("player's x speed: %d", player.WalkSpeedX);

will display the player's X speed.

*See Also:* [Character.SetWalkSpeed](ags47#Character.SetWalkSpeed),
[Character.WalkSpeedY](ags47#Character.WalkSpeedY)

---

### WalkSpeedY property

    readonly int Character.WalkSpeedY;

Gets the character's walking speed in the Y direction. If using uniform
movement, this will be the same as the X walking speed.

This property is read-only. To change the walking speed, use the
SetWalkSpeed function.

Example:

    Display("player's y speed: %d", player.WalkSpeedY);

will display the player's Y speed.

*See Also:* [Character.SetWalkSpeed](ags47#Character.SetWalkSpeed),
[Character.WalkSpeedX](ags47#Character.WalkSpeedX)

---

### x property (character)

    int Character.x;

Gets/sets the character's current X co-ordinate. This is expressed in
normal room co-ordinates, and specifies the centre-bottom of the
character's sprite.

**NOTE:** Do **NOT** change this property while the character is moving.
Make sure the character is standing still before changing his
co-ordinates.

Example:

    Display("The player is at %d,%d.", player.x, player.y);

displays the player character's current coordinates.

*See Also:* [Character.y](ags47#Character.y),
[Character.z](ags47#Character.z)

---

### y property (character)

    int Character.y;

Gets/sets the character's current Y co-ordinate. This is expressed in
normal room co-ordinates, and specifies the centre-bottom of the
character's sprite.

**NOTE:** Do **NOT** change this property while the character is moving.
Make sure the character is standing still before changing his
co-ordinates.

Example:

    Display("The player is at %d,%d.", player.x, player.y);

displays the player character's current coordinates.

*See Also:* [Character.x](ags47#Character.x),
[Character.z](ags47#Character.z)

---

### z property (character)

    int Character.z;

Gets/sets the character's current Z position. This allows the character
to levitate off the ground, whilst still retaining its normal Y
co-ordinate for baseline calculations and regions.

Normally this is set to 0 (ground-level), but you can increase it to
make the character float.

Example:

    while (player.z < 20) {
      player.z++;
      Wait(1);
    }

gradually levitates the character up to 20 pixels.

*See Also:* [Character.x](ags47#Character.x),
[Character.y](ags47#Character.y)

---

### SetCharacterProperty

    SetCharacterProperty (CHARID, PROPERTY, int new_value)

**This command is now obsolete. It has been replaced by the following
properties:**

[Clickable](ags47#Character.Clickable)\
[DiagonalLoops](ags47#Character.DiagonalLoops)\
[IgnoreLighting](ags47#Character.IgnoreLighting)\
[ManualScaling](ags47#Character.ManualScaling)\
[ScaleMoveSpeed](ags47#Character.ScaleMoveSpeed)\
[Solid](ags47#Character.Solid)\
[TurnBeforeWalking](ags47#Character.TurnBeforeWalking)
