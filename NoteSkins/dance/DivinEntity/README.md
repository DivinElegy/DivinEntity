#What is the "Divine Entity"?
This NoteSkin sets up a Lua object (well, table really) called DIVINE_ENTITY, which is global and acessible from inside a simfile (as long as the "DivinEntity" NoteSkin is selected, obviously).

DIVINE_ENTITY is essential a registry of actors accessed through simple methods. It does all the hard work of figuring out which player an actor belongs to, as well as some extra Lua magic to provide an easy API for running commands on multiple actors.

#Implementation
The implementation of the Divine Entity is reasonably simple. To the best of my knowledge, the first XML file loaded from the DivinEntity NoteSkin is [Left Tap Note 4th.xml](https://github.com/DivinElegy/DivinEntity-Noteskin/blob/master/NoteSkins/dance/DivinEntity/Left%20Tap%20Note%204th.xml). This is the file where the majority of implementation takes place. DIVINE_ENTITY is a global Lua object with some methods to make life easy.

The way that DIVINE_ENTITY knows about NoteSkin actors is through the "register" methods. In the vast majority of XML files there is something like this sample from [Down Tap Note 16th.xml](https://github.com/DivinElegy/DivinEntity-Noteskin/blob/master/NoteSkins/dance/DivinEntity/Down%20Tap%20Note%2016th.xml):

```XML
<Actor
    File='sprites/16th.sprite'
    InitCommand='%function (self)
        DIVINE_ENTITY:registerTapArrow("Down Tap Note 16th", self)
        self:rotationz(90);
    end'
/>
```

Using this technique DIVINE_ENTITY becomes a registry of every NoteSkin actor.

#Usage
Most functions are defined using : syntax. e.g., ```DIVINE_ENTITY:GetActors```, but ```catch``` and ```contains``` are defined using . syntax. : syntax automatically passes a ```self``` parameter to the function, however this is not needed in the case of  ```catch``` and ```contains```.

Every Get function returns a table with a fluent interface, allowing you to chain actor functions on a single line.

```TNS``` **usually** refers to the tap note score names used internally by StepMania, e.g., "Marvelous", "Perfect" etc. However in ```ReceptorHitNote``` it can really be whatever you like, as that function simply broadcasts a message command using the value of ```TNS```.

Some of these functions are designed to be used internally. **THESE MAY CHANGE IN THE FUTURE**. However, all the functions that expose elements of the NoteSkin out, i.e., all the Get functions, will never change to ensue maximum backwards compatibility in the future.

_table_ **catch(table, key)** - This function is used as a callback for many other table's metatable's __index method. It catches the name of a function to call, and agruments to pass on to it, and then attempts to call that function with those arguments on every element in ```table```. It then returns ```table``` which enables the fluent interface magic of other methods.

_bool_ **contains(str, stringsToFind)** - Returns true if every string in ```stringsToFind``` is contained in ```str```

_table_ **GetActors(actorTable, nameParams)** - Returns all actors in ```actorTable``` which have names matching the parameters in ```nameParams```

_void_ **RegisterReceptor(direction, actor)** - Register ```actor``` as the receptor associated with ```direction```

_table_ **GetReceptors(player, direction, sprite)** - Get all receptors matching ```player```, ```direction``` and ```sprite```. ```sprite``` refers to the the two sprites set up as an overlay and underlay (see [Left Receptor Go.xml](https://github.com/DivinElegy/DivinEntity-Noteskin/blob/master/NoteSkins/dance/DivinEntity/Left%20Receptor%20Go.xml). Valid values for ```sprite``` are 'Over' and 'Under'.

_void_ **ReceptorPressed(actor)** - Respond to ```actor``` being pressed. This function is responsible for updating DIVINE_ENTITY's internal actor states and broadcasting message commands. For an example of this being used, see [Left Receptor Go.xml](https://github.com/DivinElegy/DivinEntity-Noteskin/blob/master/NoteSkins/dance/DivinEntity/Left%20Receptor%20Go.xml)

_void_ **ReceptorLifted(actor)** - Respond to ```actor``` being lifted. This function is responsible for updating DIVINE_ENTITY's internal actor states and broadcasting message commands. For an example of this being used, see [Left Receptor Go.xml](https://github.com/DivinElegy/DivinEntity-Noteskin/blob/master/NoteSkins/dance/DivinEntity/Left%20Receptor%20Go.xml)

_bool_ **IsReceptorPressed(direction, player)** - Return true if the receptor associated with ```direction``` and ```player``` is currently pressed. Return false otherwise.

_bool_ ***GetReceptorState(direction, player)*** - Get the current internal state of the receptor associated with ```player``` and ```direction```

_void_ **ReceptorHitNote(actor, TNS)** - Respond to ```actor``` hitting a note with score TNS. This function is responsible for broadcasting message commands. For an example of this being used, see [Left Receptor Go.xml](https://github.com/DivinElegy/DivinEntity-Noteskin/blob/master/NoteSkins/dance/DivinEntity/Left%20Receptor%20Go.xml)

_void_ ***RegisterNote(noteType, name, actor)*** - Register ```actor``` in the notes table as a ```noteType``` with name ```name```. Other register functions wrap around this one.

_void_ **RegisterTapNote(name, actor)** - Wrapper around ```RegisterNote```. Registers ```actor``` as the note associated with ```name```.

_void_ **RegisterActiveHoldHead(name, actor)** - Wrapper around ```RegisterNote```. Registers ```actor``` as the active hold head associated with ```name```.

_void_ **RegisterInactiveHoldHead(name, actor)** - Wrapper around ```RegisterNote```. Registers ```actor``` as the inactive hold head associated with ```name```.

_void_ **RegisterActiveRollHead(name, actor)** - Wrapper around ```RegisterNote```. Registers ```actor``` as the active roll head associated with ```name```.

_void_ **RegisterInactiveRollHead(name, actor)** - Wrapper around ```RegisterNote```. Registers ```actor``` as the inactive roll head associated with ```name```.

_table_ **GetNotes(noteType, direction, quant, clone)** - Wrapper around ```GetActors```. Returns a table of notes of type ```noteType``` associated with ```direction```, ```quant``` and ```clone```.

_table_ **GetTapNotes(direction, quant, clone)** - Wrapper around ```GetNotes```. Returns a table of tap notes associated with ```direction```, ```quant``` and ```clone```.

_table_ **GetActiveHoldHeads(direction, quant)** - Wrapper around ```GetNotes```. Returns a table of active hold heads associated with ```direction``` and ```quant```.

_table_ **GetInactiveHoldHeads(direction, quant)** - Wrapper around ```GetNotes```. Returns a table of inactive hold heads associated with ```direction``` and ```quant```.

_table_ **GetActiveRollHeads(direction, quant)** - Wrapper around ```GetNotes```. Returns a table of active roll heads associated with ```direction``` and ```quant```.

_table_ **GetInactiveRollHeads(direction, quant)** - Wrapper around ```GetNotes```. Returns a table of inactive roll heads associated with ```direction``` and ```quant```.

_void_ **RegisterMine(name, actor)** - Register ```actor``` as the mine associated with ```name```.

_void_ **RegisterExplosion(noteType, name, actor)** - Register ```actor``` in the explosions table as a ```noteType``` with name ```name```. Other functions wrap around this one.

_table_ **GetExplosions(noteType, direction, explosionType, TNS)** - Returns a table of actors containing the ```noteType``` explosions associated with ```direction```, ``explosionType``` ('Dim' or 'Bright') and score ```TNS```.

_void_ **RegisterTapExplosion(name, actor)**  - Wrapper around ```RegisterExplosion```. Registers ```actor``` as the actor explosion with ```name```.

_void_ **GetTapExplosions(direction, explosionType, TNS)** - Return a table of explosions associated with ```direction```, ```explosionType``` and ```TNS```.

_function_ **GetMetricCallback(section, command)** - Return the callback registered to metric section ```section``` and command ```command```.

_void_ **SetMetricCallback(section, command, callback)** - Set ```callback``` as the callback function for the metric in section ```section``` and command ```command```.

#Message Commands
The NoteSkin also broadcasts messages on certain events. Below is a summary.

**StepP1LeftPressedMessageCommand** - Broadcast when player 1 steps on the left receptor.

**StepP1DownPressedMessageCommand** - Broadcast when player 1 steps on the down receptor.

**StepP1UpPressedMessageCommand** - Broadcast when player 1 steps on the up receptor.

**StepP1RightPressedMessageCommand** - Broadcast when player 1 steps on the right receptor.

**StepP1LeftLiftedMessageCommand** - Broadcast when player 1 lifts off the left receptor.

**StepP1DownLiftedMessageCommand** - Broadcast when player 1 lifts off the down receptor.

**StepP1UpLiftedMessageCommand** - Broadcast when player 1 lifts off the up receptor.

**StepP1RightLiftedMessageCommand** - Broadcast when player 1 lifts off the right receptor.

**P1FantasticMessageCommand** - Broadcast when player 1 gets a Fantastic.

**P1ExcellentMessageCommand** - Broadcast when player 1 gets an Excellent.

**P1GreatMessageCommand** - Broadcast when player 1 gets a Great.

**P1DecentMessageCommand** - Broadcast when player 1 gets a Decent.

**P1WayOffMessageCommand** - Broadcast when player 1 gets a WayOff.

**P1HitMineMessageCommand** - Broadcast when player 1 hits a mine.

The same commands exist for player 2, you just substitute P1 with P2.

#Usage Examples
Get all tap notes:
```Lua
DIVINE_ENTITY:GetTapNotes()
```

Get all tap notes associated with the direction 'Down':

```Lua
DIVINE_ENTITY:GetTapNotes('Down')
```

Get all tap notes associated with the quantity 16th:

```Lua
DIVINE_ENTITY:GetTapNotes(nil, '16th')
```

Get only Left Tap Note 64th:

```Lua
DIVINE_ENTITY:GetTapNotes('Left', '64th')
```

Reload the sprite for all actors associated with the direction 'Left':

```Lua
DIVINE_ENTITY:GetTapNotes('Left'):Load('mySprite.sprite')
```

Chain commands using the fluent interface:

```Lua
DIVINE_ENTITY:GetTapNotes():linear(300):rotationz(7200)
```

Create a player controlled actor:

```XML
<Layer
    File='mySprite.sprite'
    InitCommand="x,SCREEN_CENTER_X;y,SCREEN_CENTER_Y"
    OnCommand="%function(self)
        self:queuecommand('Update')
    end"

    UpdateCommand="%function(self)
        --up/down
        if DIVINE_ENTITY:IsReceptorPressed('Down', PLAYER_1) then self:addy(1)  end
        if DIVINE_ENTITY:IsReceptorPressed('Up', PLAYER_1) then self:addy(-1) end

        --left/right
        if DIVINE_ENTITY:IsReceptorPressed('Right', PLAYER_1) then self:addx(1) end
        if DIVINE_ENTITY:IsReceptorPressed('Left', PLAYER_1) then self:addx(-1) end

        self:sleep(0.01);
        self:queuecommand('Update');
    end"
/>
```

Create a cool effect with the clones:

```Lua
DIVINE_ENTITY:GetTapNotes():hidden(0)

for i = 0,5 do
    DIVINE_ENTITY:GetTapNotes(nil, nil, 'Clone ' .. 5-i):zoom(1-i*0.1)
end
```

Override one of the NoteSkin metrics:

```Lua
DIVINE_ENTITY:SetMetricCallback('ReceptorArrow', 'Marvelous', function(actor) actor:zoom(2) end)
```
