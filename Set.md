## Set Functions and Properties

Set allows you to store a sequence of unique strings and efficiently look them up. When adding a string Set will automatically test whether such string is already contained and won't make a duplicate.

Because of how sets work internally, searching for a string in a set is faster than you'd search for it in a plain array. Its advantage increases with the number of items. They are also fast in adding and removing items dynamically.

Similar to [Dictionary](Dictionary), Set has two general properties: **sort style** and **compare style**.

**Sort style** defines whether items are stored sorted or unsorted. The unsorted containers are commonly somewhat faster to search in, but the items will be stored in an undefined order.

**Compare style** determines whether strings are compared as case sensitive or case insensitive. For example, in case-sensitive set strings "Parameter" and "parameter" will be seen as two different items, but in case-insensitive they will be seen as identical. Compare style defines both string uniqueness and sorting.

At the moment a set itself does not let you access all of its internal data at once directly, but has [GetItemsAsArray ](Set#getitemsasarray) function that will write all items to a dynamic array, which you may parse, print, and otherwise use as you see fit. The order of items in this array will be matching one inside the set, hence if the set was sorted the array will be sorted as well.

*Compatibility:* Set struct is supported by **AGS 3.5.0** and later versions.

*See Also:* [Dictionary](Dictionary)

---

### Create

    static Set* Set.Create(SortStyle sortStyle, StringCompareStyle compareStyle)

Creates a new empty Set of the given properties. If you don't pass any options the Set is unsorted and case-insensitive. Note that you cannot change sorting style and case sensitivity later, you would have to create another Set and move values there.

Example:

    Set* mySet = Set.Create();

---

### Add

    bool Set.Add(String item)

Adds item to the set, fails if such item was already contained, returning false.

Example:

    mySet.Add("item1");
    bool wasAdded = mySet.Add("item1"); // wasAdded will be false

*See Also:* [Contains](Set#contains), [Remove](Set#remove)

---

### Clear

    void Set.Clear()

Removes all items from the set.

---

### Contains

    bool Set.Contains(String item)

Gets if the given item is in the set.

Example:

    Set* mySet = Set.Create();
    mySet.Add("test");
    if (mySet.Contains("test")) {
      Display("Test passed!");
    }

*See Also:* [Add](Set#add), [Remove](Set#remove)

---

### GetItemsAsArray

    String[] GetItemsAsArray()

Creates a dynamic array filled with items in same order as they are stored in the Set.

Example:

    Set* mySet = Set.Create();
    mySet.Add("test");
    mySet.Add("test2");
    String items[] = mySet.GetItemsAsArray();
    for (int i = 0; i < mySet.ItemCount; i++)
      Display("#%d: %s", i, items[i]);

In the above example the items will be displayed on screen one by one, preceded by their index.

*See Also:* [Set.ItemCount](Set#itemcount)

---

### Remove

    bool Set.Remove(String item)

Removes item from the set, returns false if there was no such item.

*See Also:* [Add](Set#add), [Contains](Set#contains)

---

### CompareStyle

    StringCompareStyle Set.CompareStyle

Gets if this set is case-sensitive.

*See Also:* [SortStyle](Set#sortstyle)

---

### ItemCount

    int Set.ItemCount

Gets the number of items currently in the set.

---

### SortStyle

    SortStyle Set.SortStyle

Gets the method items are arranged in this set.

*See Also:* [CompareStyle](Set#comparestyle)
