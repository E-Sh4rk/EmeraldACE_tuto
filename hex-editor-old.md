**WARNING: This tutorial is deprecated. A new version compatible with the new ACE setup is available [here](hex-editor.md).**

**The bad eggs created in this tutorial should not be marked or moved in your party: it could corrupt them.**

# Hexadecimal editor

In this tutorial, we will implement an hexadecimal editor inside the box storage. We will then implement a launcher that will make the hex editor start by pressing L+R. This hack will be persistent (it will stay after a save/reset), but you will be able to enable/disable it when you want.

**Credits:** This tutorial is an adapation of [this article on Hatena Blog](https://bzl.hatenablog.com/entry/2019/09/29/182642). Credits for the implementation of the hexadecimal editor goes to the author of this article. For my part, I analyzed and brought some minor changes to the implementation so that it can work within the English version.

## Prerequisite

- A stable ACE glitch species such as [0x40E9](stable-ace.md) (with its Thumb->ARM bootstrap)
- A [certificate exit code bootstrap](exit-code.md) (you can place it in the first slot of BOX 14 for instance). Note that it does not matter if you have renamed your BOX 14 as the creation of this bad egg uses the hexadecimal-writer bad egg
- The [hexadecimal-writer and crafting table bad eggs](hex-writer.md)

## Implementation of the hex editor

NOTE: the codes given here are for the english version. I have not written the codes for the other versions yet.

In order to implement the hexadecimal editor, you have to execute 24 codes with the hex-writer (together with the crafting table). It will create a total of 12 bad eggs. In order to avoid propagating mistakes, we recommend executing the codes by batches of 6: it should create 3 bad eggs that you should then move into their final position before continuing with the next batch.

Here is how you have to position the different elements in your boxes:

```
BOX 12:
-  -  -  -  -  -
A  -  C  +  +  +
+  +  +  +  +  +
+  +  +  +  +  +
H  H  H  H  H  H

BOX 13:
H  H  H  H  H  H
+  +  +  -  -  -
-  -  -  -  -  -
-  -  -  -  -  -
-  -  -  -  -  -

BOX 14:
E  -  -  -  -  -
-  -  -  -  -  -
-  -  -  -  -  -
-  -  -  -  -  -
-  -  -  -  W  -

-: Empty slot
A: Thumb->ARM bootstrap (if any)
C: Crafting table bad egg
+: Area of the crafting table
H: Hexadecimal editor bad eggs
E: Exit code bootstrap
W: Hexadecimal writer bad egg
```

The content of your box 14 can be different, but your crafting table and hexadecimal editor bad eggs must be in
the position specified. The order of the hexadecimal editor bad eggs is the order in which they will be created. Do not change their relative order or it will be a nightmare to fix it!

**Do not look at BOX 12** during this process except at the end of a batch. We recommend batches of 6 codes (= 3 bad eggs), but you can actually do batches of any even number if you prefer.

NOTE: spaces have been added only for readability purposes. Box names must not contain any space. Boxes 11-14 have been omitted: their name should be `00000000` during the whole process.

```
=============== CODE 1 ===============

Box 1:  80 B5 70 B4
Box 2:  DA 48 D3 4C
Box 3:  7F 46 05 37
Box 4:  BE 46 79 E0
Box 5:  00 E0 AA AA
Box 6:  05 1C D0 4C
Box 7:  7F 46 05 37
Box 8:  BE 46 71 E0
Box 9:  00 20 CF 4C
Box 10: 00 E0 AA AA

=============== CODE 2 ===============

Box 1:  7F 46 05 37
Box 2:  BE 46 69 E0
Box 3:  00 E0 AA AA
Box 4:  08 21 CF 48
Box 5:  CA 4C 7F 46
Box 6:  00 E0 AA AA
Box 7:  09 37 BE 46
Box 8:  5E E0 C9 49
Box 9:  00 E0 AA AA
Box 10: 0D 72 CD 48

=============== CODE 3 ===============

Box 1:  08 60 00 78
Box 2:  08 71 00 20
Box 3:  49 71 70 BC
Box 4:  80 BD CA 48
Box 5:  00 E0 AA AA
Box 6:  10 21 09 02
Box 7:  40 18 00 22
Box 8:  C7 49 01 80
Box 9:  01 31 01 23
Box 10: 00 E0 AA AA

=============== CODE 4 ===============

Box 1:  01 23 01 23
Box 2:  01 23 01 23
Box 3:  00 E0 AA AA
Box 4:  01 23 01 23
Box 5:  01 23 02 30
Box 6:  00 E0 AA AA
Box 7:  01 80 01 32
Box 8:  0E 2A EC D1
Box 9:  00 E0 AA AA
Box 10: 01 31 01 80

=============== CODE 5 ===============

Box 1:  01 31 BB 48
Box 2:  40 23 10 22
Box 3:  12 02 80 18
Box 4:  01 80 C1 52
Box 5:  00 E0 AA AA
Box 6:  02 31 1C 30
Box 7:  01 80 C1 52
Box 8:  01 31 B6 48
Box 9:  10 22 12 02
Box 10: 00 E0 AA AA

=============== CODE 6 ===============

Box 1:  80 18 01 80
Box 2:  01 31 00 22
Box 3:  00 E0 AA AA
Box 4:  01 23 01 23
Box 5:  01 23 01 23
Box 6:  00 E0 AA AA
Box 7:  01 23 01 23
Box 8:  01 23 01 23
Box 9:  00 E0 AA AA
Box 10: 01 23 01 23

=============== CODE 7 ===============

Box 1:  02 30 01 80
Box 2:  01 32 0E 2A
Box 3:  EC D1 01 31
Box 4:  01 80 70 47
Box 5:  00 E0 AA AA
Box 6:  A7 46 C0 46
Box 7:  80 B5 70 B4
Box 8:  84 B0 97 4D
Box 9:  28 7A 11 21
Box 10: 00 E0 AA AA

=============== CODE 8 ===============

Box 1:  A0 4C 7F 46
Box 2:  09 37 BE 46
Box 3:  00 E0 AA AA
Box 4:  7D E0 00 24
Box 5:  2E 1C 28 78
Box 6:  00 E0 AA AA
Box 7:  01 09 09 29
Box 8:  02 D9 10 31
Box 9:  00 E0 AA AA
Box 10: A1 31 31 74

=============== CODE 9 ===============

Box 1:  0F 21 01 40
Box 2:  09 29 00 D9
Box 3:  10 31 A1 31
Box 4:  71 74 01 35
Box 5:  00 E0 AA AA
Box 6:  02 36 01 34
Box 7:  05 2C 05 D0
Box 8:  04 2C E4 D1
Box 9:  01 36 E2 E7
Box 10: 00 E0 AA AA

=============== CODE 10 ===============

Box 1:  80 4D 2E 1C
Box 2:  32 1C 10 8A
Box 3:  00 E0 AA AA
Box 4:  D1 8A D0 82
Box 5:  11 82 50 8A
Box 6:  00 E0 AA AA
Box 7:  91 8A 90 82
Box 8:  51 82 00 20
Box 9:  00 E0 AA AA
Box 10: 30 62 70 62

=============== CODE 11 ===============

Box 1:  B0 62 70 79
Box 2:  04 28 07 D0
Box 3:  40 00 10 30
Box 4:  31 5A 10 30
Box 5:  00 E0 AA AA
Box 6:  31 52 07 E0
Box 7:  70 7E 29 21
Box 8:  70 54 B0 7E
Box 9:  2A 21 70 54
Box 10: 00 E0 AA AA

=============== CODE 12 ===============

Box 1:  80 48 F0 60
Box 2:  F0 61 F0 62
Box 3:  00 E0 AA AA
Box 4:  0E 36 02 96
Box 5:  00 20 01 90
Box 6:  00 E0 AA AA
Box 7:  69 48 00 90
Box 8:  28 7A 00 21
Box 9:  00 E0 AA AA
Box 10: 00 22 00 23

=============== CODE 13 ===============

Box 1:  70 4C 00 00
Box 2:  7F 46 05 37
Box 3:  BE 46 1A E0
Box 4:  10 36 02 96
Box 5:  00 E0 AA AA
Box 6:  00 20 01 90
Box 7:  60 48 00 90
Box 8:  28 7A 00 21
Box 9:  00 22 00 23
Box 10: 00 E0 AA AA

=============== CODE 14 ===============

Box 1:  66 4C 00 00
Box 2:  7F 46 09 37
Box 3:  00 E0 AA AA
Box 4:  BE 46 04 E0
Box 5:  04 B0 70 BC
Box 6:  00 E0 AA AA
Box 7:  80 BD A7 46
Box 8:  80 B5 70 B4
Box 9:  00 E0 AA AA
Box 10: 07 1C 78 46

=============== CODE 15 ===============

Box 1:  05 30 86 46
Box 2:  13 E7 4D 4D
Box 3:  5B 4E 36 88
Box 4:  10 20 30 40
Box 5:  00 E0 AA AA
Box 6:  05 D0 68 79
Box 7:  04 28 74 D0
Box 8:  01 30 68 71
Box 9:  6B E0 20 20
Box 10: 00 E0 AA AA

=============== CODE 16 ===============

Box 1:  30 40 09 D0
Box 2:  68 79 00 28
Box 3:  00 E0 AA AA
Box 4:  67 D0 01 38
Box 5:  68 71 5E E0
Box 6:  00 E0 AA AA
Box 7:  40 20 30 40
Box 8:  12 D0 68 79
Box 9:  00 E0 AA AA
Box 10: 04 28 02 D0

=============== CODE 17 ===============

Box 1:  C0 43 03 21
Box 2:  08 40 29 5C
Box 3:  01 31 29 54
Box 4:  04 28 4C D0
Box 5:  00 E0 AA AA
Box 6:  28 68 00 78
Box 7:  28 71 46 E0
Box 8:  80 20 30 40
Box 9:  0F D0 68 79
Box 10: 00 E0 AA AA

=============== CODE 18 ===============

Box 1:  04 28 04 D0
Box 2:  C0 43 03 21
Box 3:  00 E0 AA AA
Box 4:  08 40 29 5C
Box 5:  01 39 00 39
Box 6:  00 E0 AA AA
Box 7:  E3 E7 68 79
Box 8:  04 28 14 D1
Box 9:  00 E0 AA AA
Box 10: 10 20 00 01

=============== CODE 19 ===============

Box 1:  30 40 03 D0
Box 2:  29 79 10 31
Box 3:  29 71 26 E0
Box 4:  20 20 00 01
Box 5:  00 E0 AA AA
Box 6:  30 40 04 D0
Box 7:  04 20 29 79
Box 8:  10 39 29 71
Box 9:  1B E0 01 20
Box 10: 00 E0 AA AA

=============== CODE 20 ===============

Box 1:  30 40 05 D0
Box 2:  28 68 29 79
Box 3:  00 E0 AA AA
Box 4:  01 70 10 E0
Box 5:  02 20 30 40
Box 6:  00 E0 AA AA
Box 7:  11 D0 38 1C
Box 8:  26 4C 7F 46
Box 9:  00 E0 AA AA
Box 10: 09 37 BE 46

=============== CODE 21 ===============

Box 1:  7F E7 24 48
Box 2:  00 21 01 70
Box 3:  05 E0 7F 46
Box 4:  09 37 BE 46
Box 5:  00 E0 AA AA
Box 6:  E8 E6 70 BC
Box 7:  80 BD C0 46
Box 8:  00 09 09 0E
Box 9:  02 0F 8F 00
Box 10: 00 E0 AA AA

=============== CODE 22 ===============

Box 1:  00 02 03 00
Box 2:  00 04 05 00
Box 3:  00 E0 AA AA
Box 4:  80 33 00 08
Box 5:  8C 37 00 08
Box 6:  00 E0 AA AA
Box 7:  6C 23 00 08
Box 8:  B0 8F 0A 08
Box 9:  00 E0 AA AA
Box 10: 00 D6 03 02

=============== CODE 23 ===============

Box 1:  5C D3 03 02
Box 2:  45 D2 03 02
Box 3:  68 D3 03 02
Box 4:  6C D3 03 02
Box 5:  00 E0 AA AA
Box 6:  00 00 00 02
Box 7:  10 EA 00 06
Box 8:  14 E2 00 00
Box 9:  50 EA 00 06
Box 10: 00 E0 AA AA

=============== CODE 24 ===============

Box 1:  D0 EA 00 06
Box 2:  48 3C 00 08
Box 3:  00 E0 AA AA
Box 4:  64 9E 19 08
Box 5:  F0 22 00 03
Box 6:  00 E0 AA AA
Box 7:  9C 90 0A 08
Box 8:  2C 0F 00 03
Box 9:  00 E0 AA AA
Box 10: FF 00 FC 15
```

## Implementation of the launcher

Now, we have to implement the launcher that will allow us to execute the hex editor by pressing L+R.

It requires the creation of 4 bad eggs (8 codes). We will put it just above the hex-editor bad eggs:

```
BOX 12:
-  -  -  -  -  -
A  -  C  +  +  +
+  +  +  +  +  +
L  L  L  L  +  +
H  H  H  H  H  H

BOX 13:
H  H  H  H  H  H
+  +  +  -  -  -
-  -  -  -  -  -
-  -  -  -  -  -
-  -  -  -  -  -

-: Empty slot
A: Thumb->ARM bootstrap (if any)
C: Crafting table bad egg
+: Area of the crafting table
L: Launcher bad eggs
H: Hexadecimal editor bad eggs
```

The procedure is the same as for the implementation of the hex editor. As there are 8 codes this time, we recommend you to proceed by batches of 4 codes.

```
=============== CODE 1 ===============

Box 1:  F0 B4 04 1C
Box 2:  29 48 01 38
Box 3:  01 78 00 29
Box 4:  47 D1 01 21
Box 5:  00 E0 AA AA
Box 6:  01 70 41 1C
Box 7:  26 4A 26 A0
Box 8:  10 44 20 31
Box 9:  78 22 92 00
Box 10: 00 E0 AA AA

=============== CODE 2 ===============

Box 1:  0B DF 20 48
Box 2:  22 49 02 1C
Box 3:  00 E0 AA AA
Box 4:  21 32 89 23
Box 5:  9B 00 03 33
Box 6:  00 E0 AA AA
Box 7:  02 25 2E C0
Box 8:  1D 48 1E 49
Box 9:  00 E0 AA AA
Box 10: 1E 4A 1F 4B

=============== CODE 3 ===============

Box 1:  20 4D 21 4E
Box 2:  22 4F EE C0
Box 3:  22 49 24 4A
Box 4:  24 4B 25 4D
Box 5:  00 E0 AA AA
Box 6:  24 4E 25 4F
Box 7:  EE C0 26 49
Box 8:  26 4A 27 4B
Box 9:  27 4E F4 25
Box 10: 00 E0 AA AA

=============== CODE 4 ===============

Box 1:  AD 19 80 27
Box 2:  BF 00 01 37
Box 3:  00 E0 AA AA
Box 4:  EE C0 09 49
Box 5:  03 31 23 4A
Box 6:  00 E0 AA AA
Box 7:  22 4B 0E C0
Box 8:  09 48 23 49
Box 9:  00 E0 AA AA
Box 10: 08 60 F0 BC

=============== CODE 5 ===============

Box 1:  20 1C 01 49
Box 2:  08 47 00 00
Box 3:  99 A9 08 08
Box 4:  00 D0 03 02
Box 5:  00 E0 AA AA
Box 6:  2C 01 00 00
Box 7:  28 30 00 23
Box 8:  00 E0 03 02
Box 9:  0F 00 A0 E1
Box 10: 00 E0 AA AA

=============== CODE 6 ===============

Box 1:  05 00 80 E2
Box 2:  10 FF 2F E1
Box 3:  00 E0 AA AA
Box 4:  0A 48 40 78
Box 5:  03 21 88 42
Box 6:  00 E0 AA AA
Box 7:  0B D1 09 4B
Box 8:  1B 78 01 2B
Box 9:  00 E0 AA AA
Box 10: 07 D0 08 4B

=============== CODE 7 ===============

Box 1:  00 20 18 60
Box 2:  D8 60 07 48
Box 3:  98 60 07 48
Box 4:  18 61 07 48
Box 5:  00 E0 AA AA
Box 6:  6E 21 81 71
Box 7:  06 4B 18 47
Box 8:  EC 22 00 03
Box 9:  38 0E 00 03
Box 10: 00 E0 AA AA

=============== CODE 8 ===============

Box 1:  50 73 03 02
Box 2:  50 27 00 03
Box 3:  00 E0 AA AA
Box 4:  FC 7F 00 03
Box 5:  00 00 00 00
Box 6:  00 00 00 00
Box 7:  00 00 00 00
Box 8:  00 00 00 00
Box 9:  00 00 00 00
Box 10: 00 00 00 00
```

## Enabling/Disabling it

You're almost there! Now that we have the hex editor and the launcher, we just need a way to activate it. For that, let's invoke the power of Mewtwo.

You can invoke Mewtwo with the crafting table, as usual:

```
Box  1: 1A C0 9F E5
Box  2: 00 B0 A0 E3
Box  3: 01 B0 4C E5
Box  4: 0A C0 9F E5
Box  5: 6E B0 8B E2
Box  6: 06 B0 CC E5
Box  7: 1E FF 2F E1
Box  8: D2 DB 00 00
Box  9: 50 73 03 02
Box 10: 00 D0 03 02
Box 11: 00 00 00 00
Box 12: 8C 70 00 00
Boxes 13-14: 00 00 00 00
```

Mewtwo should have appeared in your crafting table.
Now, let's invoke Mew in order to calm him (move Mewtwo in the next slot of the crafting table, otherwise the data of Mew will be appended to the data of Mewtwo).

```
Box  1: 1A C0 9F E5
Box  2: 12 B0 9F E5
Box  3: 00 C0 8B E5
Box  4: 12 B0 9F E5
Box  5: 45 C0 4C E2
Box  6: 06 C0 CB E5
Box  7: 1E FF 2F E1
Box  8: 7E F3 00 00
Box  9: FC 7F 00 03 
Box 10: 50 27 00 03 
Box 11: 50 73 03 02
Box 12: 9F 70 00 00
Boxes 13-14: 00 00 00 00
```

Perfect! Mewtwo will be used to activate the launcher (when the launcher is active, you can open
the hexadecimal editor just by pressing L+R). In the other hand, Mew has the power to disable it.

We recommend you to put your Mew and Mewtwo in this location:

```
BOX 13:
H  H  H  H  H  H
+  M  M  S  -  -
-  -  -  -  -  -
-  -  -  -  -  -
-  -  -  -  -  -

-: Empty slot
+: Area of the crafting table
H: Hexadecimal editor bad eggs
M: Mewtwo/Mew
S: Summon spot (see explanation below)
```

Before I explain how to activate the launcher, you should save your game. **DO NOT SAVE YOUR GAME AFTER HAVING ACTIVATED THE LAUNCHER** (we must do some tests before).

When you want to activate the launcher, just move Mewtwo in the *Summon Spot* and trigger ACE. It will not open the Pokedex completion diploma, you have to exit the summary screen yourself quickly. You can then move Mewtwo back in its original place. Same thing with Mew when you want to deactivate it.

Before being allowed to save, you should activate the launcher and test the following things:
- Press L+R while in the overworld. It should open the hex editor and you shouldn't be able to move your character.
- Press B. It should close the hex editor (though the window does not disappear immediately due to a refreshing issue) and you should be able to move your character.
- Open and close your pokedex, inventory, bag, etc. It shouldn't crash.
- Fly in another city, enter in some houses, etc. It shouldn't crash.
- Enter in a Pokemon Center, open your PC, move Mew in the Summon Spot.
- Trigger ACE in order to disable the launcher. Pressing L+R should not open the hex editor anymore.

These tests are here to ensure that you will not be softlocked (as the launcher stays active after a save/reset). If all the tests succeeded, then well done, you succeed! You can now save your game even with the launcher active.
If some tests failed, you should refer to the appendix.

**IMPORTANT:** When the launcher is active, the following row of your crafting table area should be left empty:

```
BOX 12:
-  -  -  -  -  -
A  -  C  +  +  +
x  x  x  x  x  x
L  L  L  L  +  +
H  H  H  H  H  H

-: Empty slot
A: Thumb->ARM bootstrap (if any)
C: Crafting table bad egg
+: Area of the crafting table
x: SLOTS THE MUST REMAIN EMPTY
L: Launcher bad eggs
H: Hexadecimal editor bad eggs
```

Indeed, when the launcher is active, this row becomes the entry point of a glitched object action associated with your character. It means that each time your character is refreshed (when closing the Pokedex, when entering in a building, etc), the content of this row is executed (we want it to be empty so that the first thing to be executed is the launcher).

**How to use it:**
- Press L+R to open the hex editor
- The 4 first bytes represent the address, the last one the value
- Choose the desired address, and then you can modify the value and press A to confirm the modification
- L and R can be used to change the value by 0x10
- Press B to exit the hexadecimal editor

## Appendix: in case of failure

In order to check that the data in your bad eggs is correct, we will use a special bad egg that computes a checksum of the 6 following slots and store it in the attack and defense stats of the second pokemon in your team. Before going further, don't forget to deactivate the launcher (or reload your save)!

First, generate the following bad egg with your hex-writer:

```
Box  1: 46808FE2
Box  2: 1E9E88E2
Box  3: 00C0A0E3
Box  4: 04B098E4
Box  5: 000000FF
Box  6: 0BC08CE0
Box  7: 090058E1
Box  8: 18F04F32
Box  9: 0AB09FE5
Box 10: BAC5CBE1
Box 11: 2CC8A0E1
Box 12: BCC5CBE1
Box 13: 10FF2FE1
Box 14: 50450202
```

Now, move your exit code bootstrap and the bad egg just created in the following positions:

```
BOX 13:
H  H  H  H  H  H
+  M  M  S  -  -
E  -  -  -  -  C
x  x  x  x  x  x
-  -  -  -  -  -

-: Empty slot
+: Area of the crafting table
H: Hexadecimal editor bad eggs
M: Mewtwo/Mew
S: Summon spot (see explanation below)
E: Exit code bootstrap
C: Checksum bad egg
x: Position where you will put the bad eggs to check
```

Leave the `x` slots empty for now and trigger ACE. The second pokemon of your party should
now have an attack and defense of 0 (it does not work if the second pokemon of your party is deoxys).

If it is the case, then we can proceed to the verification of your bad eggs.
You will have to move one of the groups of bad eggs indicated below in the row with the `x` slots
(from left to right). Then, just trigger ACE and compare the value of attack and defense stats with the ones given.
Then, move your group of bad eggs back into their original position and proceed to the test of the next group.

```
Group             Attack  Defense
Launcher 1-2      4269    14203
Launcher 3-4      27183   14177

Hex editor 1-3    59215   52963
Hex editor 4-6    14453   33968
Hex editor 7-9    43544   3083
Hex editor 10-12  53719   10227
```

NOTE: The checksum does not take the order into account, so take care not to change the relative order of the bad eggs otherwise it will be difficult to notice and to find the right order again!

If you have different values for some groups, then you should throw away the corresponding bad eggs and create them again.
