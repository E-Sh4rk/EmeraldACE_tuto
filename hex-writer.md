# Hexadecimal-writer bad egg

The purpose of this tutorial is to create a special bad egg that allows easy writing of hexadecimal data in the PC storage.
When this bad egg is placed in the last slot of BOX 14, it changes the behavior of ACE codes:
instead of considering box names data as ARM binary code, it will interpret the box names text as hexadecimal and write
this hexadecimal data in the PC storage (by default, in the slot 29 of BOX 14, but this behavior can be changed with another bad egg).

As there are 14 boxes, each box name is 8 characters long and a byte is described by 2 hexadecimal digits, you can write up to
`14*8/2=56` bytes with one ACE execution.

## Prerequisite

- An ACE glitch species (for instance 0x40E9 for the english version). Unstable species such as 0x611 are not recommended (you will loose a lot of time hatching them)
- If you use a glitch species that executes Thumb code such as 0x40E9, you will also need a Thumb->ARM bootstrap
- A [certificate exit code bootstrap](exit-code.md) (you can place it in the first slot of BOX 14 for instance, and if you have renamed your BOX 14 since the creation of the bootstrap, don't forget to restore it with the code [`Restore 'BX r0' in box 14 name`](https://e-sh4rk.github.io/EmeraldACE_web/))

## Let's go

The creation of this bad egg is a little tedious: you will need to execute 10 ACE codes
the one after the other. Fortunately, you can save and restart as many times as you want during this process, there's no risk to corrupt your save.

Each ACE code will write 8 bytes of data in the BOX 10 slot 19, for a total of 80 bytes
(the entire slot). Please ensure your BOX 10 slot 19 is empty before starting.

Note that, unlike some other ACE codes, you can freely view BOX 10 content during this process,
it will not corrupt the data we are writing.

```
=============== CODE 1 ===============

Box  1: 4 C U n … ” Q n	[4CUn…”Qn]
Box  2: _ _ _ F ‘ ! n _	[   F‘!n ]
Box  3: _ _ d U … o _ _	[  dU…o  ]
Box  4: _ 1 F ? n _ _ _	[ 1F?n   ]
Box  5: ’ F Q m 8 R … o	[’FQm8R…o]
Box  6: _ _ _ 1 S R n _	[   1SRn ]
Box  7: _ _ l G R n _ _	[  lGRn  ]
Box  8: _ … F Q m _ _ _	[ …FQm   ]
Box  9: r R … o h U R n	[rR…ohURn]
Box 10: _ _ _ ” F Q m _	[   ”FQm ]
Box 11: _ _ S F ? n _ _	[  SF?n  ]
Box 12: _ ♀ F Q m _ _ _	[ ♀FQm   ]
Box 13: _ _ _ … _ _ _ _	[   …    ]

=============== CODE 2 ===============

Box  1: 4 C U n _ … Q n	[4CUn …Qn]
Box  2: _ _ _ L S … o _	[   LS…o ]
Box  3: _ _ U F ? n _ _	[  UF?n  ]
Box  4: _ ” F Q m _ _ _	[ ”FQm   ]
Box  5: z S … o “ S ? n	[zS…o“S?n]
Box  6: _ _ _ 0 S ? n _	[   0S?n ]
Box  7: _ _ ’ F Q m _ _	[  ’FQm  ]
Box  8: _ F R … o _ _ _	[ FR…o   ]
Box  9: p G ? n 3 G ? n	[pG?n3G?n]
Box 10: _ _ _ … F Q m _	[   …FQm ]
Box 11: _ _ m R … o _ _	[  mR…o  ]
Box 12: _ 7 U ? n _ _ _	[ 7U?n   ]
Box 13: ♀ F Q m _ _ _ _	[♀FQm    ]

=============== CODE 3 ===============

Box  1: 4 C U n … ” ! n	[4CUn…”!n]
Box  2: _ _ _ F ‘ Q n _	[   F‘Qn ]
Box  3: _ _ z T … o _ _	[  zT…o  ]
Box  4: _ z F ? n _ _ _	[ zF?n   ]
Box  5: x G ? n … F Q m	[xG?n…FQm]
Box  6: _ _ _ 7 F ? n _	[   7F?n ]
Box  7: _ _ ’ F Q m _ _	[  ’FQm  ]
Box  8: _ o R … o _ _ _	[ oR…o   ]
Box  9: – F R n ♀ F Q m	[–FRn♀FQm]
Box 10: _ _ _ z U ? n _	[   zU?n ]
Box 11: _ _ z F ? n _ _	[  zF?n  ]
Box 12: _ m F ? n _ _ _	[ mF?n   ]
Box 13: ” F Q m _ _ _ _	[”FQm    ]

=============== CODE 4 ===============

Box  1: 4 C U n F ” ! n	[4CUnF”!n]
Box  2: _ _ _ F ‘ ! n _	[   F‘!n ]
Box  3: _ _ d T … o _ _	[  dT…o  ]
Box  4: _ 3 U ? n _ _ _	[ 3U?n   ]
Box  5: … F Q m M S … o	[…FQmMS…o]
Box  6: _ _ _ W F ? n _	[   WF?n ]
Box  7: _ _ ” F Q m _ _	[  ”FQm  ]
Box  8: _ z S … o _ _ _	[ zS…o   ]
Box  9: ? T ? n 0 T ? n	[?T?n0T?n]
Box 10: _ _ _ J G ? n _	[   JG?n ]
Box 11: _ _ ♀ F Q m _ _	[  ♀FQm  ]
Box 12: _ ” R … o _ _ _	[ ”R…o   ]
Box 13: … H ? n ’ F Q m	[…H?n’FQm]

=============== CODE 5 ===============

Box  1: 4 C U n F ” ! n	[4CUnF”!n]
Box  2: _ _ _ … ” ! n _	[   …”!n ]
Box  3: _ _ V H … o _ _	[  VH…o  ]
Box  4: _ … H R n _ _ _	[ …HRn   ]
Box  5: ’ F Q m z S … o	[’FQmzS…o]
Box  6: _ _ _ 0 T ? n _	[   0T?n ]
Box  7: _ _ F H ? n _ _	[  FH?n  ]
Box  8: _ ” F Q m _ _ _	[ ”FQm   ]
Box  9: … R … o … F Q m	[…R…o…FQm]
Box 10: _ _ _ p R … o _	[   pR…o ]
Box 11: _ _ q F R n _ _	[  qFRn  ]
Box 12: _ ♀ F Q m _ _ _	[ ♀FQm   ]
Box 13: _ _ _ … _ _ _ _	[   …    ]

=============== CODE 6 ===============

Box  1: 4 C U n ? “ ! n	[4CUn?“!n]
Box  2: _ _ _ … ” Q n _	[   …”Qn ]
Box  3: _ _ u T … o _ _	[  uT…o  ]
Box  4: _ 2 U ? n _ _ _	[ 2U?n   ]
Box  5: 0 U ? n ♀ F Q m	[0U?n♀FQm]
Box  6: _ _ _ z F ? n _	[   zF?n ]
Box  7: _ _ x G ? n _ _	[  xG?n  ]
Box  8: _ F I ? n _ _ _	[ FI?n   ]
Box  9: ” F Q m … R … o	[”FQm…R…o]
Box 10: _ _ _ ’ F Q m _	[   ’FQm ]
Box 11: _ _ V H ? n _ _	[  VH?n  ]
Box 12: _ … H R n _ _ _	[ …HRn   ]
Box 13: … F Q m _ _ _ _	[…FQm    ]

=============== CODE 7 ===============

Box  1: 4 C U n ? “ ! n	[4CUn?“!n]
Box  2: _ _ _ F ‘ Q n _	[   F‘Qn ]
Box  3: _ _ … H … o _ _	[  …H…o  ]
Box  4: _ F I R n _ _ _	[ FIRn   ]
Box  5: … F Q m M S … o	[…FQmMS…o]
Box  6: _ _ _ P F ? n _	[   PF?n ]
Box  7: _ _ ♀ F Q m _ _	[  ♀FQm  ]
Box  8: _ 0 R … o _ _ _	[ 0R…o   ]
Box  9: Z F R n 3 G R n	[ZFRn3GRn]
Box 10: _ _ _ ’ F Q m _	[   ’FQm ]
Box 11: _ _ p R … o _ _	[  pR…o  ]
Box 12: _ 4 F R n _ _ _	[ 4FRn   ]
Box 13: ” F Q m _ _ _ _	[”FQm    ]

=============== CODE 8 ===============

Box  1: 4 C U n B “ ! n	[4CUnB“!n]
Box  2: _ _ _ ’ S … o _	[   ’S…o ]
Box  3: _ _ 3 T R n _ _	[  3TRn  ]
Box  4: _ Z G R n _ _ _	[ ZGRn   ]
Box  5: ♀ F Q m z F ? n	[♀FQmzF?n]
Box  6: _ _ _ 3 G ? n _	[   3G?n ]
Box  7: _ _ ” F Q m _ _	[  ”FQm  ]
Box  8: _ / R … o _ _ _	[ /R…o   ]
Box  9: 4 S R n C F R n	[4SRnCFRn]
Box 10: _ _ _ ’ F Q m _	[   ’FQm ]
Box 11: _ _ m S ? n _ _	[  mS?n  ]
Box 12: _ 0 S R n _ _ _	[ 0SRn   ]
Box 13: … F Q m _ _ _ _	[…FQm    ]

=============== CODE 9 ===============

Box  1: 4 C U n h “ ! n	[4CUnh“!n]
Box  2: _ _ _ 7 F … o _	[   7F…o ]
Box  3: _ _ 3 G R n _ _	[  3GRn  ]
Box  4: _ ’ F Q m _ _ _	[ ’FQm   ]
Box  5: / R … o 4 S R n	[/R…o4SRn]
Box  6: _ _ _ C F R n _	[   CFRn ]
Box  7: _ _ … F Q m _ _	[  …FQm  ]
Box  8: _ m R … o _ _ _	[ mR…o   ]
Box  9: t F ? n 0 F ? n	[tF?n0F?n]
Box 10: _ _ _ ” F Q m _	[   ”FQm ]
Box 11: _ _ V F ? n _ _	[  VF?n  ]
Box 12: _ ♀ F Q m _ _ _	[ ♀FQm   ]
Box 13: _ _ _ … _ _ _ _	[   …    ]

=============== CODE 10 ===============

Box  1: 4 C U n V “ ! n	[4CUnV“!n]
Box  2: _ _ _ … ” ! n _	[   …”!n ]
Box  3: _ _ l S … o _ _	[  lS…o  ]
Box  4: _ 1 T ? n _ _ _	[ 1T?n   ]
Box  5: B G ? n ” F Q m	[BG?n”FQm]
Box  6: _ _ _ m R … o _	[   mR…o ]
Box  7: _ _ B G ? n _ _	[  BG?n  ]
Box  8: _ ♀ F Q m _ _ _	[ ♀FQm   ]
Box  9: z T ? n J G ? n	[zT?nJG?n]
Box 10: _ _ _ … F Q m _	[   …FQm ]
Box 11: _ _ y T ? n _ _	[  yT?n  ]
Box 12: _ ’ F Q m _ _ _	[ ’FQm   ]
Box 13: _ _ _ … _ _ _ _	[   …    ]
```

If you entered all the codes correctly, your BOX 10 slot 19 should contain a bad egg,
and no other slot should have been corrupted.

If it is the case, just move the bad egg to the last slot of BOX 14, and you are done.
Note that the certificate exit code bootstrap must always be placed at least two slots before the hexadecimal-writer bad egg when using it.

When you don't want to use the hexadecimal-writer bad egg (if you just want to execute a standard ACE code for instance), just move it before the last row of BOX 11 and it will not be executed.

## Testing everything worked

In order to test your setup, you can enter the following box names and execute ACE.

```
Box  1: 00000000
Box  2: 00000000
Box  3: BDDCD5E6
Box  4: E0D9E7FF
Box  5: FFFF0002
Box  6: 00000000
Box  7: 00000000
Box  8: 01000000
Box  9: 01000000
Box 10: 00000000
Box 11: 00000000
Box 12: 00000000
Box 13: 00000000
Box 14: 00000000
```

Your BOX 14 slot 29 should now contain a shiny Bulbasaur with the name *Charles*.

## Advanced use

- You can change the location where this bad egg writes data by modifying the value
of the register `r12` before the execution of the bad egg. If this register
contains a value greater or equal to `0x02000000`, it will write to this address.

- If you want to write less than 56 bytes or if you don't want to modify some data, you can write two spaces in the box name when you don't want to overwrite data. For instance,
`0011__22` will write the following consecutive bytes: `00`, `11`, SKIP, `22`.
**All box names should be 8-characters long** (a 6-characters long box name will NOT
skip the last byte, you should fill the end of the box name with spaces if that is what you want). If you want to skip all the 4 bytes corresponding to a box name, you can write any character followed by 7 spaces.

For information, here is the hexadecimal data corresponding to the bad egg:
```
46808FE2
02045CE3
62C04F32
0090A0E3
0910D8E7
B11051E2
10109132
0BB28150
00B09C45
01001AE3
01B0CC14
00B0A013
07005AE3
01A08A32
00A0A023
01908922
019089E2
7E0059E3
40F04F42
10FF2FE1
```

# Crafting Table bad egg

This bad egg will make the hexadecimal writer more convenient to use.

One issue with the hexadecimal writer bad egg is that it always writes in bytes 0-56 of the BOX 14 slot 29. Thus, it is not possible to write data in the bytes 56-80 of a slot.

The crafting table bad egg will change this behavior: it will define an area of 30 slots (starting in the slot just after the location of this bad egg) such that:
- The location of a write will be the first location 4-bytes aligned in the crafting table area that contains 56 consecutives bytes 00. It means that, assuming the data you write does not end with multiple 00, your first write will be performed in bytes 0-56 of the first slot, then your next write will be performed in bytes 56-80 of the first slot and bytes 0-32 of the second slot, etc.
- The data in the area of the crafting table will not be executed when triggering ACE (it will be skipped). Thus, you can freely store the data you want in this area.

In order to create this crafting table bad egg, just write those box names and trigger the hexadecimal-writer bad egg:

```
Box  1: 46C08FE2
Box  2: 0080A0E3
Box  3: 08909CE7
Box  4: 048088E2
Box  5: 000000FF
Box  6: 000059E3
Box  7: 08C08C10
Box  8: 20F04F12
Box  9: 380058E3
Box 10: 000000FF
Box 11: 28F04F32
Box 12: 02901FE5
Box 13: 09F08FE0
Box 14: 74090000
```

A bad egg should appear in BOX 14 slot 29. In order for it to be active, you can place it anywhere after the Thumb->ARM bootstrap (or the ARM entry point of your ACE setup). It does not need to be after the certificate exit code bootstrap as it does not use any exit code. As the 30 slots following this bad egg will be skipped when triggering ACE, you should put it at least 30 slots before the certificate exit code bootstrap (or any data that you want to be executed).

We recommand placing it in BOX 12 slot 9 as you will need to place it there if you want to setup the binary editor and the save hack that allows it to persist after a restart.

If you follow our advice, you boxes should look like that:

```
BOX 12:
-  -  -  -  -  -
A  -  C  +  +  +
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
E  -  -  -  -  -
-  -  -  -  -  -
-  -  -  -  -  -
-  -  -  -  -  -
-  -  -  -  -  W

-: Empty slot
A: Thumb->ARM bootstrap (if any)
C: Crafting table bad egg
+: Area of the crafting table
E: Exit code bootstrap
W: Hexadecimal writer bad egg
```

## Example of use: creating any Pokemom from scratch

You can use the hexadecimal-writer bad egg together with the crafting table in order to write the data of the Pokemon you want. It will take you only 2 codes!

1. First, you have to determine the hexadecimal data of the Pokemon you want. You can use [PokeGlitzer](https://github.com/E-Sh4rk/PokeGlitzer) for that (or if you prefer, you can use PkHex to generate the Pokemon you want, save it into a *.sav* file and open it in PokeGlitzer in order to view the hexadecimal data of the Pokemon).

2. Once you know the data to write, please ensure your boxes 12-14 match the setup recommended above (or something equivalent), check that the two first slots of your crafting table are empty, and start writing the hexadecimal data in the box names. Stop after 40 bytes (half of the Pokemon data): you should have reached BOX 11. Fill the remaining boxes (11-14) with `00000000`.
   
3. Select BOX 1, exit the PC and trigger ACE.
   
4. Now, go back into your PC and fill again the boxes 1-10 with the remaining data **without looking at BOX 12** (or where your crafting table area is). As your Pokemon data is not fully written yet, viewing it in the PC would turn it into a bad egg due to a wrong checksum.

5. Once you've filled the boxes 1-10 with the remaining data, exit the PC and trigger ACE again. That's it, your Pokemon is waiting you in the first slot of the crafting table!

*NOTE: if the first half (40 bytes) of your Pokemon data ends with the bytes `00 00 00 00` (it can happen if your Pokemon has no experience and has a PID equal to its OTID), then the second write will start 4 bytes earlier. In order to compensate that, you must start the second code by `00000000` (and write the second half of the data in the boxes 2-11).*