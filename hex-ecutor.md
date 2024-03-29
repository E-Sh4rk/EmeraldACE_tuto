*UPDATE: The HeXecutor has been updated on 2021/12/30 in order to fix an issue on console.*

**The Pokemon created in this tutorial should not be marked or moved in your party: it could corrupt it.**

# HeXecutor

The *HeXecutor* is a special Exeggutor that modifies the behavior of the hexadecimal writer: instead of writing the hexadecimal in the boxes, it will execute it (without storing it in the boxes).

## Prerequisite

- A stable ACE glitch species such as [0x40E9](stable-ace.md) (with its Thumb->ARM bootstrap)
- A [certificate exit code bootstrap](exit-code.md) (you can place it in the first slot of BOX 14 for instance). Note that it does not matter if you have renamed your BOX 14 as the creation of this bad egg uses the hexadecimal-writer bad egg
- The [hexadecimal-writer](hex-writer.md)

## Let's go

NOTE: the codes given here are for the english version. However, it should also work on other european versions (not tested yet).

If you have a crafting table, ensure the first two slots of your crafting table area are empty. Otherwise, ensure the slot preceding your hexadecimal writer is empty. Then, execute the hexadecimal-writer bad egg with this code (the spaces are just for readability):

```
Box  1: 0A 80 4F E2
Box  2: 01 01 2D E9
Box  3: 02 00 9F E5
Box  4: 02 C0 9F E5
Box  5: 0C F0 8F E2
Box  6: 00 FA 03 02
Box  7: 03 00 BD E8
Box  8: 13 25 00 00
Box  9: 6C 81 00 00
Box 10: 00 C0 80 E5
Box 11: 04 C0 80 E2
Box 12: 1C F0 8F E2
Box 13: 00 00 00 00
Box 14: 00 00 00 00
```

You should now have a Exeggutor in the first slot of your crafting table (or in the slot preceding your hex-writer if you have no crafting table).

## How to use it

Now, when this Exeggutor is present before the hex-writer and after the exit code bootstrap
(for instance, you can put it in the slot just before the hex-writer),
your box names will be interpreted as hexadecimal code and executed.

For instance, you can test it by renaming you box 1 to `10FF2FE1` (the encoding of `bx r0`)
and triggering ACE: it should open the Pokedex completion diploma (or whichever routine your exit code bootstrap is using).

Here are some notes about the execution:
- The code will not be executed from the box names location as usual, but from the address
`0203FA08`. You should take that into account when doing PC-relative operations.
- The register `r1` will contain the address of the HeXecutor data (useful to compute ASLR-dependent addresses)
- Your code should end with a `bx r0`or `bx lr` instruction.
- The PC register will not be misaligned as it is the case for traditional ACE executions.
- The initial state of the carry flag in the `CPSR` register is not guaranteed,
thus you should avoid using `ADC` or `SBC` as in traditional ACE (`ADD` and `SUB` should be used instead).
