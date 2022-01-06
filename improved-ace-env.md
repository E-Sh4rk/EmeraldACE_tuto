**The bad eggs and Pokemons created in this tutorial should not be marked (unless specified otherwise) or moved in your party: it could corrupt them.**

# New ACE environment 

In this tutorial, we will update your bootstraps (thanks to the hexadecimal writer) so that they become more stable and convenient.
Then, we will create a bad egg (to use with the freezer) that will allow you to trigger ACE just by pressing L+R.

Finally, in the last (optional) part, we will add some more components to our ACE environment allowing the former bad egg to automatically be loaded when your save load.

## Prerequisite

- A stable ACE glitch species such as [0x40E9](stable-ace.md) (with its Thumb->ARM bootstrap)
- A [certificate exit code bootstrap](exit-code.md) (you can place it in the first slot of BOX 14 for instance). Note that it does not matter if you have renamed your BOX 14 as the creation of this bad egg uses the hexadecimal-writer bad egg
- The [hexadecimal-writer and crafting table bad eggs](hex-writer.md)
- The [freezer bad egg](freezer.md)

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

Soon.

## Persistence (optional)

Soon.
