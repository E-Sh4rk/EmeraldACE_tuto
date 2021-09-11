**The bad eggs created in this tutorial should not be moved in your party: it could corrupt them.**

# Freezer bad egg

The *freezer bad egg* is a bad egg that can be used to run any piece of code each frame. It can be used, among other things, to *freeze* the value of a memory address.

## Prerequisite

- An ACE glitch species (for instance 0x40E9 for the english version)
- If you use a glitch species that executes Thumb code such as 0x40E9, you will also need a Thumb->ARM bootstrap
- A [certificate exit code bootstrap](exit-code.md) (you can place it in the first slot of BOX 14 for instance). Note that it does not matter if you have renamed your BOX 14 as the creation of this bad egg uses the hexadecimal-writer bad egg
- The [hexadecimal-writer and crafting table bad eggs](hex-writer.md)

## Let's go

NOTE: the codes given here are for the english version. The freezer itself should also work on other european versions (not tested yet), but the code you want to execute each frame must be adapted to your version.

Ensure the first two slots of your crafting table area are empty, and execute the hexadecimal-writer bad egg two times **without looking at BOX 12** (or where your crafting table area is) between the execution of the two codes:

```
=============== CODE 1 ===============

Box  1: 07182DE9
Box  2: 06F04FE2
Box  3: 38109FE5
Box  4: 3C008FE2
Box  5: 000000FF
Box  6: 4B2EA0E3
Box  7: 00000BEF
Box  8: 28B09FE5
Box  9: 04B021E5
Box 10: 18C09FE5
Boxes 11-14: 00000000

=============== CODE 2 ===============

Box  1: 00B09CE5
Box  2: 01005BE1
Box  3: 04B00115
Box  4: 04101105
Box  5: 00108CE5
Box  6: 0718BDE8
Box  7: 10FF2FE1
Box  8: FC7F0003
Box  9: 08F00302
Box 10: 0C001FE5
Boxes 11-14: 00000000
```

You should now have a bad egg in the first slot of your crafting table (and the second slot should still be empty).

## Testing everything worked

We are gonna test our newly created freezer bad egg with a simple script that will basically freeze the PRNG seed to the value 0. Execute the hexadecimal-writer bad egg with this data (your freezer bad egg should still be in the first slot of your crafting table):

```
Box  1: 0CC09FE5
Box  2: 00B0A0E3
Box  3: 00B0ACE5
Box  4: 10FF2FE1
Box  5: 00000002
Box  6: 805D0003
Box  7: 00000000 
Box  8: 081C0000
Box  9: 9C700000
Boxes 10-14: 00000000
```

It will generate an Articuno in the second slot of the crafting table. This Articuno contains the code that will be executed each frame by the freezer. Now, move the freezer in BOX 14 slot 3 and the Articuno in BOX 14 slot 4 (or somewhere else depending on where you put your exit code bootstrap: it should be at least 2 slots after the exit code bootstrap).

Now, trigger the ACE and observe the world: the NPCs should always do the same moves, there should be no wild Pokemon in the grass, etc. Trigger the ACE again: everything should be back to normal.

For information, the code contained in the Articuno is the following:
```
ldr r12, [pc, 12]
mov r11, 0
str r11, [r12]!
bx r0
0x02000000
0x03005D80
... (some additional data in order to have a valid Pokemon)
```

## How to use it

Here are some explanations about how to use the freezer bad egg:

- When you want to execute the freezer bad egg, you should put it at least two slots AFTER the exit code bootstrap. When you don't want to execute it (in order to execute the hexadecimal writer or standard ACE), you should put it in the crafting table area or before the last row of BOX 11.
- The code to execute each frame should be placed in the 30-slots area starting at the slot just after the freezer. It is not an issue if this area contains some other data as long as the code to execute is the first.
- The code to execute must end with a `BX r0` command.
It should also preserve the other registers (of course, if you modify `r0`, restore its value before calling `BX r0`). Note that the code will be copied before being executed each frame, so do not expect `PC` to point inside the PC storage.
- The freezer bad egg works like a toggle that enable/disable the execution on each frame of the provided code. The state of this toggle is not persistent: it will always be disabled after a save and restart.
