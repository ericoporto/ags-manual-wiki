## `Dictionary` Functions and Properties

A Dictionary allows you to store key/value string pairs and look up values be referencing their associated key. Within the dictionary each key must be unique, but the value does not have to be. This means that you may have the same value assigned for multiple keys, but not a single key with multiple values.

Because of how dictionaries work internally, searching for a key in dictionary is faster than you'd search for it in a regular array. The advantage increases with the number of items searched. They are also fast to add or remove items.

A Dictionary has two general properties: **sort style** and **compare style**.

**Sort style** defines whether items are stored sorted or unsorted, based on their keys. The unsorted containers are commonly somewhat faster to search in, but the items will be stored in an undefined order.

**Compare style** determines whether string keys are compared as case sensitive or case insensitive. For example, in a case-sensitive dictionary the strings "Parameter" and "parameter" will be seen as two different keys, but in a case-insensitive dictionary they will be seen as the same key. Compare style defines both key uniqueness and sorting.

At the moment a dictionary does not let you directly access all of its internal data, but has [GetKeysAsArray](Dictionary#dictionarygetkeysasarray) and [GetValuesAsArray](Dictionary#dictionarygetvaluesasarray) functions that will write all items to a dynamic array, which you may parse, print, and otherwise use as you see fit. The order of items in these arrays will match their order within the dictionary, hence if the dictionary was sorted the array will be sorted as well.

To summarize, dictionaries make convenient storage for key/value pairs. If you do not need pairs but rather a sequence of unique values, you may wish to use a [Set](Set) instead.

*Compatibility:* Dictionary struct is supported by **AGS 3.5.0** and later versions.

---

### `Dictionary.Create`

    static Dictionary* Dictionary.Create(SortStyle sortStyle, StringCompareStyle compareStyle)

Creates a new empty Dictionary of the given properties. If you don't pass any options the Dictionary is unsorted and case-insensitive. Note that you cannot change sorting style and case sensitivity later, you would have to create another Dictionary and then re-add the values there.

Example:

    Dictionary* myDictionary = Dictionary.Create();

---

### `Dictionary.Clear`

    void Dictionary.Clear()

Removes all items from the dictionary.

---

### `Dictionary.Contains`

    bool Dictionary.Contains(String key)

Returns true if the key is in the dictionary, otherwise - false.

Example:

    Dictionary* myDictionary = Dictionary.Create();
    myDictionary.Set("my-key","my-value");
    if(myDictionary.Contains("my-key")){
      Display("has my key!");
    }

This will add "my-key" key, assign "my-value" to that key and then test whether that key was added successfully.

*See Also:* [Dictionary.Get](Dictionary#dictionaryget),
[Dictionary.Set](Dictionary#dictionaryset)

---

### `Dictionary.Get`

    String Dictionary.Get(String key)

Gets the value for the given key. Returns null if such a key does not exist.

Example:

    Dictionary* myDictionary = Dictionary.Create();
    myDictionary.Set("a-key","a-value");
    String myValue = myDictionary.Get("a-key");

Here _myValue_ variable will be assigned "a-value" from the dictionary.

*See Also:* [Dictionary.Set](Dictionary#dictionaryset)

---

### `Dictionary.GetKeysAsArray`

    String[] Dictionary.GetKeysAsArray()

Creates a dynamic array filled with keys in the same order as they are stored in the Dictionary.

**IMPORTANT:** this returns a *copy* of Dictionary contents existing at the time of function call. If you change Dictionary later, that won't affect previously created key array and you would have to call this function again.

Returns null if this Dictionary is empty.

Example:

    Dictionary* myDictionary = Dictionary.Create();
    myDictionary.Set("my-key1","my-value1");
    myDictionary.Set("my-key2","my-value2");
    String keys[] = myDictionary.GetKeysAsArray();
    for (int i = 0; i < myDictionary.ItemCount; i++)
      Display("#%d: %s", i, keys[i]);

In the above example the keys will be displayed on screen one by one, preceded by their index.

*See Also:* [Dictionary.ItemCount](Dictionary#dictionaryitemcount)

---

### `Dictionary.GetValuesAsArray`

    String[] Dictionary.GetValuesAsArray()

Creates a dynamic array filled with values in the same order as they are stored in the Dictionary.

**IMPORTANT:** this returns a *copy* of Dictionary contents existing at the time of function call. If you change Dictionary later, that won't affect previously created values array and you would have to call this function again.

Returns null if this Dictionary is empty.

Example:

    Dictionary* myDictionary = Dictionary.Create();
    myDictionary.Set("my-key1","my-value1");
    myDictionary.Set("my-key2","my-value2");
    String values[] = myDictionary.GetValuesAsArray();
    for (int i = 0; i < myDictionary.ItemCount; i++)
      Display("#%d: %s", i, values[i]);

In the above example the values will be displayed on screen one by one, preceded by their index.

*See Also:* [Dictionary.ItemCount](Dictionary#dictionaryitemcount)

---

### `Dictionary.Remove`

    bool Dictionary.Remove(String key)

Removes a key/value pair from the dictionary, returns true on success and false if there was no such key.

*See Also:* [Dictionary.Set](Dictionary#dictionaryset)

---

### `Dictionary.Set`

    bool Dictionary.Set(String key, String value)

Assigns a value to the given key. If the key did not exist then it will be created, otherwise the old value for this key will be overwritten with a new one.

*See Also:* [Dictionary.Get](Dictionary#dictionaryget),
[Dictionary.Remove](Dictionary#dictionaryremove)

---

### `Dictionary.CompareStyle`

    StringCompareStyle Dictionary.CompareStyle

Returns the string comparison method for this dictionary, which determines whether its keys are case-sensitive.

*See Also:* [Dictionary.SortStyle](Dictionary#dictionarysortstyle)

---

### `Dictionary.ItemCount`

    int Dictionary.ItemCount

Gets the number of key/value pairs currently in the dictionary.

---

### `Dictionary.SortStyle`

    SortStyle Dictionary.SortStyle

Returns the key sorting method for this dictionary.

*See Also:* [Dictionary.CompareStyle](Dictionary#dictionarycomparestyle)
