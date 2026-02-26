# *Super Bomberman 5* RAM Addresses
RAM addresses and values in *Super Bomberman 5* (Super Famicom, Japan).

Addresses are WRAM offsets and correspond to Super Famicom address `$7E:xxxx` (add `$7E0000` to the listed value).

All values are **8-bit** unless otherwise noted.<br>Multi-byte values (**16-bit or higher**) are stored in **little-endian** format: least significant byte first, most significant byte last.

## Addresses
### Player Status
```
0x0015a2–0x0015a6 - P1 to P5 Status (8-Bit Bit Flag)
  Bit Flags (8-bit): +$04 = Invulnerable, +$20 = Stunned, +$40 = Dead

0x00170a–0x00170e - P1 to P5 I-Frames LoByte
  Expected Value Range: $00 - $ff

0x001722–0x001726 - P1 to P5 I-Frames HiByte
  Expected Value Range: $00 - $04

0x001782–0x001786 - Is P1 to P5 on a Rooey? (8-Bit Bit Flag)
  Expected Values: +$00 = No Rooey, +$02 = In Transit, +$80 = Riding Rooey
```

#### Notes
- The **Status** and **I-Frames** addresses must be used together to grant a player invulnerability.
- The **Is on a Rooey?** addresses work instantly, but may crash the game if used in the middle of a level.

### Player Customization
```
0x0016c2–0x0016c6 - P1 to P5 Character
  Expected Value Range: $00 - $09

0x0016da–0x0016de - P1 to P5 Palette
  Expected Value Range: $01 - $4f
```

#### Notes
- Changing the **character or palette** addresses work as expected for all players in a Normal or Battle Game, but will reset to their expected values at the map screen (Normal Game) or Score Board (Battle Game) unless frozen.

### Player Power-Ups
```
0x0015d2–0x0015d6 - P1 to P5 Speed (LoByte)
  Expected Value Range: $00–$e0 (in increments of $20)
  Default Values: $e0 (Normal Game), $00 (Battle Game)

0x0015ea–0x0015ee - P1 to P5 Speed (HiByte)
  Expected Value Range: $00–$02
  Default Values: $00 (Normal Game), $01 (Battle Game)

0x001662–0x001666 - P1 to P5 Hearts
  Expected Value Range: $00–$ff (Will "roll over"–$00 after $ff.)

0x00167a–0x00167e - P1 to P5 Block Pass Items (Reverse Bitmask)
  Expected Value Range: $e0–$80

0x0016c7–0x0016cb - P1 to P5 Rooey Type
  Expected Value Range: $00–$05

0x0017ca–0x0017ce - P1 to P5 Fire-Ups
  Expected Value Range: $02–$08

0x004ebd–0x004ec1 - P1 to P5 Bomb-Ups
  Expected Value Range: $01–$08

0x004ed5–0x004ed9 - P1 to P5 Power-Ups (Bitmask)
  Expected Value Range: $00–$4e
```

