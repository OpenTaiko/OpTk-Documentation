# Skinning & Customization

In addition to OpenTaiko's default skins, users are able to create their own skins.

## Lua Scripting

OpenTaiko's Lua API allows creators to further customize their skin beyond just replacing textures and sounds, allowing for more dynamic visuals without the need to modify the game's source code. While most menus can have Lua scripts, most scripts are only suited for animating backgrounds at this time. The capabilities of our Lua API are still a work in progress, and will expand in the future.

Read-only variables are also provided by OpenTaiko, allowing the creator to change the behavior of their script based on what is happening at that moment.

Some examples of what can be done with Lua include :

* Being able to read the BPM, gauge percentage, go-go state, and clear status of each active player, and change how visuals are animated using these values.
* Checking what language the user is currently using, allowing for localization support for skins.
* Changing the visuals of a background depending on their Tower progress or AI battle state.

### Calling Functions

Calling Functions are commands that you send to OpenTaiko to execute a function.

Most of these functions are related to drawing and manipulating textures that your script imports, and does not modify the game itself.

|Function|Input Type(s)|Description|
|:---:|:---:|:---:|
|<u>**Console Drawing**</u>|-|-|
|func:DrawText(x, y, text)|integer, integer, string|Draws text using the skin's Console Font. (/Graphics/Console_Font.png)|
|func:DrawNum(x, y, num)|integer, integer, number|Draws a number using the skin's Console Font. (/Graphics/Console_Font.png)|
|<u>**Image Drawing**</u>|-|-|
|func:AddGraph(filepath)|string|Load an image file to be used for your script. This is mandatory for drawing functions to work on your image.|
|func:DrawGraph(x, y, filepath)|integer, integer, string|Draw a given image at a position.|
|func:DrawGraphCenter(x, y, filepath)|integer, integer, string|Draw a given image at a position, centered at the given coordinates.|
|func:DrawRectGraph(x, y, rect_x, rect_y, rect_width, rect_height, filepath)|integer, integer, integer, integer, integer, integer, string|Draw a given image at a position.<br>A rectangle is used to specify what portion of the image you want to draw.<br>If a rectangle goes outside the bounds of the given image, it will loop back to continue drawing. This method can be used to repeat textures.|
|func:DrawGraphRectCenter(x, y, rect_x, rect_y, rect_width, rect_height, filepath)|integer, integer, integer, integer, integer, integer, string|Draw a given image at a position, centered at the given coordinates.<br>A rectangle is used to specify what portion of the image you want to draw.<br>If a rectangle goes outside the bounds of the given image, it will loop back to continue drawing. This method can be used to repeat textures.|
|<u>**Image Manipulation**</u>|-|-|
|func:SetScale(x_scale, y_scale, filepath)|number, number, string|Set the scale of your image. 1.0 is the default value.|
|func:SetRotation(rotation, filepath)|number, string|Set the rotation of your image. Value is typically between 0 and 360.|
|func:SetOpacity(opacity, filepath)|integer, string|Set the opacity of a given image. Value must be between 0 and 255.|
|func:SetColor(r, g, b, filepath)|number, number, number, string|Use a Multiply filter to recolor your image. All values must be between 0.0 and 1.0.|
|func:SetBlendMode(mode, filepath)|string, string|Specify how an image should blend into the background.<br>Blend modes available are: "Normal", "Add", "Multi" (Multiply), "Sub" (Subtract), "Screen"|
|<u>**Image Information**</u>|-|-|
|func:GetTextureWidth(filepath)|string|Get the width of the loaded texture. Returns -1 if the texture is nil.|
|func:GetTextureHeight(filepath)|string|Get the height of the loaded texture. Returns -1 if the texture is nil.|

### Receiving Functions

Receiving Functions are commands that OpenTaiko sends to your script.

Some of these functions are called every frame, while others are only called when necessary. Some can also be called multiple times per frame.

