# *Final Fantasy IV Advance* (USA) RAM Addresses
RAM addresses and values in *Final Fantasy IV Advance* (Game Boy Advance, USA).

Addresses are WRAM offsets. Corresponding Game Boy Advance EWRAM addresses can be obtained by adding `$01FF8000` to the listed value.

All values are **8-bit** unless otherwise noted.<br>Multi-byte values (**16-bit or higher**) are stored in **little-endian** format: least significant byte first, most significant byte last.

## Character Stats (`0x48` Bytes Each)
```
0x00E9F8 - Cecil                0x00EA40 - Kain                 0x00EA88 - Rosa
0x00EAD0 - Rydia                0x00EB18 - Cid                  0x00EB60 - Tellah
0x00EBA8 - Edward               0x00EBF0 - Yang                 0x00EC38 - Palom
0x00EC80 - Porom                0x00ECC8 - Edge                 0x00ED10 - FuSoYa
```

### Byte Values Within Each Range
#### Vitals:
```
+0x00 - Current HP (16-Bit)             +0x02 - Maximum HP (16-Bit)
+0x04 - Current MP (16-Bit)             +0x06 - Maximum MP (16-Bit)
```

#### Identity
```
+0x0A - Job                             +0x0B - Level
```

#### Ability Attributes
```
+0x0C Strength (Temporary)              +0x14 Strength (Permanent)
+0x0D Agility (Temporary)               +0x15 Agility (Permanent)
+0x0E Stamina (Temporary)               +0x16 Stamina (Permanent)
+0x0F Intellect (Temporary)             +0x17 Intellect (Permanent)
+0x10 Spirit (Temporary)                +0x18 Spirit (Permanent)
```

#### Combat Stats
```
+0x19 - Attack (Base)                   +0x1A - Attack (Gear)
+0x1B - Precision
+0x1C - Defense (Base)                  +0x1D - Defense (Gear)
+0x1E - Physical Evasion
+0x1F - Magic Defense (Base)            +0x20 - Magic Defense (Gear)
+0x21 - Magic Evasion
```

#### Equipment
```
+0x24 - Right Hand Item (16-bit)        +0x26 - Right Hand Quantity
+0x28 - Left Hand Item (16-bit)         +0x2A - Left Hand Quantity
+0x2C - Head Item (16-bit)
+0x2E - Body Item (16-Bit)
+0x30 - Arms Item (16-bit)
```

#### Progression
```
+0x40 - Experience (24-bit)
```

#### Expected Value Ranges per Byte
```
HP (Both): $0000–$270F                  MP (Both): $0000–$270F
Job: $00–$0B                            Level: $01–$63

Ability Attributes: $00–$63             Combat Stats: $00–$FF
Equipment: $0000–$4401

Experience: $00000000–$0098967f
```

### Notes
- Unlike in the Super Famicom version, Right / Left Hand Quantity only works with Arrows.
- The Equipment values are 16-bit in this version due to the exclusive additional items.

## Spell Lists (`0x18` bytes each)
### White Magic
```
0x00EDC4 - Paladin              0x00EDDC - White Mage (Rosa)    0x00EDF4 - Summoner (Young)
0x00EE0C - Sage                 0x00EE24 - White Mage (Porom)   0x00EE3C - Lunarian
```

### Black Magic
```
0x00EE54 - Summoner             0x00EE6C - Sage                 0x00EE84 - Black Mage
0x00EE9C - Lunarian
```

### Other Magic
```
0x00EEB4 - Summons (Summoner)   0x00EECC - Ninjitsu (Ninja)
```

### Notes
- If a character is swapped to any of the Jobs listed above, they will learn from the expected spell list.

## Inventory (`0x04` bytes each)
### Party Inventory
```
0x00EEE4 - Item Slot 1          0x00EEE8 - Item Slot 2        0x00EEEC - Item Slot 3
0x00EEF0 - Item Slot 4          0x00EEF4 - Item Slot 5        0x00EEF8 - Item Slot 6
…
0x00EF98 - Item Slot 46         0x00EF9C - Item Slot 47       0x00EFA0 - Item Slot 48
```

### Fat Chocobo Inventory
```
0x00EFA4 - Item Slot 1          0x00EFA8 - Item Slot 2        0x00EFAC - Item Slot 3
0x00EFB0 - Item Slot 4          0x00EFB4 - Item Slot 5        0x00EFB8 - Item Slot 6
…
0x00F198 - Item Slot 126
```

