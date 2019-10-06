## Tumbleweed Unhandled Events

In order to give a the player a feedback for actions the author hasn't thought
of, unhandled events come into play.
With a single function, you can achieve something like "That doesn't work" or
"I can't pull that", which makes a game much more authentic and alive.
The messages itself are defined outside of this function, initially in TemplateSettings.asc

---

### Verbs.Unhandled

```
void Verbs.Unhandled(int door_script);
```

Use this function at the end of your any_click functions in order to cause default reactions. For example:

```
function cChar_AnyClick()
{
        if (Verbs.UsedAction(eGA_LookAt)) player.Say("He looks like he is hungry.");
        else Verbs.Unhandled();
}
```

In this example, you get a default reaction for everything but look at. The optional parameter is only used internally to make the function work with the door scripts.

