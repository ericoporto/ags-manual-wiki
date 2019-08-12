## Dictionary Functions and Properties

### Create

    Dictionary* Create(SortStyle sortStyle, StringCompareStyle compareStyle)

Creates a new empty Dictionary of the given properties. If you don't pass any options, the Dirctionary is non sorted and case insensitive.

Example:

    Dictionary* myDictionary = Dictionary.Create();

will fade the screen to black, wait 1 sec (40 game cycles) and then fade
in again.

*See Also:* [Set](Set#create)

---

### Clear

    Clear()

Removes all items from the dictionary.

---

### Set

    bool Set(String key)

Assigns a value to the given key, adds this key if it did not exist yet.

---

### Contains

    bool Contains(String key)

Returns true if the key is in the dictionary.

Example:

    Dictionary* myDictionary = Dictionary.Create();
    myDictionary.Set("my-key","my-value");
    if(myDictionary.Contains("my-key")){
      Display("has my key!");
    }

will fade the screen to black, wait 1 sec (40 game cycles) and then fade
in again.

*See Also:* [Remove](Dictionary#remove)

---

### Get

    String Get(String key)

Gets value by the key. Returns null if such key does not exist.

Example:

    Dictionary* myDictionary = Dictionary.Create();
    myDictionary.Set("a-key","a-value");
    String myValue = myDictionary.Get("a-key");


---

### Remove

    bool Remove(String key)

Removes key/value pair from the dictionary, returns false if there was no such item.

*See Also:* [Set](Dictionary#set)

---

### CompareStyle

    StringCompareStyle CompareStyle

Gets if this dictionary keys are case-sensitive.

*See Also:* [SortStyle](Dictionary#sortstyle)

---

### SortStyle

    SortStyle SortStyle

Gets the method keys are arranged in this dictionary.

*See Also:* [CompareStyle](Dictionary#comparestyle)

---

### ItemCount

    int ItemCount

Gets the number of key/value pairs currently in the dictionary.

---

### GetKeysAsArray

    String[] GetKeysAsArray()

Creates a dynamic array filled with keys in same order as they are stored in the Dictionary.

Example:

    Dictionary* myDictionary = Dictionary.Create();
    myDictionary.Set("my-key1","my-value1");
    myDictionary.Set("my-key2","my-value2");
    String* myDictionaryKeysAsArray = myDictionary.GetKeysAsArray();
    
---

### GetValuesAsArray

    String[] GetValuesAsArray()

Creates a dynamic array filled with values in same order as they are stored in the Dictionary.

Example:

    Dictionary* myDictionary = Dictionary.Create();
    myDictionary.Set("my-key1","my-value1");
    myDictionary.Set("my-key2","my-value2");
    String* myDictionaryValuesAsArray = myDictionary.GetValuesAsArray();

---