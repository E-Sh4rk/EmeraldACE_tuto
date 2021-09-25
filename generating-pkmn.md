# Generating Pokemons with the crafting table

One possible use of the crafting table is to write Pokemons from scratch. Here is a tutorial for that.

## Prerequisite

- A stable ACE glitch species such as [0x40E9](stable-ace.md) (with its Thumb->ARM bootstrap)
- A [certificate exit code bootstrap](exit-code.md) (you can place it in the first slot of BOX 14 for instance). Note that it does not matter if you have renamed your BOX 14 as the creation of this bad egg uses the hexadecimal-writer bad egg
- The [hexadecimal-writer and crafting table bad eggs](hex-writer.md)

## Generating any Pokemon from scratch

You can use the hexadecimal-writer bad egg together with the crafting table in order to write the data of the Pokemon you want. It will take you only 2 codes!

1. First, you have to determine the hexadecimal data of the Pokemon you want. You can use [PokeGlitzer](https://github.com/E-Sh4rk/PokeGlitzer) for that (or if you prefer, you can use PkHex to generate the Pokemon you want, save it into a *.sav* file and open it in PokeGlitzer in order to view the hexadecimal data of the Pokemon).

2. Once you know the data to write, please ensure your boxes 12-14 match the [setup recommended](hex-writer.md) (or something equivalent), check that the two first slots of your crafting table are empty, and start writing the hexadecimal data in the box names. Stop after 40 bytes (half of the Pokemon data): you should have reached BOX 11. Fill the remaining boxes (11-14) with `00000000`.
   
3. Select BOX 1, exit the PC and trigger ACE.
   
4. Now, go back into your PC and fill again the boxes 1-10 with the remaining data **without looking at BOX 12** (or where your crafting table area is). As your Pokemon data is not fully written yet, viewing it in the PC would turn it into a bad egg due to a wrong checksum.

5. Once you've filled the boxes 1-10 with the remaining data, exit the PC and trigger ACE again. That's it, your Pokemon is waiting you in the first slot of the crafting table!

*NOTE: if the first half (40 bytes) of your Pokemon data ends with the bytes `00 00 00 00` (it can happen if your Pokemon has no experience and has a PID equal to its OTID), then the second write will start 4 bytes earlier. In order to compensate that, you must start the second code by `00000000` (and write the second half of the data in the boxes 2-11).*

## Example 1 : Generating a JAA Celebi

Ensure the first two slots of your crafting table area are empty, and execute the hexadecimal-writer bad egg with these 2 codes **without looking at BOX 12** (or where your crafting table area is) between the execution of the two codes:

```
(codes by @rileyk64)

Box 1:  500361A0
Box 2:  0A000000
Box 3:  BDBFC6BF
Box 4:  BCC3FF00
Box 5:  00000202
Box 6:  A2A100BB
Box 7:  C8C3D000
Box 8:  D4690000
Box 9:  5A0361A0
Box 10: 5A0361A0
Boxes 11-14: 00000000

Box 1:  5A0361A0
Box 2:  5AFC2701
Box 3:  C10CD2B7
Box 4:  5A0361A0
Box 5:  A10361A0
Box 6:  DA4064A0
Box 7:  5A4561A0
Box 8:  AC0399A0
Box 9:  B803A2A0
Box 10: 5F0C49A5
Boxes 11-14: 00000000
```

The Celebi should have been generated in the first slot of your crafting table area.

## Example 2 : Generating a shiny Wishmaker Jirachi

Ensure the first two slots of your crafting table area are empty, and execute the hexadecimal-writer bad egg with these 2 codes **without looking at BOX 12** (or where your crafting table area is) between the execution of the two codes:

```
(codes by @rileyk64)

Box 1:  8D60C12E
Box 2:  4B4E0000
Box 3:  C4C3CCBB
Box 4:  BDC2C3FF
Box 5:  08700202
Box 6:  D1C3CDC2
Box 7:  C7C5CC00
Box 8:  D3B20000
Box 9:  5F2F6B2E
Box 10: 5A2EC12E
Boxes 11-14: 00000000

Box 1:  C64AC12E
Box 2:  C6D1C40F
Box 3:  39C4130B
Box 4:  C62EC12E
Box 5:  C62EC12E
Box 6:  C62EC12E
Box 7:  C62EC12E
Box 8:  D72F9C2E
Box 9:  5A2EC12E
Box 10: CC37CB2E
Boxes 11-14: 00000000
```

The Jirachi should have been generated in the first slot of your crafting table area.