### Byte Values Within Each Range
```
+0x00 - Item Type (16-bit)              +0x02 - Item Quantity (8-bit)
  Expected Value Range: $0000–$4101       Expected Value Range: $00—$FF
```

### Notes
- Byte `0x03` of every item appears to be unused, rather than as part of a 16-bit value.

## Other Addresses
```
0x00E9E6–0x00E9EA - Party Slot 1 to 5
  Expected Value Range: $00—$0B

0x00F2BC - Gil (32-bit)
  Expected Value Range: $00000000—$05F5E0FF
```

## Values
### Items
> *Please refer to [Final Fantasy IV Advance (W) - Items Appendix.md](./Final Fantasy IV Advance (W) - Items Appendix.md)*

### Spells
#### None
```
$00 - Empty
```

#### White Magic
```
$01 - Hold                      $02 - Silence                   $03 - Confuse
$04 - Blink                     $05 - Protect                   $06 - Shell
$07 - Slow                      $08 - Haste                     $09 - Berserk
$0A - Reflect                   $0B - Holy                      $0C - Dispel
$0D - Scan                      $0E - Cure                      $0F - Cura
$10 - Curaga                    $11 - Curaja                    $12 - Esuna
$13 - Life                      $14 - Full-Life                 $15 - Mini
$16 - Teleport                  $17 - Sight                     $18 - Float
```

#### Black Magic
```
$19 - Toad                      $1A - Pig                       $1B - Warp
$1C - Poison                    $1D - Fire                      $1E - Fira
$1F - Firaga                    $20 - Blizzard                  $21 - Blizzara
$22 - Blizzaga                  $23 - Thunder                   $24 - Thundara
$25 - Thundaga                  $26 - Bio                       $27 - Tornado
$28 - Quake                     $29 - Sleep                     $2A - Break
$2B - Death                     $2C - Stop                      $2D - Drain
$2E - Osmose                    $2F - Meteor                    $30 - Flare
```

#### Summon
```
$31 - Goblin                    $32 - Bomb                      $33 - Cockatrice
$34 - Mind Flayer               $35 - Chocobo                   $36 - Shiva
$37 - Ramuh                     $38 - Ifrit                     $39 - Titan
$3A - Dragon                    $3B - Sylph                     $3C - Odin
$3D - Leviathan                 $3E - Asura                     $3F - Bahamut
```

#### Twincast
```
$40 - Comet                     $41 - Pyro
```

#### Ninjitsu:
```
$42 - Flame                     $43 - Flood                     $44 - Blitz
$45 - Smoke                     $46 - Pin                       $47 - Image
```

### Notes
- Any spell-casting Job can use any of these spells if hacked in.
- Both "Comet" (`0x40`) and "Pyro" (`0x41`) have the description "Dummy [Spell]". This is normally impossible to see, as Twincast casts either randomly.
- Entries `0x46` through `0xAD` contain various text strings relating to special skills, Summon abilities, and enemy attacks. However, that's all they are — text strings.
- Everything from `0xAE` onward is just bits of in-game text.

## Jobs
```
$00 - Dark Knight               $01 - Dragoon                   $02 - White Mage (Rosa)
$03 - Summoner (Child)          $04 - Engineer                  $05 - Sage
$06 - Bard                      $07 - Monk                      $08 - Black Mage
$09 - White Mage (Porom)        $0A - Ninja                     $0B - Lunarian
$0C - Paladin                   $0D - Summoner (Adult)          $0E - None (Golbez)
```

### Notes
- "Paladin" (`$0C`) and "Summoner (Adult)" (`$0D`) are set on Cecil and Rydia, respectively, at certain points of the game.
- "None" (`$0E`) appears to be a copy of either Lunarian or Sage:
  - It has the ability to use Black and White Magic, but can never learn any spells.
  - While "None" can't physically equip anything, hovering over anything a Lunarian can equip in shop menus *will* cause the "None" to play its victory / "can equip" animation.

## Party Slots
```
$00 - Cecil                     $01 - Kain                      $02 - Rosa
$03 - Rydia                     $04 - Cid                       $05 - Tellah
$06 - Edward                    $07 - Yang                      $08 - Palom
$09 - Porom                     $0A - Edge                      $0B - FuSoYa
$0E - Golbez
```

### Notes
- Golbez is *technically* playable. However, his "stats" read from the Magic Lists coding, he lacks many necessary sprites, and will crash the game if attacking normally.
- By default, Golbez's Job is `$00` (Dark Knight), but he *does* have his own "Job", listed above. This gives him a proper portrait, but that's about it.