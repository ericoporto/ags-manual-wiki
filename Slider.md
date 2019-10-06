## `Slider` properties

Slider is a subclass of [GUIControl](GUIControl) and therefore inherits all GUIControl's functions and properties in addition to its own, which are listed below.

_See also:_ [Editing GUI Sliders](EditingGUIs#sliders)

---

### `Slider.BackgroundGraphic`

    int Slider.BackgroundGraphic;

Gets/sets the sprite used to draw the slider background. This image is
tiled along the length of the slider.

The background graphic can be set to 0, which will draw the default grey
slider background.

Example:

    Display("sldHealth's background is sprite %d", sldHealth.BackgroundGraphic);

displays the *sldHealth* slider's background image

*Compatibility:* Supported by **AGS 3.1.0** and later versions.

*See Also:* [Slider.HandleGraphic](Slider#sliderhandlegraphic)

---

### `Slider.HandleGraphic`

    int Slider.HandleGraphic;

Gets/sets the sprite used to draw the handle on the slider. The handle
represents the slider's current position, and can be dragged around by
the player.

The handle graphic can be set to 0, which will draw the default grey
handle.

Example:

    Display("sldHealth's handle is sprite %d", sldHealth.HandleGraphic);

displays the *sldHealth* slider's handle image

*Compatibility:* Supported by **AGS 3.1.0** and later versions.

*See Also:*
[Slider.BackgroundGraphic](Slider#sliderbackgroundgraphic),
[Slider.HandleOffset](Slider#sliderhandleoffset)

---

### `Slider.HandleOffset`

    int Slider.HandleOffset;

Gets/sets the offset at which the handle image is drawn. This value is
initially set up in the editor.

Example:

    sldHealth.HandleOffset = 2;

sets the *sldHealth* slider's handle to be drawn an extra 2 pixels to
the right.

*Compatibility:* Supported by **AGS 3.1.0** and later versions.

*See Also:* [Slider.HandleGraphic](Slider#sliderhandlegraphic)

---

### `Slider.Max`

    int Slider.Max;

Gets/sets the maximum value of the specified GUI slider.

When changing the maximum, the slider's Value will be adjusted if
necessary so that it lies within the Min - Max range.

An error occurs if you try to set the Max to a lower value than the Min.

Example:

    sldHealth.Max = 200;

sets the maximum value of the *sldHealth* slider to 200.

*See Also:* [Slider.Min](Slider#slidermin),
[Slider.Value](Slider#slidervalue)

---

### `Slider.Min`

    int Slider.Min;

Gets/sets the minimum value of the specified GUI slider.

When changing the minimum, the slider's Value will be adjusted if
necessary so that it lies within the Min - Max range.

An error occurs if you try to set the Min to a higher value than the
Max.

Example:

    sldHealth.Min = 0;

sets the minimum value of the *sldHealth* slider to 0.

*See Also:* [Slider.Max](Slider#slidermax),
[Slider.Value](Slider#slidervalue)

---

### `Slider.Value`

*(Formerly known as GetSliderValue, which is now obsolete)*<br>
*(Formerly known as SetSliderValue, which is now obsolete)*

    int Slider.Value;

Gets/sets the value of the specified GUI slider. You would usually use
this in the slider's OnChange event handler to find out what value the
player has changed the slider to, in order to process their command.

When setting the value, the new value must lie between the MIN and MAX
settings for the slider, as set up in the GUI editor.

Example:

    System.Volume = sldVolume.Value;

will set the audio volume to the value of the slider *sldVolume*.

*See Also:* [Label.Text](Label#labeltext)

