**The bad eggs and Pokemons created in this tutorial should not be marked (unless specified otherwise) or moved in your party: it could corrupt them.**

# New ACE environment 

In this tutorial, we will update your bootstraps (thanks to the hexadecimal writer) so that they become more stable and convenient.
Then, we will create a bad egg (to use with the freezer) that will allow you to trigger ACE just by pressing R.

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

*NOTE: you can freely mark/unmark it in order to switch between the two exit codes. However, DO NOT mark/unmark any other element of your ACE setup (unless specified otherwise) or it will be corrupted.*

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
+  +  +  B  -  -
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
B: CPSR status reset (Bulbasaur)
H: HeXecutor (only when you want to use it)
W: Hexadecimal writer (bad egg)
```

You can freely store unused components in the crafting table area (preferably not at the beginning because that's where the hexadecimal writer will write).

*Optional:*

As we are in the mood, let's create another bootstrap: a Thumb<->ARM switch
that allows to switch the execution mode of the processor between ARM and Thumb.
This bootstrap is different than the ARM bootstrap we made above: it requires the processor to be in ARM mode, and then allows to switch to Thumb mode (if the bootstrap is marked) or to stay in ARM mode but with the PC register aligned (if the bootstrap is unmarked).

```
Box  1: 00 00 00 FF
Box  2: 06 F0 4F E2
Box  3: 0B B0 DF E5
Box  4: 00 00 5B E3
Box  5: 38 B0 8F E2
Box  6: 08 F0 8F E2
Box  7: 00 00 00 00
Box  8: D6 F0 00 00
Box  9: 44 F0 00 00
Box 10: 01 B0 8B 12
Box 11: 1B FF 2F E1
Boxes 12-14: 00 00 00 00
```

This should create a Machop. You can store it somewhere (we do not need it now). We recommend you to make a second instance of this Machop (just execute the code again), because you might need two such switches in the future.

## The ACE trigger bad egg

This purpose of this section is to create a bad egg that, when executed with the freezer, allows to trigger ACE for anywhere just by pressing R.

**WARNING: This is NOT compatible with the old version of the *memory editor + save hack*.
Please disable your save hack before following this section: you will then be able to [update your memory editor launcher](hex-editor.md) so that it works with this new setup.**

Before following this section, please ensure you have extended your freezer with the [Registry-Saver Metapod](freezer.md).

This bad egg can be created with 2 codes using the hexadecimal writer. As usual, do not look at the box 12 between the execution of the first code and the execution of the second one, or it will corrupt the data you are writing.

```
CODE 1:

Box  1: 3C 90 9F E5
Box  2: B0 A0 D9 E1
Box  3: 01 AC 0A E2
Box  4: 01 0C 5A E3
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
Now, the ACE-trigger should be active. You can test it by pressing R: it should trigger ACE and thus open the pokedex completion diploma again. As the Freezer is currently active in your ACE setup, it will have as effect to execute it again and this it will disable the ACE-trigger.

If this worked, well done! You can now enable the ACE trigger again (by manually triggering ACE with your stable ACE species), and then you can freely remove the freezer (and the two elements next to it) and execute the ACE you want by pressing R :)

*NOTE: Pressing R succintly will only trigger ACE once. If you press it more than 30 frames, it will start triggering ACE on each frame until you release R.*

When you want to disable the ACE-trigger, you can just move the freezer back in its position and trigger ACE, or alternatively you can save and reset.

## Example: walk-through-walls

This section is an example of application of the ACE-trigger.

If you have created the [walk-through-walls bad eggs](walk-through-walls.md), you can use it with this setup.
Usually the walk-through-walls bad eggs must be used with the freezer in order to be executed at each frame. However, now that we can trigger ACE at any time just by pressing R, we can easily execute it at each frame just by maintaining R. Thus, the freezer bad egg is not needed anymore to walk through walls.

Instead, you can directly put the two walk-through-walls bad eggs somewhere in your box 14. Or you could, if there wasn't a subtelty: the walk-through-walls bad eggs were designed to work with the PC register aligned. Thus, if we directly execute them through ACE, it will not work because they will be executed with the PC register misaligned.

In order to realign the PC register just before the execution of the walk-through-walls bad eggs, we can use the Machop we generated earlier (the Thumb<->ARM switch).

Move the Machop just before the two walk-through-walls bad egg, somewhere in BOX 14.
Ensure that the Machop is unmarked: we do not want to switch to Thumb mode, but to stay in ARM mode and realign the PC register. Now, when you will maintain R pressed, you will be able to walk through walls (don't forget to unmark your exit code bootstrap or it will open the pokedex completion diploma each time).

*NOTE: When you use the walk-through-walls bad eggs this way, a bad egg will be created next to them. It is just some data that the walk-through-walls bad eggs store there. You can freely remove it when you want (or you can leave it there and consider that your walk-through-walls setup is now composed of 3 bad eggs).*

## Persistence (optional)

In this section, we'll learn how to make the ACE trigger persistent to a save/reset.

*NOTE: actually it can also be used to make other codes persistent, such as the walk-through-wall code for instance, but making the ACE trigger persistent seems more convenient as it then allows to trigger any other ACE code).*

Before starting, you have to understand how this works. We will modify the save so that the object event associated with the main character is glitched. When the game will load your character (i.e. when the save loads), it will execute the callback associated with this glitched object event. This callback leads to somewhere in the box data, a little after the glitched sprite animation callback used by ACE:

