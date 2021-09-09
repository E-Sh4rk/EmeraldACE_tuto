# Walk through walls

This script will allow you to walk through walls (however it does not allow you to
leave the bounds of the map). In order to enable it, it must be executed each frame by using the *freezer bad egg*.

## Prerequisite

- An ACE glitch species (for instance 0x40E9 for the english version)
- If you use a glitch species that executes Thumb code such as 0x40E9, you will also need a Thumb->ARM bootstrap
- A [certificate exit code bootstrap](exit-code.md) (you can place it in the first slot of BOX 14 for instance). Note that it does not matter if you have renamed your BOX 14 as the creation of this bad egg uses the hexadecimal-writer bad egg
- The [hexadecimal-writer and crafting table bad eggs](hex-writer.md)
- The [freezer bad egg](freezer.md)

## Let's go

We will use the hexadecimal-writer bad egg in order to write the script in the PC storage.
You should ensure that you have the hexadecimal-writer bad egg in the last slot of BOX 14 (with the exit code bootstrap at least 2 slots before), and that your freezer bad egg will not be executed instead of the hexadecimal-writer (in order for it to not be executed, you can put it either somewhere in the crafting table area or before the last row of BOX 11). Also ensure that there are at least 3 empty slots at the beginning of the crafting table area, and run these 3 codes (you can freely save and view the crafting table area during the process):

```
=============== CODE 1 ===============

Box  1: 001F2DE9
Box  2: 88A09FE5
Box  3: B2C1DAE1
Box  4: BCB8DFE1
Box  5: 000000FF
Box  6: B4C8CFE1
Box  7: 0B005CE1
Box  8: 80A09F05
Box  9: B0B8DF01
Box 10: B0B0CA01
Box 11: 68A09FE5
Box 12: 00B09AE5
Box 13: 64C09FE5
Box 14: B081DCE1

=============== CODE 2 ===============

Box  1: B291DCE1
Box  2: 18C0DCE5
Box  3: 11005CE3
Box  4: 01908902
Box  5: 33005CE3
Box  6: 01804802
Box  7: 22005CE3
Box  8: 01904902
Box  9: 44005CE3
Box 10: 01808802
Box 11: 000000FF
Box 12: 08A09AE5
Box 13: 88A08AE0
Box 14: 00000000

=============== CODE 3 ===============

Box  1: 990B09E0
Box  2: 89A08AE0
Box  3: 28A08FE5
Box  4: B0B0DAE1
Box  5: B4B2CFE1
Box  6: 03CBE0E3
Box  7: 0CB00BE0
Box  8: B0B0CAE1
Box  9: 001FBDE8
Box 10: 10FF2FE1
Box 11: 18730302
Box 12: C05D0003
Box 13: 50730302
Box 14: 00000000
```

After that, there should be 2 bad eggs at the beginning of your crafting table area.

Now, move the freezer bad egg in the BOX 14 slot 3 (or anywhere at least 2 slots after the exit code bootstrap) and move these two bad eggs just after (**don't change their order**).

Execute the ACE... and the walk-through-walls mode should be active. Just execute the ACE again to disable it.
