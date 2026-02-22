# Super Bomberman 5 RAM Values
RAM values observed in Super Bomberman 5 (SNES).

Addresses are WRAM offsets and correspond to SNES address `$7E:xxxx` (add `$7E0000` to the listed value).

All values are 8-bit unless otherwise noted.

---

- `0x001031` - Current Room (includes cutscenes and menus)
- `0x0016c2` - P1 Character ($00 - $09)
- `0x0016c3` - P2 Character
- `0x0016c4` - P3 Character (Battle) / P1 Rooey ($00 - $06) / Boss 1 (Vs. Boss)
- `0x0016c5` - P4 Character (Battle) / P2 Rooey / P1 Rooey (Vs. Boss) or Boss 2 (Vs. Boss)
- `0x0016c6` - P5 Character (Battle) / Enemy (Normal Game) / P2 Rooey (Vs. Boss) or P1 Rooey (Vs. Boss)
- `0x0016c7` - P1 Rooey (Battle) / Enemy (Normal Game) / Boss 1 Rooey (Vs. Boss) or P2 Rooey (vs. Boss)
- `0x0016c8` - P2 Rooey (Battle) / Enemy (Normal Game) / Boss 1 Rooey (Vs. Boss)
- `0x0016c9` - P3 Rooey (Battle) / Enemy (Normal Game) / Boss 2 Rooey (Vs. Boss)
- `0x0016ca` - P4 Rooey (Battle) / Enemy (Normal Game)
- `0x0016cb` - P5 Rooey (Battle) / Enemy (Normal Game)
- `0x0016cc` - Enemy (Normal Game)
- `0x0016da` - P1 Palette ($01 - $4f)
- `0x0016db` - P2 Palette
- `0x0016dc` - P3 Palette
- `0x0016dd` - P4 Palette
- `0x0016de` - P5 Palette
- `0x001782` - P1 on Rooey? ($00 - No, $02 - In Transit, $80 - Yes)
- `0x001783` - P2 on Rooey?
- `0x001784` - P3 on Rooey?
- `0x001785` - P4 on Rooey?
- `0x001786` - P5 on Rooey?
- `0x006269` - P1 Controller
- `0x00626a` - P2 Controller
- `0x00626b` - P3 Controller
- `0x00626c` - P4 Controller
- `0x00626d` - P5 Controller

---

### Values
#### Characters
```
  $00 - Bomberman               $01 - Bomber Woof       $02 - Dave Bomber
  $03 - Gary Bomber             $04 - Pirate Bomber     $05 - Muscle Bomber
  $06 - Iron Mask Bomber        $07 - Baron Bombano     $08 - Plunder Bomber
  $09 - Subordinate Bomber
```

#### Rooeys
```
  $00 - Nagurooey (Red)         $01 - Marooey (Green)   $02 - Hanerooey (Pink)
  $03 - Gyarooey (Yellow)       $04 - Kerooey (Blue)    $05 - Magicarooey (Purple)
  $06 - Warooey (Black)
```

#### Palettes
```
  $00 to $07 - Bomberman
  (White, White, Black, Red, Blue, Green, Gold, Burning)

  $08 to $0f - Bomber Woof              $10 to $17 - Dave Bomber
  $18 to $1f - Gary Bomber              $20 to $27 - Pirate Bomber
  $28 to $2f - Muscle Bomber            $30 to $37 - Iron Mask Bomber
  $38 to $3f - Baron Bombano            $40 to $47 - Plunder Bomber
  $48 to $4f - Subordinate Bomber
  (White, Black, Red, Blue, Green, Gold, Burning, Boss)
  $50 to $59 - Random enemy palettes? (Possible junk data.)
```

---

### Notes
#### Character, Rooey, and Boss Addresses
- The character and palette codes work for both players in a Normal Game, but will reset to their expected values at the map screen unless frozen.
  - The character and palette codes work for all players in a Battle Game, but will reset to their expected values at the Score Board unless frozen.
- `0x0016c4` through `0x0016cc` are a sliding data block. Boss character entries occupy the first slots, pushing player Rooey values downward:
  - In a Normal Game, `0x0016c4` and `0x0016c5` are Player 1 and Player 2's Rooey values, and `0x0016c7` through `0x0016cc` are enemy values.
  - In a single-boss fight, `0x0016c4` is the boss character value, `0x0016c5` and `0x0016c6` are Player 1 and Player 2's Rooey values, and `0x0016c7` is Boss 1's Rooey value.
  - In a double-boss fight (Pirate and Subordinate), `0x0016c4` and `0x0016c5` are Boss 1 and Boss 2's character values, and `0x0016c6` and `0x0016c7` are Player 1 and Player 2's Rooey values, respectively. `0x0016c8` is Boss 1's Rooey value.
  - Any untouched values in a boss fight — typically `0x0016c9` through `0x0016cc` — may be used for normal enemies.
    - `0x0016c9` can also store Boss 2's Rooey value, though this goes unused in normal gameplay.
- The "Is on Rooey?" codes work instantly, but may crash the game if not used between level transitions.
- The "Controller" codes **are for Battle Game only**. You cannot make Player 2 computer-controlled in a Normal Game through this method. (I'm not sure it's possible, *period*.)

#### Other Notes
- In normal gameplay, Subordinate Bomber and Warooey are unusable by the player:
  - Subordinate Bomber is fully functional, but causes the scoreboard to harmlessly glitch during a Battle Game.
    - If he gets a solo victory, the game will crash as he doesn't have a "shout out" voice clip.
  - Warooey has no ability, and his jumping graphics are never called when hopping into a mine cart.

    - However, he *does* have graphics for both things in the ROM.
