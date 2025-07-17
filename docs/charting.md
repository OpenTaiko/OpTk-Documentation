# Charting

OpenTaiko uses the TJA format for charting songs. They can be opened with any text editor, or with a visual editor such as PeepoDrumKit. Below is a list of note types used.

## Note Types

There are many notes supported by OpenTaiko. Some are commonly used in every chart, while others appear less often. Some may also be exclusive to other modes, or have different behaviors.

### Taiko Notes

Listed here are common note types used in Taiko mode.

|ID|Name|Details|
|:---:|:---:|:---:|
|0|Empty|Essential in spacing apart notes, as well as assisting in creating complex patterns.|
|1|Don||
|2|Ka||
|3|Don (Large)||
|4|Ka (Large)||
|5|Start of Drumroll|Marks the beginning of a drumroll. Use 0 to increase the length of the drumroll, and 8 to end the drumroll.|
|6|Start of Drumroll (Large)|Marks the beginning of a drumroll. Use 0 to increase the length of the drumroll, and 8 to end the drumroll.|
|7|Start of Balloon|Marks the beginning of a balloon. Use 0 to increase the length of the drumroll, and 8 to end the drumroll.<br>Similar to the drumroll, but must be hit a certain amount within a time limit to be cleared. Balloon value is specified by the `BALLOON` tag.|
|8|End of long note|Marks the end of any long (drumroll/balloon) note.|
|9|Start of Kusudama|Marks the beginning of a kusudama. Use 0 to increase the length of the drumroll, and 8 to end the drumroll.<br>Similar to the drumroll, but must be hit a certain amount within a time limit to be cleared. In addition, the value of all active players' Kusudama values are combined, and can be hit by all players. Kusudama value is specified by the `BALLOON` tag.|
|A|Don (Large - Both)|Displays connected hands when playing a chart in multiplayer & the note appear aligned together.|
|B|Ka (Large - Both)|Displays connected hands when playing a chart in multiplayer & the note appear aligned together.|

### Konga Notes

Listed here are common note types used in Konga mode.

Many of them are already used in Taiko mode, but a few are exclusively used in this gamemode.

|ID|Name|Details|
|:---:|:---:|:---:|
|0|Empty|Essential in spacing apart notes, as well as assisting in creating complex patterns.|
|1|Right||
|2|Left||
|3|Double||
|4|Clap||
|5|Start of Right Drumroll|Marks the beginning of a drumroll. Use 0 to increase the length of the drumroll, and 8 to end the drumroll.|
|6|Start of Double Drumroll|Marks the beginning of a drumroll. Use 0 to increase the length of the drumroll, and 8 to end the drumroll.|
|7|Start of Balloon|Marks the beginning of a balloon. Use 0 to increase the length of the drumroll, and 8 to end the drumroll.<br>Similar to the drumroll, but must be hit a certain amount within a time limit to be cleared. Balloon value is specified by the `BALLOON` tag.|
|8|End of long note|Marks the end of any long (drumroll/balloon) note.|
|9|Start of Kusudama|Marks the beginning of a kusudama. Use 0 to increase the length of the drumroll, and 8 to end the drumroll.<br>Similar to the drumroll, but must be hit a certain amount within a time limit to be cleared. In addition, the value of all active players' Kusudama values are combined, and can be hit by all players. Kusudama value is specified by the `BALLOON` tag.|
|A|Double?|(Currently unknown if hands are displayed in multiplayer)|
|B|Clap?|(Currently unknown if hands are displayed in multiplayer)|
|I|Start of Left Drumroll|Marks the beginning of a drumroll. Use 0 to increase the length of the drumroll, and 8 to end the drumroll.<br>Becomes a small drumroll in Taiko Mode.|
|H|Start of Clap Drumroll|Marks the beginning of a drumroll. Use 0 to increase the length of the drumroll, and 8 to end the drumroll.<br>Becomes a large drumroll in Taiko Mode.|

### Miscellaneous Notes

Listed here are miscellaneous notes used in all modes.

These note types are not regularly used in normal charts. You'll typically only find them in gimmick charts.

|ID|Name|Details|
|:---:|:---:|:---:|
|C|Bomb|A note that players should actively avoid hitting. Breaks combo and drastically drops gauge if hit.|
|F|Adlib|Appears invisible by default, does not affect current combo, does not add onto the player's current score, and is not required to be hit. If hit, a special hitsound plays.|
|G|Kadon|Requires the player to hit both don & ka. In Konga Mode, this appear as a Double note.|
|D|Start of Fuse Roll|Marks the beginning of a drumroll. Use 0 to increase the length of the drumroll, and 8 to end the drumroll.<br>Behaves similarly to Balloon, but must be broken in time. If the user fails, it will behave like a Bomb note, breaking combo and damaging their current gauge. Fuse Roll value is specified by the `BALLOON` tag.|