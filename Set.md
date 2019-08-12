## Set Functions and Properties

### Create

    Set* Create(SortStyle sortStyle, StringCompareStyle compareStyle)

Creates a new empty Set of the given properties. If you don't pass any options, the Set is non sorted and case insensitive.

Example:

    Set* mySet = Set.Create();

will fade the screen to black, wait 1 sec (40 game cycles) and then fade
in again.

*See Also:* [Dictionary](Dictionary#create)

---

### Add

    bool Add(String item)

Adds item to the set, fails if such item was already existing, returning false.

Example:

    mySet.Add("item1");
    bool wasAdded = mySet.Add("item1"); //wasAdded is false

will fade the screen to black, wait 1 sec (40 game cycles) and then fade
in again.

*See Also:* [Remove](Set#remove)

---

### Clear

    Clear()

Removes all items from the set.

---

### Contains

    bool Contains(String item)

Returns true if given item is in the set.

Example:

    Set* mySet = Set.Create();
    mySet.Add("test");
    if(mySet.Contains("test")){
      Display("This was a triumph")
    }


---

### Remove

    bool Remove(String item)

Removes item from the set, returns false if there was no such item.

*See Also:* [Add](Set#add)

---

### CompareStyle

    StringCompareStyle CompareStyle

Gets if this set is case-sensitive.

*See Also:* [SortStyle](Set#sortstyle)

---

### SortStyle

    SortStyle SortStyle

Gets the method items are arranged in this set.

*See Also:* [CompareStyle](Set#comparestyle)

---

### ItemCount

    int ItemCount

Gets the number of items currently in the set.

---

### GetItemsAsArray

    String[] GetItemsAsArray()

Creates a dynamic array filled with items in same order as they are stored in the Set.

Example:

    Set* mySet = Set.Create();
    mySet.Add("test");
    mySet.Add("test2");
    String* mySetAsArray = mySet.GetItemsAsArray();

---