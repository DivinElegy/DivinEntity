#What is this?
**THIS WIP BRANCH IN _NO WAY_ REFLECTS THE FINAL BUILD OF THE NOTESKIN. IT IS HIGHLY SUBJECT TO CHANGE.**

This is the DivinEntity noteskin for OpenITG/ITG/StepMania 3.95 presented by DivinElegy.

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
- Cameron Ball#What is this?
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
