## Standard Types

Standard Types are managed structs available that can be used pass values to the script API, and return values. You can also use them in your scripts. For now, AGS only has point available.

### Point

    managed struct Point {
        int x, y;
    };

Point is a very simple struct containing an `x` and an `y` value, useful to indicate a position on the room or the screen.

    Point* target = new Point;
    target.x = 225;
    target.y = 80;