#### Notes
- In normal gameplay, players can only have one Bomb Type at a time (handled by the **Power-Ups** bitmask. However, if modded in, the game code happens to allow multiple active bomb abilities (with quirks):
  - **Remote Bomb** overrides all other bomb types visually and functionally, but preserves Pierce Bomb's piercing effect.
  - **Pierce Bomb** overrides Search Bomb and Mine Bomb visually, but preserves Search Bomb's tracking ability while ignoring Mine Bomb's trap ability.
  - **Search Bomb** takes precedence over Mine Bomb's trap ability, but retains Mine Bomb's graphics.
  - **Mine Bomb**, when combined with Pierce Bomb, retains its trap ability but uses Pierce Bomb's graphics.

- `0x0016c4` through `0x0016cc` are a sliding data block:
  - In a Normal Game, `0x0016c4` and `0x0016c5` are **Player 1 and Player 2's Rooey values**, and `0x0016c7` through `0x0016cb` (plus `0x0016cc`) are **enemy values**.
  - In a single-boss battle, `0x0016c4` is the **boss character value**, `0x0016c5` and `0x0016c6` are **Player 1 and Player 2's Rooey values**, and `0x0016c7` is **Boss 1's Rooey value**.
  - In a double-boss battle (Pirate and Subordinate), `0x0016c4` and `0x0016c5` are **Boss 1 and Boss 2's character values**, and `0x0016c6` and `0x0016c7` are **Player 1 and Player 2's Rooey values**, respectively. `0x0016c8` is **Boss 1's Rooey value**.
    - `0x0016c9` can also store **Boss 2's Rooey value**, though this goes unused in normal gameplay.
  - Any untouched values in a boss fight — typically `0x0016c9` through `0x0016cc` — may still be used for normal enemies. (Iron Mask or Baron Bombano fights.)

### Other Addresses
```
0x000e1c - Time Left (24-Bit)
  Expected Value Range: $0100eb–$05003b
  Disabled: $006309, Maximum: $3b3b09

0x001d23 - Normal Game Lives
  Expected Value Range: $00–$09

0x001031 - Current Room
  Expected Value Range: $00–$ae
```

## Values
### Characters

```
$00 - Bomberman                 $01 - Bomber Woof               $02 - Dave Bomber
$03 - Gary Bomber               $04 - Pirate Bomber             $05 - Muscle Bomber
$06 - Iron Mask Bomber          $07 - Baron Bombano             $08 - Plunder Bomber
$09 - Subordinate Bomber
```

#### Notes
- Despite being only a boss, **Subordinate Bomber** is fully functional with some small caveats:
  - He lacks a player icon, causing some harmless glitches to the Battle Game scoreboard or the Config Mode interface.
  - He uses Bomberman's portrait in menus, and Bomberman's sprite for the Score Board.
  - If he gets a solo victory, the **game will crash** as he doesn't have a "shout out" voice clip.

### Palettes
```
$00–$07 - Bomberman
  Color Schemes: White, White, Black, Red, Blue, Green, Gold, Burning

$08–$0f - Bomber Woof                   $10–$17 - Dave Bomber
$18–$1f - Gary Bomber                   $20–$27 - Pirate Bomber
$28–$2f - Muscle Bomber                 $30–$37 - Iron Mask Bomber
$38–$3f - Baron Bombano                 $40–$47 - Plunder Bomber
$48–$4f - Subordinate Bomber
  Color Schemes: White, Black, Red, Blue, Green, Gold, Burning, Boss Colors

$50–$59 - Random enemy palettes? (Possible junk data.)
```

### Rooeys
```
$00 - Nagurooey (Red)           $01 - Marooey (Green)           $02 - Hanerooey (Pink)
$03 - Gyarooey (Yellow)         $04 - Kerooey (Blue)            $05 - Magicarooey (Purple)
$06 - Warooey (Black)
```

#### Notes
- Warooey, the "boss-only" Rooey, has some quirks:
  - Most of his sprites are there — including unused mine cart sprites.
  - Warooey's jumping sprites exist in ROM but are never called during gameplay.
  - Unlike other Rooeys, he has no special ability. However, he *does* have graphics for a shoulder tackle move in the ROM.

### Rooms
```
$01 - Hudson Logo                       $02 - Title
$03 - Normal Game Menus                 $04 - Battle Game Menus
$05 - Battle Game Scoreboard            $07 - Password
$08 - Game Over                         $09 - Completion Certificate
$0a - Battle Mode Draw Game             $0b - Options
$0c - Debug Level Select*

$0d–$66 - Normal Game Levels            $67–$70 - Normal Game Boss
$74–$a7 - Battle Game Levels

$a8 - Bomber Bowl                       $a9 - Intro Cutscene
$aa - Good Ending                       $ab - Bad Ending
$ac - Battle Game Test (doesn't end)*   $ad - Normal Game Item Test*
$ae - Normal Game Enemy Test*
```

#### Notes
- Values not listed here either lead to a black screen soft-lock, or a broken blue play field where the player dies over and over, but never actually loses any lives.
- Debug menu and room values originally found by Shizi Kekotsike on *The Cutting Room Floor Wiki*.

### Power-Up Bitmask Values
**Increasing** the address by these values gives a player an array of power-ups.

> **Example:**<br>`$00` + `$20` + `$02` + `$08` = `$2a` (Mine Bomb + Kick + Boxing Glove)

```
+$00 - No Power-Ups             +$01 - Remote Bomb              +$02 - Kick
+$04 - Power Glove              +$08 - Boxing Glove             +$10 - Pierce Bomb
+$20 - Mine Bomb                +$40 - Search Bomb              +$80 - Not Used
```

### Pass Item Bitmask Values
**Decrementing** the address (which typically starts at `$e0`) by these values will give a player the listed abilities.

> **Example:**<br>`$e0` - `$20` - `$40` = `$80` (Soft + Bomb Pass)

```
-$00 - No Pass Items                    -$20 - Soft Block Pass
-$40 - Bomb Pass                        -$80 - Hard Block Pass (Unused; for debugging?)
```