|Function|Variable Type(s)|Description|
|:---:|:---:|:---:|
|<u>**General**</u>|||
|function init()|-|Called once when the script is first loaded. This is used to initialize data, including images.|
|function update()|-|Called once every frame. Used to calculate & update values. Temporarily stops being called if the game is paused.<br>This is always called before draw().|
|function draw()|-|Called once every frame. Used to manipulate and draw images.|
|<u>**In-Game Only**</u>|||
|function clearIn(player)|integer|Called once when a player has reached the clear range. The player value is the player ID that has entered the clear range.<br>The player ID starts at 0 and ends at 4.<br>0 for 1P, 1 for 2P, 2 for 3P, etc.|
|function clearOut(player)|integer|Called once when a player has dropped from the clear range. The player value is the player ID that has dropped from the clear range.|
|<u>**In-Game Only (Kusudama)**</u>|||
|function kusuIn()|-|Called once when a Kusudama sequence has started.|
|function kusuBroke()|-|Called once when a Kusudama was successfully cleared.|
|function kusuMiss()|-|Called once when a Kusudama has failed to clear before the sequence has ended.|
|<u>**In-Game Only (Ending)**</u>|||
|function update(player)|integer|Called every frame. Used to calculate & update values. Unlike the original function, this is called for each player ID qualified to run this script.<br>Can run multiple times in a single frame.|
|function draw(player)|integer|Called every frame. Used to manipulate & draw images. Unlike the original function, this is called for each player ID qualified to run this script.<br>Can run multiple times in a single frame.|
|function playEndAnime(player)|integer|Called once when a course is finished. The player value is the player ID qualified to run this script.<br>Can run multiple times in a single frame.|
|<u>**Results Only**</u>|||
function skipAnime()|-|Called once when any player skips the Results Screen animation.|
|<u>**Song Select Only**</u>|||
function playAnime()|-|Called when a player on the difficulty select screen swaps between Extreme and Extra difficulty.<br>Animation duration is specified in the Skin Config files.|

### Variables

OpenTaiko gives variables with read-only values to get details about what's happening at that moment.

Some details include information about what state a player is in, while others may provide detail about the gamemode status or certain application parameters.

Because these variables are already reserved, you can not create your own variables with the same names as the ones listed below.

|Variable Name|Type|Description|
|:---:|:---:|:---:|
|<u>**Application Information**</u>|
|fps|integer|Gets the framerate of the application.|
|deltaTime|number|Gets the amount of time that has passed since the last frame was drawn.<br>Non-integral, valued in seconds (i.e. 0.0166666...)|
|lang|string|Gets the current selected language as a short string format.<br>(i.e. "en", "ja", "fr", etc.)|
|<u>**Player Information**</u>|
|playerCount|integer|Gets the current number of active players.|
|p1IsBlue|boolean|Gets a bool stating if Player 1 is blue. (via. selecting Right in the title menu)<br>1P only; Returns false if not blue, or if there are 2 or more players.|
|characterRarities|string[]|Gets each player's Character rarity.<br>Possible rarities: "Poor"/"Common"/"Uncommon"/"Rare"/"Epic"/"Legendary"/"Mythical"|
|puchicharaRarities|string[]|Gets each player's Puchichara rarity.<br>Possible rarities: "Poor"/"Common"/"Uncommon"/"Rare"/"Epic"/"Legendary"/"Mythical"|
|<u>**Player Information (In-Game)**</u>|
|bpm|number[]|Gets a list of numbers for each player that tell what BPM their chart is currently on.<br>Can be different for each player.|
|gauge|number[]|Gets a list of numbers between 0-100 for each player that tell where the player is on the soul gauge.|
|isClear|boolean[]|Gets a list of booleans for each player that tell if each player is clearing their course.|
|gogo|boolean[]|Gets a list of booleans for each player that tell if Go-Go Time is currently active.|
|<u>**Gameplay Information**</u>|
|timeStamp|number|Gets the amount of time in seconds that have passed since the chart has begun, beginning at the first measure.<br>Can be negative if the chart hasn't started yet.|
|<u>**Tower Information**</u>|
|towerNightNum|number|Gets a number starting at 0 and going up to (but not always ending at) 1, which changes depending on how far the player has progressed through a Tower.<br>The source code determining towerNightNum's value is: `Math.Min(CurrentMeasure / Math.Max(140, MaxFloorCount / 2), 1);`|
|<u>**AI Battle Information**</u>|
|battleState|integer|Gets a number related to the current state of the active AI Battle, valued between -9 and 9. Default is 0.<br>Zero or higher number means the player is winning. Negative number means the AI is winning.|
|battleWin|boolean|Gets a bool stating if the player is winning (or has won) against the AI in AI Battle.<br>Can also be used in the Results Screen menu.|