# Commands for interacting the the game

These commands allow chat to interact with the game while the song is playing. Alternatively, the actions that are called by these commands can be used with Channel Points redemption.

## Commands

1. Ragnarock - AHOU:`!r-ahou {left|right|first|second|third|fourth}`

    Triggers the same cherring animation in-game as when the shields are hit.
    
    Without the optional parameter (just `!r-ahou`) - all vikings will cheer, or you can specify which column/row should cheer with the parameter.

    Example: `!r-ahou left` - all four vikings on the left will cheer.

    **Note**: This is animation only. If you want to have the sound as well, you'll need to add a separate sub-action to `Ragnarock - AHOU` action to play a sound file.

2. Ragnarock - Hammer: `!r-hammer {hammerNameOrId} {left|right|both}`

    Changes the hammer for selected hand until the song ends or the hammer is changed again.

    When used without parameters (just `!r-hammer`), an explanation is displayed on how to use it (list of hammers is NOT displayed, as it's way too long). Without the second parameter, both hammers will be changed.

    Unknown hammer names, ids, or hammers you haven't unlocked yet will change your hammer to the original hammer skin (the one everyone starts with, not the one you started the song with).

    Examples:

    1. `!r-hammer Odin left` - changes left hand hammer to the Odin hammer
    2. `!r-hammer 16` - changes both hammers to Chicken Drumsticks

    List of supported hammers and their ids can be found [here](https://github.com/Brollyy/RagnarockWebsocketUtil/blob/master/src/RagnarockWebsocketCore/Enums/Hammer.cs).

3. Ragnarock - Song Info: `!r-song`

    Triggers a bot response in chat with the title and artist of the currently playing song.

## Installation

1. Import `RagnarockInteractionCommands.bot` into Streamer.bot to add the actions and commands.
![alt text](image.png)
2. Go to Commands tab and enable the commands you want to use (you can also adjust things like cooldowns or permissions if you want).
![alt text](commands.png)

## Interactions

### AHOU

1. `Ragnarock - AHOU` command - `!r-ahou`
2. `Ragnarock - AHOU` action that parses the input provided to `!r-ahou` command, sets arguments and calls `Ragnarock AHOU Animation`.
3. `Ragnarock AHOU Animation` action that communicates with the game.
    This action can be used as a standalone to trigger the animation with different triggers. 
    
    Before calling this action, you need to set below arguments.

    | Argument   | Type         | Note        | Example |
    | ---------- | ------------ | ----------- | ------- |
    | `rowersId` | `Array[int]` | Determines which vikings will do the animation. See [documentation](https://github.com/Brollyy/RagnarockWebsocketUtil/blob/master/src/RagnarockWebsocketCore/Enums/Rowers.cs). | `[0, 1, 4, 8]` |

### Change hammers

1. `Ragnarock - Change Hammer` command - `!r-hammer`
2. `Ragnarock - Hammer` action that parses the input provided to `!r-hammer` command, sets arguments and calls `Ragnarock Change Hammer`.
3. `Ragnarock Change Hammer` action that communicates with the game.
    This action can be used as a standalone to change the hammers with different triggers. 
    
    Before calling this action, you need to set below arguments.

    | Argument     | Type         | Note        | Example |
    | ------------ | ------------ | ----------- | ------- |
    | `hammerId`   | `int`        | See [documentation](https://github.com/Brollyy/RagnarockWebsocketUtil/blob/master/src/RagnarockWebsocketCore/Enums/Hammer.cs). | `12` |
    | `hammerHand` | `string`     | See [documentation](https://github.com/Brollyy/RagnarockWebsocketUtil/blob/master/src/RagnarockWebsocketCore/Enums/HammerHand.cs). | `left` |

### Song Info

1. `Ragnarock - Song Info` command - `!r-song`
2. `Ragnarock - Song Info` action requests that the game sends the song info as a response to `!r-song` command. This action can be used as a standalone to request song info with different triggers.
3. `Ragnarock - On Song Info` action that handles the incoming event from the game and sends a message with song info to chat.

### Show Dialog

1. `Ragnarock Show Dialog` action that can be used to display a dialog window in-game with different triggers. 
    
    Before calling this action, you need to set below arguments.

    | Argument          | Type         | Note        | Example |
    | ----------------- | ------------ | ----------- | ------- |
    | `dialogId`        | `string`     | Unique identifier, different values will display different windows. | `dialog` |
    | `dialogTitle`     | `string`     | Title of the dialog window | `Window` |
    | `dialogLocationX` | `double`     | X location of the dialog window | `0,0` |
    | `dialogLocationY` | `double`     | Y location of the dialog window | `0,0` |
    | `dialogLocationZ` | `double`     | Z location of the dialog window | `0,0` |
    | `dialogMessage`   | `string`     | Message in the dialog window | `bla bla bla...` |
    | `dialogDuration`  | `double`     | How long the dialog window will be visible (in seconds) | `5,0` |

    Sending a second event for the same `dialogId` will override previous settings (location/message/duration/etc.).

    Location: `(0, 0, 0)` is roughly where the song timer is on the boat.
    Varying X moves the dialog window further for negative values and closer for positive values, Y - right for negative, left for positive, Z - down for negative, up for positive. For testing it's best to move by around 100 units to find the spot you're looking for.

    An example of an action that sets the arguments and displays the dialog on every Twitch chat message can be found in `ExampleDialogAction.bot`.