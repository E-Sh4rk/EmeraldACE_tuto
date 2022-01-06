**The bad eggs and Pokemons created in this tutorial should not be marked (unless specified otherwise) or moved in your party: it could corrupt them.**

# New ACE environment 

In this tutorial, we will update your bootstraps (thanks to the hexadecimal writer) so that they become more stable and convenient.
Then, we will create a bad egg (to use with the freezer) that will allow you to trigger ACE just by pressing L+R.

Finally, in the last (optional) part, we will add some more components to our ACE environment allowing the former bad egg to automatically be loaded when your save load.

## Prerequisite

- A stable ACE glitch species such as [0x40E9](stable-ace.md) (with its Thumb->ARM bootstrap)
- A [certificate exit code bootstrap](exit-code.md) (you can place it in the first slot of BOX 14 for instance). Note that it does not matter if you have renamed your BOX 14 as the creation of this bad egg uses the hexadecimal-writer bad egg
- The [hexadecimal-writer and crafting table bad eggs](hex-writer.md)
- The [freezer bad egg](freezer.md) (not required if you just want to update your bootstraps)

## Updating your bootstraps

In this section, we will update the Thumb->ARM bootstrap and the exit code bootstrap in order to make them more stable and convenient. In particular:

- The new Thumb->ARM bootstrap will not depend anymore on the specific sprite animation ACE context, allowing it to work even when ACE is triggered differently.
Moreover, it will work regardless of the current processor mode (Thumb/ARM) and PC-alignment (+0/+2): in every case, it will switch the processor to ARM mode and make the PC register misaligned (+2).
- The new exit code bootstrap will allow us to choose beetwen the Pokedex Completion Diploma and the `lr` exit code just by changing its marking. Moreover, it will not depend on the CPSR flags anymore, making it more stable when used outside of the standard sprite animation ACE context.

