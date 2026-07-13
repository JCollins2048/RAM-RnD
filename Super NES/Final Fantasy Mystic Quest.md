# *Final Fantasy Mystic Quest* (W) RAM Addresses
RAM addresses and values in *Final Fantasy Mystic Quest* (Super NES, all regions).

Addresses are WRAM offsets corresponding to Super NES WRAM address `$7E:xxxx` (add `$7E0000` to the listed value).

All values are **8-bit** unless otherwise noted.<br>Multi-byte values (**16-bit or higher**) are stored in **little-endian** format: least significant byte first, most significant byte last.

## General Addresses
```
0x000E84 - GP (24-bit)                  0x000E97 - Play Time (32-bit)
0x000E9B - Message Speed                0x000E9C - Window Color (16-Bit Math)

0x000E9E - Usable Item 1 (Type)         0x000E9F - Usable Item 1 (Amount)
0x000EA0 - Usable Item 2 (Type)         0x000EA1 - Usable Item 2 (Amount)
0x000EA2 - Usable Item 3 (Type)         0x000EA3 - Usable Item 3 (Amount)
0x000EA4 - Usable Item 4 (Type)         0x000EA5 - Usable Item 4 (Amount)

0x000EA6 - Quest Items (16-Bit Math)

0x000EC6 - Life Indicate (4-bit Upper)  0x000EC6 - Player Visible? (4-bit Lower)
```

## Character Stats (`0x80` Bytes Each)
```
0x001000 - Player                       0x001080 - Companion
```

### Byte Layout
#### Player and Companion
```
+0x00 - Name (8 bytes)                  +0x10 - Level                           
+0x14 - Current Life (16-bit)           +0x16 - Max. Life (16-bit)

+0x18 - White Magic (Spells Left)       +0x1B - White Magic (Spells Max)
+0x19 - Black Magic  (Spells Left)      +0x1C - Black Magic (Spells Max)
+0x1A - Wizard Magic  (Spells Left)     +0x1D - Wizard Magic (Spells Max)

+0x21 - Status (Bit Math)

+0x22 - Current Attack                  +0x26 - Base Attack
+0x23 - Current Defense                 +0x27 - Base Defense
+0x24 - Current Speed                   +0x28 - Base Speed
+0x25 - Current Magic                   +0x29 - Base Magic
+0x40 - Accuracy                        +0x41 - Evade

+0x30 - Ammo Count                      +0x31 - Equipped Weapon
+0x38 - Held Magic Tomes (Bit Math)
```

#### Player Only
```
+0x11 - Exp. (24-bit)
+0x20 - Run Away (4-bit Upper)
+0x32 - Weapons Owned (16-Bit Math)     +0x35 - Armor Owned (16-Bit Math)
```

#### Companion Only
```
+0x20 - Control (4-bit Upper)           +0x20 - Which Companion? (4-bit Lower)
+0x35 - Helmet (4-bit Upper)            +0x35 - Armor (4-bit Lower)
+0x36 - Shield (4-bit Upper)            +0x36 - Accessory (4-bit Lower)
```

### Notes
#### General Addresses
- The timer increments once per rendered frame. So, if the game has been running for 90,210 (`$16062`) frames, then the in-game timer will read "00:25".
  - This was **not** adjusted for the European / PAL version, which runs at 50 FPS (~17% slower).
- The in-game timer only displays hours and minutes despite having theoretical functionality for seconds or even days.
- The in-game timer only displays the first two digits of the hours number. (Example: 103 hours displays as "03".)
- The "Player Visible?" value is used during cutscenes where the camera moves around.
- Any item can be placed into the "usable item" slots, but only the actual usable items do anything.
  - Outside of combat, using unusable items (quest items, weapons, et cetera) either has them act like a Cure Potion (items before `$10`) or do nothing (after `$13`).
  - *In* combat, using unusable items does one of two things:
    - If used by the player, they attack the left-most enemy with their equipped weapon. If Bombs are equipped, they attack all enemies.
    - If used by the companion, they attack whomever was targeted. If forced to have Bombs equipped, they'll attack all enemies.
    - If *either* character has Bombs equipped but no ammo, they'll use Bare Hands against all enemies, but do Bomb damage against the second and third enemies.

