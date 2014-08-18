#What is this?
This is the DivinEntity noteskin for OpenITG/ITG/StepMania 3.95 presented by DivinElegy.

This master branch of the project will always be the latest stable release and should always remain backwards compatible with existing simfiles.

#Why?
The existing "God" and "Satan" NoteSkins floating around the Internet are ugly behomoths of cobbled together code with no real structure. They are hard for a novice to know how to use (and even for a relative expert). The DivinEntity NoteSkin aims to empower step artists with creative tools to make the best simfiles possible, without having to deal with too much bullshit.

From a code point of view, the main goal of the DivinEntity NoteSkin is to remove as much Lua as possible from XML files and keep everything neat, organised and maintainable.

#How?
For detailed documentation on the NoteSkin, see the readme in the [DivinEntity folder](https://github.com/DivinElegy/DivinEntity-Noteskin/tree/master/NoteSkins/dance/DivinEntity)

The central idea of this NoteSkin is to provide functions that expose out elements of the NoteSkin for use in a simfile. Every function will return a _table_ of Actors. The neat thing about these tables is that you can run Actor commands on them, and every element in the table will have that command applied to it. For example:

```Lua
DIVINE_ENTITY:GetTapNotes('Down', '4th'):Load('mySprite.sprite')
```

Will replace the graphic for every down 4th note with mySprite.sprite.

The table also has a fluent interface, allowing you to chain functions without having to start a new line. For example:

```Lua
DIVINE_ENTITY:GetTapNotes('Down', '4th'):Load('mySprite.sprite'):vibrate()
```

Will load mySprite and cause all the notes to vibrate.

The functions always return as many actors as possible based on their arguments. Here are specific examples for GetTapNotes:

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

#Installation
To install the NoteSkin follow these steps:

1. Download the NoteSkin using the "Download ZIP" button to the right.
2. Extract the zip to your desktop (or wherever else you'd like).
3. Copy the NoteSkins directory to the _root_ of your OpenITG/SM install. For example if you have OpenITG installed in C:\Program Files\OpenITG, simply copy the NoteSkins folder from the zip in to C:\Program Files\OpenITG

Windows might prompt you about an existing NoteSkins folder. Make sure you tell it to _merge_ the two folders.

#Functions
Below is a list of functions you can use to access and modify NoteSkin elements:

**DIVINE_ENTITY:GetTapNotes(direction, quant, clone)**
    
**DIVINE_ENTITY:GetActiveHoldHeads(direction, quant)**
    
**DIVINE_ENTITY:GetInactiveHoldHeads(direction, quant)**

**DIVINE_ENTITY:GetActiveRollHeads(direction, quant)**
    
**DIVINE_ENTITY:GetInactiveRollHeads(direction, quant)**

**DIVINE_ENTITY:GetMines(direction)**
    
**DIVINE_ENTITY:GetTapExplosions(direction, explosionType, TNS)**

In each function, ```direction``` can be one of "Up", "Down", "Left" and "Right" and ```quant``` can be any note quantity from "4th" to "192nd". In ```GetTapExplosions```, ```explosionType``` can be either "Dim" or "Bright" (bright explosions occur when the player's combo is above 100) and ```TNS``` can be one of "Marvelous", "Perfect", "Great", "Good", "Boo", "Miss" or "HitMine".

#Message Commands
Below is a list of message commands the NoteSkin broadcasts.

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

#Contributing
If you feel you have something of value to add to this project, _please_ make a fork under your own GitHub account, then send a pull request. This is the best way to keep track of changes and give credit where credit is due. Thanks.

#Maintainer
This NoteSkin is maintained by Cameron Ball.

#Acknowledgments
This noteskin would not exist were it not for the hard work by the following people:

- Alan James (https://www.youtube.com/taro4012)
- Nick Psyhogios (https://www.youtube.com/WinDEU)
- Jona Day (https://www.youtube.com/puurokulho)
- Jayce Newton (https://www.youtube.com/divinejayce)
- Cameron Ball
