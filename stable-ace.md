# Stable ACE species: 0x40E9 with Thumb->ARM bootstrap

The purpose of this tutorial is to create the stable ACE species 0x40E9 (a stable ACE species is a species that can trigger ACE by viewing its summary, without crashing as 0x611 would do), as well as a Thumb->ARM bootstrap, i.e. a special bad egg that will allow executing regular ACE codes (composed of ARM instructions) with species that would normally execute THUMB instructions (such as 0x40E9).

**Credits:** This tutorial is an adapation of [Merrp's tutorial](https://pastebin.com/Sz2Aiu6p). The code for generating 0x40E9 has been changed, but not the code for the Thumg->ARM Bootstrap: credits goes to Merrp. 

## Prerequisite

- An ARM ACE glitch species such as 0x611

## Let's go

First, we will generate a 0x40E9 species. Ensure your BOX 10 slot 19 is empty
(first slot of the fourth row), and enter these box names:

```
Box  1: 4 C U n f S … o	[4CUnfS…o]
Box  2: _ _ _ 3 T ? n _	[   3T?n ]
Box  3: _ _ 3 G ? n _ _	[  3G?n  ]
Box  4: _ ‘ G w m _ _ _	[ ‘Gwm   ]
Box  5: ’ F w m _ _ _ _	[’Fwm    ]
Box  6: _ _ _ _ _ _ … _	[      … ]
Box  7: _ _ l G E n _ _	[  lGEn  ]
Box  8: _ m … l o _ _ _	[ m…lo   ]
Box  9: y ♀ Q o m ” Q o	[y♀Qom”Qo]
Box 10: _ _ _ _ … ? q _	[    …?q ]
Box 11: _ _ h T – n _ _	[  hT–n  ]
Box 12: _ Y N ? n _ _ _	[ YN?n   ]
Box 13: F N R o b _ ? n	[FNRob ?n]
Box 14: _ _ _ _ _ _ … _	[      … ]
```

Now, hatch a 0x611 egg in order to trigger ACE. Don't forget to clone your 0x611 egg if it's your last copy (in case you would need to hatch another one in the future). Alternatively, you can also register a hatched 0x611 species in a contest in order to trigger ACE. Reminder: the last row of your box 11 as well as your boxes 12-14 must be empty (or only contain Pokemons specifically designed for ACE) when executing ACE.

You should be teleported in front of a Pokemon Center, and a decamark should have appeared in your BOX 10 slot 19: this is your 0x40E9 species. Leave it there for now, and do not open its summary. Its species name should look like this: ` ÓàÉ LvLv` and it should be a female level 63. If it is the case, you can save the game if you want. Now, write the following box names (do not change the name of the boxes 6-14):

```
Box  1: 4 C U n l “ Q n	[4CUnl“Qn]
Box  2: _ _ _ z S … o _	[   zS…o ]
Box  3: _ _ u S ? n _ _	[  uS?n  ]
Box  4: _ 3 T ? n _ _ _	[ 3T?n   ]
Box  5: ♀ I w m _ _ _ _	[♀Iwm    ]
```

Execute the code using 0x611, as previously. Once again, you should be teleported in front of a Pokemon Center, and your decamark in your BOX 10 slot 19 should now be level 100. If it is the case, you can save the game if you want.

Now, before being able to use it, we have to create the Thumb->ARM bootstrap.
Catch any Pokemon and name it `x♂zN 6FFxC`, then put it in your BOX 10 slot 20 (just after the newly created decamark). Then, write these box names (do not change the name of your BOX 14, the previous codes should have renamed it `Œ` and you have to leave this name for this code):

```
Box  1: x ♂ z N _ 6 F F	[x♂zN 6FF]
Box  2: X _ X x C _ _ _	[X XxC   ]
Box  3: _ _ 4 C U n _ _	[  4CUn  ]
Box  4: _ ♀ 2 Q m _ _ _	[ ♀2Qm   ]
Box  5: , 2 Q m / 2 Q m	[,2Qm/2Qm]
Box  6: _ _ _ A 2 w m _	[   A2wm ]
Box  7: _ _ D F w m _ _	[  DFwm  ]
Box  8: _ x U … o _ _ _	[ xU…o   ]
Box  9: k N ? n z H ? n	[kN?nzH?n]
Box 10: _ _ _ _ F ! q _	[    F!q ]
Box 11: _ _ z P – n _ _	[  zP–n  ]
Box 12: _ p Q ? n _ _ _	[ pQ?n   ]
Box 13: 1 R ? n T _ ? n	[1R?nT ?n]
```

Do not execute this code with 0x611. Instead, save your game and reload your save (it will reset the value of some CPU registers). Now, open the summary of the decamark in BOX 10 slot 19. It should open the Pokedex completion diploma. Moreover, your pokemon in the BOX 10 slot 20 should have turned into a bad egg: this is your Thumb->ARM bootstrap.

Move this bad egg in your BOX 12 slot 7 (it must be there each time you want to execute a regular ACE code using 0x40E9), and take the 0x40E9 decamark in your party. Now, you will be able to trigger an ACE code just by looking at its summary. You can save (unless you prefer to test it before, in this case, refer to next section).

## Testing everything worked

Enter these box names (do not change your current BOX 14 name).

```
Box  1: 4 C U n V H … o	[4CUnVH…o]
Box  2: _ _ _ … H R n _	[   …HRn ]
Box  3: _ _ ‘ G w m _ _	[  ‘Gwm  ]
Box  4: _ ’ F w m _ _ _	[ ’Fwm   ]
Box  5: _ _ _ … _ _ _ _	[   …    ]
Box  6: _ _ _ _ _ _ … _	[      … ]
Box  7: _ _ _ _ _ … _ _	[     …  ]
Box  8: _ _ _ _ … _ _ _	[    …   ]
Box  9: _ _ _ … _ _ _ _	[   …    ]
Box 10: _ _ _ _ _ _ … _	[      … ]
Box 11: _ _ z P – n _ _	[  zP–n  ]
Box 12: _ p Q ? n _ _ _	[ pQ?n   ]
Box 13: 1 R ? n T _ ? n	[1R?nT ?n]
```

Now, open the summary of your 0x40E9. It should open the Pokedex completion diploma,
and a shiny Bulbasaur should have appeared in your BOX 10 slot 19 (do not use it in battle, most of its data is irrelevant, this is just a test).
