# Certificate exit-code bootstrap

The purpose of this tutorial is to create a special decamark that will allow us to skip
most of the *exit code* part when writing ACE codes in the box names
(consequently, more space will be available for the *payload* part).

## Prerequisite

- An ACE glitch species (for instance 0x40E9 for english version). Unstable species such as 0x611 are not recommended (you will loose a lot of time hatching them)
- If you use a glitch species that executes Thumb code such as 0x40E9, you will also need a Thumb->ARM bootstrap

## Let's go

NOTE: the codes given here are for the english version. For other languages,
you should refer to the [ACE code generator](https://e-sh4rk.github.io/EmeraldACE_web/).

The first step is to generate a pokemon of species `0xFF` in the BOX 10 slot 19
and, in the same time, to modify the name of BOX 14 with something that would not be writable
normally (more precisely, we will write the bytes corresponding to the command `BX r0`).

For that, just make sure the BOX 10 slot 19 is empty, write the following box names and
trigger ACE:

```
Box  1: 4 C U n b F … o	[4CUnbF…o]
Box  2: _ _ _ 3 G ? n _	[   3G?n ]
Box  3: _ _ ‘ G w m _ _	[  ‘Gwm  ]
Box  4: _ ’ F w m _ _ _	[ ’Fwm   ]
Box  5: _ _ _ … _ _ _ _	[   …    ]
Box  6: _ _ _ _ _ _ … _	[      … ]
Box  7: _ _ l G E n _ _	[  lGEn  ]
Box  8: _ m … l o _ _ _	[ m…lo   ]
Box  9: y ♀ Q o m ” Q o	[y♀Qom”Qo]
Box 10: _ _ _ _ … ? q _	[    …?q ]
Box 11: _ _ z P – n _ _	[  zP–n  ]
Box 12: _ p Q ? n _ _ _	[ pQ?n   ]
Box 13: 1 R ? n T _ ? n	[1R?nT ?n]
Box 14: _ _ _ _ _ _ … _	[      … ]
```

Now, we will modify some data of our newly created decamark.
For that, just write the following box names and trigger ACE (do not move the decamark nor
rename BOX 14):

```
Box  1: 4 C U n . K l o	[4CUn.Klo]
Box  2: _ _ _ J I ? n _	[   JI?n ]
Box  3: _ _ k N ? n _ _	[  kN?n  ]
Box  4: _ _ F ! q _ _ _	[  F!q   ]
Box  5: F ‘ ! n r H … o	[F‘!nrH…o]
Box  6: _ _ _ f G ? n _	[   fG?n ]
Box  7: _ _ 8 M ? n _ _	[  8M?n  ]
Box  8: _ E P ? n _ _ _	[ EP?n   ]
Box  9: _ F ! q … ” ! n	[ F!q…”!n]
Box 10: _ _ _ z P – n _	[   zP–n ]
Box 11: _ _ p Q ? n _ _	[  pQ?n  ]
Box 12: _ 1 R ? n _ _ _	[ 1R?n   ]
Box 13: T _ ? n _ _ ! q	[T ?n  !q]
```

That's it. The decamark should now have the name `Á q:·n`.
You should now move it somewhere after the Thumb->ARM bootstrap (or the ARM entry point of your ACE setup), but not in the last slot of BOX 14.
You can put it in the first slot of BOX 14 for instance.

*NOTE: Due to the way it was created, the decamark should not be moved using group selection
or it will disappear.*

You should not rename the BOX 14 (nor use a code that renames it), otherwise the exit code bootstrap will not work. Its name should be `Œ`. If your BOX 14 gets renamed, don't worry, just execute the following ACE code to restore the good name (the exit code bootstrap must be present in BOX 14, otherwise the following code will crash):

```
Box  1: _ _ _ … _ _ _ _	[   …    ]
Box  2: _ _ _ _ _ _ … _	[      … ]
Box  3: _ _ _ _ _ … _ _	[     …  ]
Box  4: _ _ _ _ … _ _ _	[    …   ]
Box  5: _ _ _ … _ _ _ _	[   …    ]
Box  6: _ _ _ _ _ _ … _	[      … ]
Box  7: _ _ l G E n _ _	[  lGEn  ]
Box  8: _ m … l o _ _ _	[ m…lo   ]
Box  9: y ♀ Q o m ” Q o	[y♀Qom”Qo]
Box 10: _ _ _ _ … ? q _	[    …?q ]
Box 11: _ _ _ _ _ … _ _	[     …  ]
Box 12: _ _ _ _ … _ _ _	[    …   ]
Box 13: _ _ _ … _ _ _ _	[   …    ]
Box 14: _ _ _ _ _ _ … _	[      … ]
```

## Testing everything worked

If you want to test your exit code bootstrap setup, just execute the following ACE code:

```
Box  1: _ _ _ … _ _ _ _	[   …    ]
Box  2: _ _ _ _ _ _ … _	[      … ]
Box  3: _ _ _ _ _ … _ _	[     …  ]
Box  4: _ _ _ _ … _ _ _	[    …   ]
Box  5: _ _ _ … _ _ _ _	[   …    ]
Box  6: _ _ _ _ _ _ … _	[      … ]
Box  7: _ _ _ _ _ … _ _	[     …  ]
Box  8: _ _ _ _ … _ _ _	[    …   ]
Box  9: _ _ _ … _ _ _ _	[   …    ]
Box 10: _ _ _ _ _ _ … _	[      … ]
Box 11: _ _ _ _ _ … _ _	[     …  ]
Box 12: _ _ _ _ … _ _ _	[    …   ]
Box 13: _ _ _ … _ _ _ _	[   …    ]
```

It should open the Pokédex completion diploma.
