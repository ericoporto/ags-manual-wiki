## Standard Types

Standard Types are managed structs used for passing and returning values in the script API. You can also use them in your scripts. For now, AGS only has point available.

### Point

```ags
managed struct Point {
    int x, y;
};
```

Point is a very simple struct containing an `x` and an `y` value, useful to indicate a position on the room or the screen.

```ags
Point* target = new Point;
target.x = 225;
target.y = 80;
```

