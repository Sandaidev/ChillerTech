---
title: Designing modular worlds within a CLI game
---

So here's the plan: you're creating a CLI-based game and you want to make a modular world design, with the player going where they want.

Some people will be doing it using functions/classes but it's very clunky and the code becomes very complicated for no real benefit, since the system is "room-based", with each room containing its own data, the best way to do it is by using dicts!

Here's how you might do it as well :

```python
world_rooms = {
	"ROOM1": {
    	"NAME": "The first room",
        "DESC": "It seems quite empty...",
        "NORTH": "ROOM2",
        "SOUTH": None,
        "EAST": None,
        "WEST": None
	}
    
    "ROOM2": {
    	"NAME": "The second room",
        "DESC": "This room is kinda like the first.",
        "NORTH": None,
        "SOUTH": "ROOM1",
        "EAST": None,
        "WEST": None
	}
}
```

Here you can see that we have two rooms containing their own data, but following the same template, `"NAME"` will contain the name of the room presented to the player, `"DESC"` contains a longer and more descriptive string about the room and `"NORTH"`, `"SOUTH"`, `"EAST"` and `"WEST"` should point to the ID of another room, if not, it should be `None`.

This gives us the opportunity to add lots of rooms fast, and it can be used on other concepts as well, take items or enemies for example! you can setup a dict of items containing their own data, if they can be used or not with the `"USABLE": True` for example.

Enemies can have a health range, like `"HEALTH_RANGE": [100, 200]` that should be used with a random number generator to create an enemy with that health range!

I hope that tip helped you creating your CLI-based game!

See ya!




