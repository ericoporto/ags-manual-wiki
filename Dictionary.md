## Dictionary Functions and Properties

Dictionary allows you to store key/value string pairs and look values up by a string key. In the dictionary key must be unique, but value does not have to be. This means that you may have same value assigned for multiple keys, but not same key with multiple values.

Because of how dictionaries work internally, searching for a key in dictionary is faster than you'd search for it in a plain array. Its advantage increases with the number of items. They are also fast in adding and removing items dynamically.

Dictionary has two general properties: **sort style** and **compare style**.

**Sort style** defines whether items are stored sorted or unsorted. The unsorted containers are commonly somewhat faster to search in, but the items will be stored in an undefined order.

**Compare style** determines whether string keys are compared as case sensitive or case insensitive. For example, in case-sensitive dictionary strings "Parameter" and "parameter" will be seen as two different keys, but in case-insensitive they will be seen as identical. Compare style defines both key uniqueness and sorting.

At the moment a dictionary itself does not let you see access all of its internal data at once directly, but has [GetKeysAsArray](Dictionary#getkeysasarray) and [GetValuesAsArray](Dictionary#getvaluesasarray) functions that will write all items to a dynamic array, which you may parse, print, and otherwise use as you see fit. The order of items in these arrays will be matching one inside the dictionary, hence if the dictionary was sorted the array will be sorted as well.

To summarize, dictionaries make convenient storage for key/value pairs. If you do not need pairs but rather a sequence of unique values - then look for [Set](Set).

### Create

    static Dictionary* Dictionary.Create(SortStyle sortStyle, StringCompareStyle compareStyle)

Creates a new empty Dictionary of the given properties. If you don't pass any options the Dictionary is unsorted and case -insensitive. Note that you cannot change sorting style and case sensitivity later, you would have to create another Dictionary and move values there.

Example:

    Dictionary* myDictionary = Dictionary.Create();

---

### Clear

    void Dictionary.Clear()

Removes all items from the dictionary.

---

### Contains

    bool Dictionary.Contains(String key)

Returns true if the key is in the dictionary, otherwise - false.

Example:

    Dictionary* myDictionary = Dictionary.Create();
    myDictionary.Set("my-key","my-value");
    if(myDictionary.Contains("my-key")){
      Display("has my key!");
    }

This will add "my-key" key, assign "my-value" to that key and then test whether that key was added successfuly.

*See Also:* [Dictionary.Get](Dictionary#get),
[Dictionary.Set](Dictionary#set)

---

### Get

    String Dictionary.Get(String key)

Gets value by the key. Returns null if such key does not exist.

Example:

    Dictionary* myDictionary = Dictionary.Create();
    myDictionary.Set("a-key","a-value");
    String myValue = myDictionary.Get("a-key");

Here _myValue_ variable will be assigned "a-value" from the dictionary.

*See Also:* [Dictionary.Set](Dictionary#set)

---

### GetKeysAsArray

    String[] Dictionary.GetKeysAsArray()

Creates a dynamic array filled with keys in same order as they are stored in the Dictionary.

Example:

    Dictionary* myDictionary = Dictionary.Create();
    myDictionary.Set("my-key1","my-value1");
    myDictionary.Set("my-key2","my-value2");
    String keys[] = myDictionary.GetKeysAsArray();
    for (int i = 0; i < myDictionary.ItemCount; i++)
      Display("#%d: %s", i, keys[i]);

In the above example the keys will be displayed on screen one by one, preceded by their index.

*See Also:* [Dictionary.ItemCount](Dictionary#itemcount)

---

### GetValuesAsArray

    String[] Dictionary.GetValuesAsArray()

Creates a dynamic array filled with values in same order as they are stored in the Dictionary.

Example:

    Dictionary* myDictionary = Dictionary.Create();
    myDictionary.Set("my-key1","my-value1");
    myDictionary.Set("my-key2","my-value2");
    String values[] = myDictionary.GetValuesAsArray();
    for (int i = 0; i < myDictionary.ItemCount; i++)
      Display("#%d: %s", i, values[i]);

In the above example the values will be displayed on screen one by one, preceded by their index.

*See Also:* [Dictionary.ItemCount](Dictionary#itemcount)

---

### Remove

    bool Dictionary.Remove(String key)

Removes key/value pair from the dictionary, returns true on success and false if there was no such key.

*See Also:* [Dictionary.Set](Dictionary#set)

---

### Set

    bool Dictionary.Set(String key, String value)

Assigns a value to the given key. If the key did not exist then it will be created, if there was such key already then old assigned value will be overwritten with a new one.

*See Also:* [Dictionary.Get](Dictionary#get),
[Dictionary.Remove](Dictionary#remove)

---

### CompareStyle

    StringCompareStyle Dictionary.CompareStyle

Gets if this dictionary keys are case-sensitive.

*See Also:* [Dictionary.SortStyle](Dictionary#sortstyle)

---

### ItemCount

    int Dictionary.ItemCount

Gets the number of key/value pairs currently in the dictionary.

---

### SortStyle

    SortStyle Dictionary.SortStyle

Gets the method keys are arranged in this dictionary.

*See Also:* [Dictionary.CompareStyle](Dictionary#comparestyle)