#### Character Stats
- Companion characters technically have Exp. and Weapons Owned values. However, due to how companion characters function, they aren't ever set to anything meaningful and go unused.
- Changing the companion value only changes the battle sprite. Swapping Kaeli (`$1`) for Tristan (`$2`), for example, doesn't change stats, equipment, spells, or who appears on the save menu.

## Expected Value Ranges
### General Addresses
```
GP: $000000–$98967F                     Play Time: $00000000–$FFFFFFFF
Message Speed: $00–$06                  Window Color: $0000–$7FFF

Usable Item Type: $FF, $10–$13          Usable Item Amount: $00–$63
Quest Items: $0000–$FFFF

Life Indicate: $0 or $8                 Player Visible?: $0 or $4
```

### Character Stats
```
Name:
  USA (8 bytes): $03, $90–$DD, $FF        Japan (6 bytes): $03, $4B–$FC, $FF

Level: $01–$29                          Life: $0028–$0668

White Magic: $03–$2B                    Black Magic: $00–$15
Wizard Magic: $00–$0A

Status: $00–$80

Current Attack: $07–$84                 Base Attack: $07–$7F
Current Defense: $0C–$88                Base Defense: $06–$56
Current Speed: $08–$67                  Base Speed: $08–$58
Current Magic: $0A–$3C                  Base Magic: $0A–$32
Accuracy: $4B–$5F                       Evade: $00–$30

Ammo Count: $00–$63                     Equipped Weapon: $20–$2B, $2C–$2E
Held Magic Tomes: $0000–$FFF0
```

#### Player Only
```
Exp.: $000000–$98967F
Run Away: $0 or $4
Weapons Owned: $0000–$FFF0              Armor Owned: $000000–$FC3B80
```

#### Companion Only
```
+0x20 - Control (4-bit Upper)           +0x20 - Which Companion? (4-bit Lower)
+0x35 - Helmet (4-bit Upper)            +0x35 - Armor (4-bit Lower)
+0x36 - Shield (4-bit Upper)            +0x36 - Accessory (4-bit Lower)
```

### Notes
#### General Addresses
- The "GP" value resets to `$98967F` if set higher.
- The in-game timer can exceed 99 hours, 59 minutes, 59 seconds, and 59 frames (`$14996FF`, displayed as "99:59") and, in fact, can go all the way up to 19,884 hours, 6 minutes, 28 seconds, and 15 frames (`$FFFFFFFF`, displayed as "84:06") before rolling back around to 0 minutes (`$00000000`, displayed as "00:00").
- The window color setting works like this:
> **Intensity 0–7:**<br>Red = `+$0004`, Green = `+$0080`, Blue = `+$1000`
> **Intensity 8:**<br>Red = `+$0003`, Green = `+$0060`, Blue = `+$0C00`
> **Example:**<br>Hot Pink (`$4098`) = Red: `+0018`, Green: `+0080`, Blue = `+$4000`

#### Character Stats
- There are some statistical differences between the USA / Japan versions and the Europe version of the game:
  - The damage and stat calculation appear to use different formulas across versions.
  - Companion characters generally have *some* amount of Evade rather than 0. Kaeli, for example, has 18 (`$12`).
- Although the level is capped at 41 (`$29`), forcing it to 255 (`$FF`) causes the next level-up to wrap it to 0, after which leveling proceeds normally.
- Upon hitting 9,999,999 (`$98967F`) Exp., the player will be awarded with 2 White Magic and 1 Black Magic use. Consider, however, that it only takes 146,546 (`$23C72`) experience to hit the level cap.
- Companion equipment values are encoded rather than stored as item IDs. See the Values Appendix linked below.

# Reference Values
## Items
> *Please refer to [Final Fantasy Mystic Quest - Values Appendix.md](Final20%Fantasy20%Mystic20%Quest20%-20%Values20%Appendix.md)*