The new Thumb->ARM bootstrap (let's call it just *ARM bootstrap* now) can be made with the following code (using the hexadecimal writer):

```
Box  1: 78 46 00 00
Box  2: 00 47 00 00
Box  3: 06 F0 4F E2
Box  4: 3E F0 8F E2
Box  5: 00 00 00 02
Box  6: 00 00 00 00
Box  7: 00 00 00 00
Box  8: A0 11 00 00
Boxes 9-14: 00 00 00 00
```

It should create an Absol. Replace your current Thumb->ARM bootstrap by this one
and trigger ACE again: it should work as before. Store the second Absol that has just been created: you will need it later (if you plan to setup persistence).

The new exit code bootstrap can be made with the following code (using the hexadecimal writer):

```
Box  1: 11 00 DF E5
Box  2: 00 00 50 E3
Box  3: 1A 00 9F E5
Box  4: 00 F0 8F 12
Box  5: 00 00 8E E2
Box  6: 08 F0 8F E2
Box  7: 00 00 00 00
Box  8: 2F 81 00 00
Box  9: 2E 00 00 00
Box 10: 00 00 50 E3
Box 11: 20 F0 8F E2
Box 12: B5 7C 13 08
Boxes 13-14: 00 00 00 00
```

It should create an Abra. When this Abra is marked with any symbol, it will set the exit code to the Pokedex Completion Diploma. When it is unmarked, it will set the exit code to the value of the register `lr`.

*NOTE: you can freely mark/unmark it in order to switch between the two exit codes. However, DO NOT mark/unmark any other element of your ACE setup or it will be corrupted.*

Mark your Abra with any symbol and replace your current exit code bootstrap by this one. Trigger ACE again: it should work as before. Store the second Abra that has just been created: you will need it later (if you plan to setup persistence).

These new bootstraps can be put in the slot just before an ACE component (you do not need to leave one slot empty as it might have been the case for the former bootstraps). We recommand you to use this new layout for your ACE components:

```
BOX 12:
-  -  -  -  -  -
A  E  C  +  +  +
+  +  +  +  +  +
+  +  +  +  +  +
+  +  +  +  +  +

BOX 13:
+  +  +  +  +  +
+  +  +  -  -  -
-  -  -  -  -  -
-  -  -  -  -  -
-  -  -  -  -  -

BOX 14:
-  -  -  -  -  -
-  -  -  -  -  -
-  -  -  -  -  -
-  -  -  -  -  -
-  -  - (H) W  -

-: Empty slot
A: ARM bootstrap (Absol)
E: Exit code bootstrap (Abra)
C: Crafting table (bad egg)
+: Area of the crafting table
H: HeXecutor (only when you want to use it)
W: Hexadecimal writer (bad egg)
```

You can freely store unused components in the crafting table area (preferably not at the beginning because that's where the hexadecimal writer will write).

## The ACE trigger bad egg

This purpose of this section is to create a bad egg that, when executed with the freezer, allows to trigger ACE for anywhere just by pressing L+R.

**WARNING: This is NOT compatible with the (deprecated) Hex Editor + Save Hack.
Please disable your Hex Editor before following this section. An updated setup for the Hex Editor will be coming.**

Before following this section, please ensure you have extended your freezer with the [Registry-Saver Metapod](freezer.md).

This bad egg can be created with 2 codes using the hexadecimal writer. As usual, do not look at the box 12 between the execution of the first code and the execution of the second one, or it will corrupt the data you are writing.

```
CODE 1:

Box  1: 3C 90 9F E5
Box  2: B0 A0 D9 E1
Box  3: 03 AC 0A E2
Box  4: 03 0C 5A E3
Box  5: 00 00 00 FF
Box  6: 04 F0 8F 02
Box  7: 00 80 A0 E3
Box  8: 28 80 8F E5
Box  9: 24 80 9F E5
Box 10: 01 80 88 E2
Boxes 11-14: 00 00 00 00

CODE 2:

Box  1: 1C 80 8F E5
Box  2: 14 90 9F E5
Box  3: 20 00 58 E3
Box  4: 19 FF 2F A1
Box  5: 02 00 58 E3
Box  6: 19 FF 2F 01
Box  7: 1E FF 2F E1
Box  8: EC 22 00 03
Box  9: FE FE 06 02
Box 10: 00 00 00 00
Boxes 11-14: 00 00 00 00
```

It should create a bad egg. Move the freezer, the metapod extension and this bad egg as follows (their exact location is not important but it must be after the exit code bootstrap):

```
BOX 14:
F  M  T  -  -  -
-  -  -  -  -  -
-  -  -  -  -  -
-  -  -  -  -  -
-  -  - (H)(W) -

-: Empty slot
F: Freezer (bad egg)
M: Registry-saver extension (Metapod)
T: ACE-trigger (bad egg)
```

Ensure that your exit code bootstrap is marked (the freezer must be executed with the pokedex completion diploma exit code in order to ensure that it will be executed only once).

Trigger ACE by looking at the summary of your stable ACE species (it shouldn't crash).
Now, the ACE-trigger should be active. You can test it by pressing L+R: it should trigger ACE and thus open the pokedex completion diploma again. As the Freezer is currently active in your ACE setup, it will have as effect to execute it again and this it will disable the ACE-trigger.

If this worked, well done! You can now enable the ACE trigger again (by manually triggering ACE with your stable ACE species), and then you can freely remove the freezer (and the two elements next to it) and execute the ACE you want by pressing L+R :)

*NOTE: Pressing L+R succintly will only trigger ACE once. If you press it more than 30 frames, it will start triggering ACE on each frame until you release L+R.*

When you want to disable the ACE-trigger, you can just move the freezer back in its position and trigger ACE, or alternatively you can save and reset.

## Example: walk-through-walls

This section is an example of application of the ACE-trigger.

If you have created the [walk-through-walls bad eggs](walk-through-walls.md), you can use it with this setup.
Usually the walk-through-walls bad eggs must be used with the freezer in order to be executed at each frame. However, now that we can trigger ACE at any time just by pressing L+R, we can easily execute it at each frame just by maintaining L+R. Thus, the freezer bad egg is not needed anymore to walk through walls.

Instead, you can directly put the two walk-through-walls bad eggs somewhere in your box 14. Or you could, if there wasn't a subtelty: the walk-through-walls bad eggs were designed to work with the PC register aligned. Thus, if we directly execute them through ACE, it will not work because they will be executed with the PC register misaligned.

In order to realign the PC register just before the execution of the walk-through-walls bad eggs, you can generate this Machop with the hexadecimal writer:

```
Box  1: 06 F0 4F E2
Box  2: 44 F0 8F E2
Box  3: 00 00 00 00
Box  4: 00 00 00 00
Box  5: 00 00 00 02
Box  6: 00 00 00 00
Box  7: 00 00 00 00
Box  8: 18 0C 00 00
Boxes 9-14: 00 00 00 00
```

Move the generated Machop just before the two walk-through-walls bad egg, somewhere in BOX 14. Now, when you will maintain L+R pressed, you will be able to walk through walls (don't forget to unmark your exit code bootstrap or it will open the pokedex completion diploma each time).

*NOTE: When you use the walk-through-walls bad eggs this way, a bad egg will be created next to them. It is just some data that the walk-through-walls bad eggs store there. You can freely remove it when you want (or you can leave it there and consider that your walk-through-walls setup is now composed of 3 bad eggs).*

## Persistence (optional)

Soon.
