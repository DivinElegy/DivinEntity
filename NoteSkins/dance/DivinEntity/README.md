#What is the "Divine Entity"?

This NoteSkin sets up a Lua object (well, table really) called DIVINE_ENTITY, which is global and acessible from inside a simfile (as long as the "DivinEntity" NoteSkin is selected, obviously).

DIVINE_ENTITY is essential a registry of actors accessed through simple methods. It does all the hard work of figuring out which player an actor belongs to, as well as some extra Lua magic to provide an easy API for running commands on multiple actors.

#Implementation

The implementation of the Divine Entity is reasonably simple. To the best of my knowledge, the first XML file loaded from the DivinEntity NoteSkin is [Left Tap Note 4th.xml](https://github.com/DivinElegy/DivinEntity-Noteskin/blob/de-wip/NoteSkins/dance/DivinEntity/Left%20Tap%20Note%204th.xml). This is the file where the majority of implementation takes place. DIVINE_ENTITY is a global Lua object with some methods to make life easy.

The way that DIVINE_ENTITY knows about NoteSkin actors is through the "register" methods. In the vast majority of XML files there is something like this sample from [Down Tap Note 16th.xml](https://github.com/DivinElegy/DivinEntity-Noteskin/blob/de-wip/NoteSkins/dance/DivinEntity/Down%20Tap%20Note%2016th.xml):

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
**This is an incomplete reference guide to DIVINE_ENTITY's methods. It will likely change in the future**

_void_ **registerReceptor(direction, actor)** - Register ```actor``` as the receptor associated with ```direction```

_void_ **receptorPressed(actor)** - Respond to ```actor``` being pressed. This function is responsible for updating DIVINE_ENTITY's internal actor states and broadcasting message commands. For an example of this being used, see [Left Receptor Go.xml](https://github.com/DivinElegy/DivinEntity-Noteskin/blob/de-wip/NoteSkins/dance/DivinEntity/Left%20Receptor%20Go.xml)

_void_ **receptorLifted(actor)** - Respond to ```actor``` being lifted. This function is responsible for updating DIVINE_ENTITY's internal actor states and broadcasting message commands. For an example of this being used, see [Left Receptor Go.xml](https://github.com/DivinElegy/DivinEntity-Noteskin/blob/de-wip/NoteSkins/dance/DivinEntity/Left%20Receptor%20Go.xml)

_bool_ **isReceptorPressed(direction, player)** - Return true if the receptor associated with ```direction``` and ```player``` is currently pressed. Return false otherwise.

_bool_ ***getReceptorState(direction, player)*** - Get the current internal state of the receptor associated with ```player``` and ```direction```

_void_ ***registerTapArrow(name)*** - Register ```actor``` as the tap arrow associated with ```name```

_table_ ***getTapArrows(direction, quant)*** - Return a table of actors which have associations with ```direction``` and ```quant```. It returns a table with a fluent interface allowing you to run actor commands on every actor it contains.

#Usage Examples
Get all tap arrows:

```Lua
DIVINE_ENTITY:getTapArrows()
```

Get all tap arrows associated with the direction 'Down':

```Lua
DIVINE_ENTITY:getTapArrows('Down')
```

Get all tap arrows associated with the quantity 16th:

```Lua
DIVINE_ENTITY:getTapArrows(nil, '16th')
```

Get only Left Tap Note 64th:

```Lua
DIVINE_ENTITY:getTapArrows('Left', '64th')
```

Reload the sprite for all actors associated with the direction 'Left':

```Lua
DIVINE_ENTITY:getTapArrows('Left'):Load('mySprite.sprite')
```

Chain commands using the fluent interface:

```Lua
DIVINE_ENTITY:getTapArrows():linear(300):rotationz(7200)
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
        if DIVINE_ENTITY:isReceptorPressed('Down', PLAYER_1) then self:addy(1)  end
        if DIVINE_ENTITY:isReceptorPressed('Up', PLAYER_1) then self:addy(-1) end
                   
        --left/right
        if DIVINE_ENTITY:isReceptorPressed('Right', PLAYER_1) then self:addx(1) end
        if DIVINE_ENTITY:isReceptorPressed('Left', PLAYER_1) then self:addx(-1) end
                       
        self:sleep(0.0166666666);
        self:queuecommand('Update');
    end"
/>
```