```
BOX 12:
\\\\\\\\\\\\\\\\
A  E  C  +  +  +
////////////////
+  +  +  +  +  +
+  +  +  +  +  +

-: Empty slot
A: ARM bootstrap (Absol)
E: Exit code bootstrap (Abra)
C: Crafting table (bad egg)
+: Area of the crafting table
\\\\: Approximate entry area for sprite animation ACE (and ACE-trigger)
////: Approximate entry area for glitched object event callback
```

It means that, when your save will load, it will execute the code located just after
the third row of the box 12. In the other hand, when you trigger standard ACE, it executes the code located just after the first row (the two bootstraps and the crafting table that makes it jump to the end of the crafting table area). Consequently, the code that you put in the crafting table area, below the third row, will be executed when your save load but not when you trigger ACE.

That's why the code responsible for loading the ACE trigger bad egg will be located in the crafting table area (we only want it to be executed once when the save loads).

You have to be careful:
- **DO NOT PUT ANY DATA (POKEMON OR EGG) IN THE /////// AREA**: when your save loads, it will jump to somewhere randomly in this area (due to ASLR), thus you shouldn't put any data or code here as it might get partially executed.
- Before enabling the persistence, you must ensure that the code you put in the crafting table area does not make the game crash, otherwise it will crash every time you try to load your save (and every time you make a change in this area, you must test it before saving).

Okay, now let's start. We just need two new extensions for the freezer: the main purpose of these two extensions is to keep the main character object event glitched.

You can create them using the hexadecimal writer:

```
Box  1: 1A B0 9F E5
Box  2: 0B C0 A0 E3
Box  3: 00 C0 CB E5
Box  4: 02 10 9F E5
Box  5: 0E 00 8F E2
Box  6: 34 F0 8F E2
Box  7: 99 A9 08 08
Box  8: 8F 8E 00 00
Box  9: 98 70 00 00
Box 10: 56 73 03 02
Box 11: 04 00 A0 E1
Box 12: 11 FF 2F E1
Boxes 13-14: 00 00 00 00

```

It will create a Porygon. Store it somewhere (in another slot of the crafting table area or before the last row of BOX 11).

```
Box  1: 28 10 9F E5
Box  2: 0C 10 91 E5
Box  3: 00 00 51 E3
Box  4: 0B 10 A0 E3
Box  5: 63 10 81 12
Box  6: 10 20 9F E5
Box  7: 04 F0 8F E2
Box  8: 3B 66 00 00
Box  9: CD 00 00 00
Box 10: 00 10 C2 E5
Box 11: 20 F0 8F E2
Box 12: 56 73 03 02
Box 13: C0 22 00 03
Box 14: 00 00 00 00
```

It will create a Porygon 2.
You should also have a second copy of the ARM bootstrap and the exit code bootstrap (cf. section *Updating your bootstraps*).

Dispose everything like that:

```
BOX 12:
-  -  -  -  -  -
A  E  C  +  +  +
x  x  x  x  x  x
A  P  E  F  M  Q
T  +  +  +  +  +

-: Empty slot
A: ARM bootstrap (Absol)
E: Exit code bootstrap (Abra)
C: Crafting table (bad egg)
+: Area of the crafting table
x: Never put anything here!
P: Porygon
F: Freezer (bad egg)
M: Registry-saver extension (Metapod)
Q: Porygon 2
T: ACE-trigger (bad egg)
```

Ensure your second exit code bootstrap (the one in the crafting table area) is marked.

Also, setup your BOX 14 so that triggering ACE will only open the pokedex completion diploma without doing anything else (for that you can either set up the hex writer with only `00000000` as box names, or you can set up the hexecutor with the command `10FF2FE1` in BOX 1 name).

At this point, save your game. Now we will ensure that everything's okay.

*Reminder: the data in the crafting table area, below the third row, will be executed automatically when your save loads. Thus we must be careful and ensure it is correct!*

1. Move the crafting table bad egg in the last slot of BOX 12, so that when you trigger ACE, it will not jump over the crafting table data (and thus it will execute it).
2. Trigger ACE. It should open the pokedex completion diploma. Now your ACE trigger (and the persistence) should be active.
3. Restore the crafting table bad egg in its original position.
4. Briefly press R: each time you press it, it should open the Pokedex completion diploma.
5. Enter/leave a building, open/close the Pokedex. It shouldn't crash.
6. Move the crafting table bad egg in the last slot of BOX 12 again.
7. Move the exit code bootstrap of the crafting table area one row down (it should be in the last row).
8. Briefly press R many times. It should not crash (and it should not open the diploma). Now your ACE trigger should be inactive.
9. Restore the crafting table bad egg and the exit code bootstrap back in their original positions.
10. Pressing R should not do anything. Enter or leave a building.

If there was no crash, you can proceed.

**In order to activate the persistence:**

Your BOX 12 should look like the scheme above.

1. Move the crafting table bad egg in the last slot of BOX 12.
2. Trigger ACE. It should open the pokedex completion diploma. Now your ACE trigger (and the persistence) should be active.
3. Restore the crafting table bad egg in its original position.
4. Your setup should look like the one above.
5. You can do some more tests by pressing R and ensuring there are no crashes, and then you can save.

Note that while the persistence is active, the pokedex completion diploma will open once each time you load your save.

**In order to disable the persistence:**

1. Do the exact same steps as for the activation.
2. Enter in a new map (you can enter or leave a building).
3. Test that your ACE trigger is disabled (pressing R shouldn't do anything), and then you can save.
