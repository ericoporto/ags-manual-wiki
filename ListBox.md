## ListBox functions and properties

ListBox is a subclass of [GUIControl](GUIControl) and therefore inherits all GUIControl's functions and properties in addition to its own, which are listed below.

---

### AddItem

*(Formerly known as ListBoxAdd, which is now obsolete)*

    ListBox.AddItem(string newitem)

Adds NEWITEM to the specified list box. The item will be appended to the
end of the list.

**NOTE:** List boxes have a limit of 200 items. If you try to add more
than that, this function will return *false* and the item will not be
added.

Example:

    String input = txtUserInput.Text;
    lstChoices.AddItem(input);

will take the input from the user and add it to the listbox.

*See Also:* [ListBox.Clear](ListBox#clear),
[ListBox.FillDirList](ListBox#filldirlist),
[ListBox.InsertItemAt](ListBox#insertitemat),
[ListBox.Items](ListBox#items),
[ListBox.RemoveItem](ListBox#removeitem)

---

### Clear

*(Formerly known as ListBoxClear, which is now obsolete)*

    ListBox.Clear()

Removes all items from the specified list box.

Example:

    lstNoteBook.Clear();

will remove all the items from listbox *lstNoteBook*.

*See Also:* [ListBox.AddItem](ListBox#additem)

---

### FillDirList

*(Formerly known as ListBoxDirList, which is now obsolete)*

    ListBox.FillDirList(string filemask)

Fills the list box with a list of filenames matching FILEMASK in the
current directory. This could be useful if you have various data files
and the player can choose which one to load.

FILEMASK is a standard Windows search expression such as `"*.dat"` or
`"data*.*"`

When specifying file path you may use special location tags:<br>
`$INSTALLDIR$`, which allows you to explicitly access files in the game
installation directory.<br>
`$SAVEGAMEDIR$`, which allows you to access files in the save game
directory.<br>
`$APPDATADIR$`, which allows you to access files to a folder on the
system which is accessible by and shared by all users.

Example:

    lstSaveGames.FillDirList("agssave.*");

will fill the listbox with the list of the saved games. Note that
actually for this task you would use FillSaveGameList instead.

*See Also:* [ListBox.AddItem](ListBox#additem),
[ListBox.Clear](ListBox#clear),
[ListBox.FillSaveGameList](ListBox#fillsavegamelist)

---

### FillSaveGameList

*(Formerly known as ListBoxSaveGameList, which is now obsolete)*

    ListBox.FillSaveGameList()

Fills the specified listbox with the save game list, sorted correctly
with the most recent game at the top of the list.

The [SaveGameSlots](ListBox#savegameslots) property is updated
to contain the save game slot number for each index in the list, so that
you can do:

    int index = lstSaveGames.SelectedIndex;
    RestoreGameSlot(lstSaveGames.SaveGameSlots[index]);

**NOTE:** The save game list can only hold 50 save games. If
ListBox.ItemCount returns 50 and you are doing a Save dialog box, you
may want to make the user replace an existing file rather than saving a
new one.

Example:

    lstSaveGames.FillSaveGameList();

will fill listbox *lstSaveGames* with the list of the saved games.

*See Also:* [ListBox.FillDirList](ListBox#filldirlist),
[ListBox.ItemCount](ListBox#itemcount),
[ListBox.SaveGameSlots](ListBox#savegameslots),
[ListBox.SelectedIndex](ListBox#selectedindex)

---

### GetItemAtLocation

    ListBox.GetItemAtLocation(int x, int y)

Determines which item in the list box is at the screen co-ordinates
(X,Y). This allows you to find out which item the mouse is hovering
over, for instance.

Returns the item index (where the first item is 0), or -1 if the
specified co-ordinates are not over any item or are outside the list
box.

Example:

    int index = lstOptions.GetItemAtLocation(mouse.x, mouse.y);
    if (index < 0) {
      Display("The mouse is not over an item!");
    }
    else {
      String selectedItem = lstOptions.Items[index];
      Display("The mouse is over item '%s'.", selectedItem);
    }

will display the item text that the mouse is currently hovering over.

*See Also:* [ListBox.SelectedIndex](ListBox#selectedindex)

---

### InsertItemAt

    ListBox.InsertItemAt(int index, string newitem)

Inserts NEWITEM into the specified list box. The item will be inserted
**before** the specified index.

Listbox indexes go from 0 (the first item) to ItemCount - 1 (the last
item). The new item will be inserted before the index you specify.

**NOTE:** List boxes have a limit of 200 items. If you try to add more
than that, this function will return *false* and the item will not be
added.

Example:

    lstChoices.AddItem("First item");
    lstChoices.AddItem("Second item");
    lstChoices.InsertItemAt(1, "Third item");

will insert the Third Item in between the First and Second items.

*See Also:* [ListBox.AddItem](ListBox#additem),
[ListBox.RemoveItem](ListBox#removeitem)

---

### RemoveItem

*(Formerly known as ListBoxRemove, which is now obsolete)*

    ListBox.RemoveItem(int item)

Removes ITEM from the specified list box. ITEM is the list index of the
item to remove, starting with 0 for the top item.

If you want to remove all items from the list, then use
[ListBox.Clear](ListBox#clear) instead.

**NOTE:** Calling this function causes other items in the list to get
re-numbered, so make sure you don't keep around any references from
ListBox.SelectedIndex and related functions while using this command.

Example:

    lstTest.AddItem("First item");
    lstTest.AddItem("Second item");
    lstTest.RemoveItem(0);

the list box will now just contain "Second item".

*See Also:* [ListBox.Clear](ListBox#clear),
[ListBox.FillDirList](ListBox#filldirlist)

---

### ScrollDown

    ListBox.ScrollDown()

Scrolls the list box down one row. If it is already at the bottom,
nothing happens.

Example:

    lstTest.ScrollDown();

will scroll the *lstTest* list box down one row.

*See Also:* [ListBox.ScrollUp](ListBox#scrollup)

---

### ScrollUp

    ListBox.ScrollUp()

Scrolls the list box up one row. If it is already at the top, nothing
happens.

Example:

    lstTest.ScrollUp();

will scroll the *lstTest* list box up one row.

*See Also:* [ListBox.ScrollDown](ListBox#scrolldown)

---

### Font

    FontType ListBox.Font

Gets/sets the font used by the specified list box.

Example:

    lstSaveGames.Font = eFontSpeech;

will change the *lstSaveGames* list box to use Font "Speech".

*See Also:* [Label.Font](Label#font),
[TextBox.Text](TextBox#text)

---

### HideBorder

**This property is obsolete since AGS 3.5.0. Use [ListBox.ShowBorder](ListBox#showboder) instead.**

    bool ListBox.HideBorder

Gets/sets whether the list box's border is _hidden_.

---

### HideScrollArrows

**This property is obsolete since AGS 3.5.0. Use [ListBox.ShowScrollArrows](ListBox#showscrollarrows) instead.**

    bool ListBox.HideScrollArrows

Gets/sets whether the built-in up/down scroll arrows are _hidden_.

---

### ItemCount

*(Formerly known as ListBoxGetNumItems, which is now obsolete)*

    readonly int ListBox.ItemCount

Gets the number of items in the specified listbox. Valid item indexes
range from 0 to (numItems - 1).

This property is read-only. To change the item count, use the AddItem
and RemoveItem methods.

Example:

    int saves = lstSaveGames.ItemCount;

will pass the number of saved games to the int saves.

*See Also:* [ListBox.Items](ListBox#items)

---

### Items

*(Formerly known as ListBoxGetItemText, which is now obsolete)*<br>
*(Formerly known as ListBox.GetItemText, which is now obsolete)*<br>
*(Formerly known as ListBox.SetItemText, which is now obsolete)*

    String ListBox.Items[index]

Gets/sets the text of the list box item at INDEX.

List box items are numbered starting from 0, so the first item is 0, the
second is 1, and so on. The highest allowable index is ItemCount minus
1.

If you want to add a new item to the listbox, use the
[ListBox.AddItem](ListBox#additem) method.

Example:

    String selectedItemText = lstOptions.Items[lstOptions.SelectedIndex];

will get the text of the selected item in the list box.

*See Also:* [ListBox.SelectedIndex](ListBox#selectedindex),
[ListBox.ItemCount](ListBox#itemcount),
[ListBox.AddItem](ListBox#additem)

---

### RowCount

    readonly int ListBox.RowCount

Gets the number of rows that can be shown within the list box. This
depends on the size of the list box, and **does not** depend on how many
items are actually stored in the list box.

This property is read-only. To change the row count, adjust the height
of the list box.

Example:

    Display("You can currently see %d items from the listbox's contents", lstSaveGames.RowCount);

will display the number of rows that the listbox can display.

*See Also:* [ListBox.ItemCount](ListBox#itemcount),
[ListBox.ScrollDown](ListBox#scrolldown),
[ListBox.ScrollUp](ListBox#scrollup)

---

### SaveGameSlots

*(Formerly known as global array savegameindex, which is now obsolete)*

    readonly int ListBox.SaveGameSlots[];

Contains the corresponding save game slot for each item in the list.

This is necessary because the FillSaveGameList command sorts the list of
save games to put the most recent first. Therefore, you can use this
array to map the list box indexes back to the corresponding save game
slot.

**NOTE:** You must use the FillSaveGameList command in order to populate
this array.

Example:

    int index = lstSaveGames.SelectedIndex;
    RestoreGameSlot(lstSaveGames.SaveGameSlots[index]);

will restore the currently selected game in the list, assuming
FillSaveGameList had been used previously.

*See Also:*
[ListBox.FillSaveGameList](ListBox#fillsavegamelist),
[ListBox.SelectedIndex](ListBox#selectedindex)

---

### SelectedBackColor

    int ListBox.SelectedBackColor

Gets/sets the fill color of the selection rectangle drawn around the selected item.

Example:

    lstSaveGames.SelectedBackColor = Game.GetColorFromRGB(0, 148, 255);

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [ListBox.Font](ListBox#font), [ListBox.SelectedTextColor](ListBox#selectedtextcolor), [ListBox.TextColor](ListBox#textcolor)

---

### SelectedIndex

*(Formerly known as ListBoxGetSelected, which is now obsolete)*<br>
*(Formerly known as ListBoxSetSelected, which is now obsolete)*

    int ListBox.SelectedIndex

Gets/sets the index into the list of the currently selected item. The
first item is 0, second is 1, and so on. If no item is selected, this is
set to -1.

You can set this to -1 to remove the highlight (ie. un-select all
items).

Example:

    String selectedText = lstOptions.Items[lstOptions.SelectedIndex];

will get the text of the selected item in the listbox.

---

### SelectedTextColor

    int ListBox.SelectedTextColor

Gets/sets the text color used for the selected item.

Example:

    lstSaveGames.SelectedTextColor = Game.GetColorFromRGB(255, 255, 80);

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [ListBox.Font](ListBox#font), [ListBox.SelectedTextColor](ListBox#selectedtextcolor), [ListBox.TextColor](ListBox#textcolor)

---

### ShowBorder

*(Formerly known as ListBox.HideBorder, which is now obsolete)*

    bool ListBox.ShowBorder

Gets/sets whether the list box's border is shown.

Border is drawn using color from TextColor property.

Note that hiding the border will also implicitly hide the up/down scroll arrows for the list box.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:*
[ListBox.ShowScrollArrows](ListBox#showscrollarrows), [ListBox.TextColor](ListBox#textcolor)

---

### ShowScrollArrows

*(Formerly known as ListBox.HideScrollArrows, which is now obsolete)*

    bool ListBox.ShowScrollArrows

Gets/sets whether the built-in up/down scroll arrows are shown.

Arrows are drawn using color from TextColor property.

Because the overall appearance of the scroll arrows is not customizable, you may
wish to use this to hide them and provide your own arrows using GUI
Button controls.

**NOTE:** If the list box's "Show Border" setting is disabled, then the
scroll arrows will also be hidden, since "Show Border" supersedes "Show
Scroll Arrows". You only need to use this ShowScrollArrows property if
you want the border to be shown but the arrows hidden.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [ListBox.ShowBorder](ListBox#showborder), [ListBox.TextColor](ListBox#textcolor)

---

### TextAlignment

    HorizontalAlignment ListBox.TextAlignment

Gets/sets the way a text is aligned inside an item's rectangle. Currently only horizontal alignment is supported, that is: eAlignLeft, eAlignCenter and eAlignRight.

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [Standard Enumerated Types](StandardEnums), [ListBox.Font](ListBox#font), [ListBox.SelectedBackColor](ListBox#selectedbackcolor), [ListBox.SelectedTextColor](ListBox#selectedtextcolor)

---

### TextColor

    int ListBox.TextColor

Gets/sets the text color used by default, that is - for the non-selected items. Note that the same color is also used for the listbox's border and and scroll arrows.

Example:

    lstSaveGames.TextColor = Game.GetColorFromRGB(80, 80, 200);

*Compatibility:* Supported by **AGS 3.5.0** and later versions.

*See Also:* [ListBox.Font](ListBox#font), [ListBox.SelectedBackColor](ListBox#selectedbackcolor), [ListBox.SelectedTextColor](ListBox#selectedtextcolor), [ListBox.ShowBorder](ListBox#showborder), [ListBox.ShowScrollArrows](ListBox#showscrollarrows)

---

### TopItem

*(Formerly known as ListBoxSetTopItem, which is now obsolete)*

    int ListBox.TopItem

Gets/sets the top item in the list box. The top item is the first item
that is visible within the list box, so changing this effectively
scrolls the list up and down.

Indexes for TopItem start from 0 for the first item in the list.

Example:

    lstSaveGames.TopItem = 0;

will automatically scroll listbox *lstSaveGames* back to the top of the
list.

---

### Translated

    bool ListBox.Translated

Gets/sets whether the list box's items are translated to the selected
game language at runtime.

*Compatibility:* Supported by **AGS 3.3.0** and later versions.

