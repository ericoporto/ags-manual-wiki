## Advanced room features

This section describes slightly more advanced things you can do with the
rooms.

---

### Character scaling

AGS supports scaling of characters, where the character can appear to
get smaller as he walks away from the screen. Character scaling is
supported as part of the walkable areas in a room.

The reason why you have multiple colors available for the walkable
areas is because you can set a zoom level for each color, which defines
how large the character will be while he is in that area. The default
for all walkable areas is `100%`, i.e. full size. However, you can adjust
it using the "Walkable Areas" mode to anywhere from `10%` (one-tenth
size) to `200%` (double size).

The scaling settings can affect all characters and objects in the game.
For characters, it is on by default but you can disable the scaling for
an individual character by setting the "UseRoomAreaScaling" option in
that character's properties.

For objects, it is off by default but you can make a specific object
obey scaling levels by setting its "UseRoomAreaScaling" option.

If you set the "UseContinuousScaling" option, then rather than just
specifying a zoom level for the whole walkable area, you specify a min
and max zoom level. These specify the scaling at the top and bottom of
the walkable area. When the game is run, AGS will interpolate these
values to make the character smoothly scale down from one value to
another as he walks towards the back or front of the screen.

---

### Scrolling

It's easy to create scrolling rooms like the ones used in LucasArts
games like Monkey Island (TM) and Day of the Tentacle.

To do this, just import a background scene that is larger than your game
resolution. For example, in a 320x200 game, 500x200 is a good size for
LucasArts-type rooms.

That's all you have to do. Draw on the walkable areas, hotspots and so
on, as normal, and then save the room. The screen will scroll to follow
the main character around.

With the script command [Camera.SetAt](Camera#camerasetat), you can manually scroll
the room around if you don't want it to follow the character. The default camera
is accessible using [Game.Camera](Game#gamecamera).

---

### Importing a file as the walkable area mask

AGS has the ability to import an external BMP or PNG file to use as the
walkable-area, hotspot or walk-behind area mask. If you don't like the
way you have to draw these in the editor itself, you can draw them in
another program and then import them. This is also useful if you are
converting a game you were making with another game-creation system into
AGS.

To use the feature, click the "Import Mask" button (in the toolbar) in
the relevant mode of the Areas editor. There are some restrictions to
how this file must be drawn: it must be the exact same size as the
background scene, and it must be in 16-color (4-bit) or 256-color
(8-bit). Then, color 0 on the bitmap signifies transparency and colors
1-15 are used as the respective hotspot/walk-behind/walkable area
numbers.

![Note](images/icon_info.png) (**IMPORTANT**: Do NOT use any color numbers above 15 on the mask
bitmap. Use only palette indexes 0 to 15.)

---

### Animating background scenes

If you want to have a lot of animation on the screen, you will come
across two problems if you try to do it using objects:

-   There is a limit on the number of objects per screen, so you may not
    be able to animate everything that you want to that way.
-   Objects slow down the game - the more objects on the screen, the
    slower the game runs.

The solution to these problems is to use an animating background scene.

How it works is this: Each room can have from 1 to 5 backgrounds.
Normally, each room just has one background. However, you can import up
to four extra backgrounds in each room, and if you do so then the game
will cycle through them, giving the effect of animation.

This gives two main advantages - you can animate the entire screen, and
due to the way the engine works, it doesn't slow down the game at all.

To import a second background for a room, load the room into the editor,
pull down the "Main background" list box, and choose the "Import new
background" option. Choose the file that's storing the background and
you're done.

To delete a background, select it then click the "Delete" button.

You define the speed at which the backgrounds will animate by setting
the "BackgroundAnimationDelay" option in the property grid for the room.
The default is 5, which cycles background every 5 frames.

![Note](images/icon_info.png) (**NOTE**: All the background scenes must be the same size.)

![Note](images/icon_info.png) (**NOTE**: **(256-color only)** The backgrounds frames each have their own
palette (unless you select "Share palette with main background" before
importing). This means that when the current frame switches in-game, the
palette will get reset - therefore you can't use special palette effects
such as CyclePalette or SetPalRGB on screens with animating backgrounds.)

---

### Lighting effects

You can control the brightness of your characters, courtesy of the
"LightLevel" setting for room Regions.

By default this is `100%`, but you can change it from `0% to 200%`. This
number is the light level in the current walkable area. Smaller numbers
are darker, so that `0%` is pitch black and `200%` is very bright.

This feature could be useful if, for example, you have a street lamp on
your scene so when the character walks under it they get brighter, or if
a wall is shading the character from the light they can get darker.

You can alternatively use a color tint for the region. If you select
this, then you can enter Red, Green and Blue values as numbers from
0-255, which reflect the color you want the area to be tinted to. The
Amount setting determines to what extent characters will be tinted, and
is from 0-100.

![Note](images/icon_info.png) (**NOTE**: Light levels only work when the character's graphic is at the
same color depth as the background (i.e. a 256-color character in a
hi-color game won't get lightened).)

![Note](images/icon_info.png) (**NOTE**: In a 256-color game, only darkening areas (light level <
`100%`) will work. Also, depending on the room palette the quality of
the darkening will vary in 256-color games.)

![Note](images/icon_info.png) (**NOTE**: Light levels affect characters and objects, depending on the
"UseRoomAreaLighting" setting for each one. They do not affect overlays
or the background scene.)

Now you are ready to read in-depth about setting up your game.

Next Reading: [Setting Up Your Game](Settingupthegame)

Return to Tutorials Index: [Tutorials Index](StartingOff)
