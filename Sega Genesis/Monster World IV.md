# *Monster World IV* RAM Addresses
RAM addresses and values in *Monster World IV* (Sega Mega Drive, Japan).

Addresses are WRAM offsets and correspond to Sega Genesis address `$FF:0000` (add `$FF0000` to the listed value).

All values are 8-bit unless otherwise stated. Please note: *Monster World IV*'s RAM is heavily organized around the Motorola 68000's 16-bit word boundaries. Many 8-bit values are stored in adjacent byte pairs within 16-bit big-endian words, while larger counters (such as Gold) are stored as multiple 16-bit big-endian words.

For ease of reading, values in this document are organized according to their order in the game interface rather than by ascending memory address.

Lastly, these addresses are valid for both the Japanese original release and the official English releases (including Virtual Console and Genesis Mini versions). They may not apply to fan translations or modified ROM hacks, as these can alter memory layout and data placement.

## Player Stats
### Health
```
0xDA76 - Current Health
0xDA74 - Max. Pink Hearts               0xDA7A - Max. Blue Hearts
```

### Collectables
```
0xDA7C - Life Drops
0xDA7E - Gold (16-bit BE High Word)     0xDA80 - Gold (16-bit BE Low Word)
```

### Other Stats
```
0xDE2B - Pepelogoo Level
```

### Notes
- Pink Hearts are granted by armor via the Endurance stat.
- Blue Hearts are obtained by collecting Life Drops (10 per heart).
- Although the HUD displays two separate heart types (Pink and Blue), the game uses a single underlying Current Health value. The number of filled Pink and Blue Hearts is derived from this value. As Current Health decreases or increases, the HUD distributes filled hearts across Blue Hearts first, then Pink Hearts.

## HUD Animation Counters
```
0xDA87 - Pink Hearts                    0xDA85 - Blue Hearts
0xDA8A - Life Drops
0xDA8C - Gold (16-bit BE High Word)     0xDA8E - Gold (16-bit BE Low Word)
```

### Notes
- These control the visual elements of the HUD. When a relevant stat changes, the corresponding counter will increment or decrement at a fixed rate until it matches the actual value.
- Changing these values manually does not affect the underlying stat and appears to have no lasting effect on gameplay.

## Player Inventory
```
0xDE25 - Sword                  0xDE24 - Shield                 0xDE27 - Armor
0xDAA9 - Have Life Medicine?                                   0xDAE1 - Medicine Slot
0xDE1B - Item Slot 1            0xDE1A - Item Slot 2            0xDE1D - Item Slot 3
…
0xDE22 - Item Slot 10
```

## Expected Value Ranges
### Player Stats
```
Current Health: $00–$1E                 Hearts (Both): $03–$0E
Life Drops: $00–$0A                     Gold (32-bit): $00000000–$000F423F
Pepelogoo Level: $00–$02, $FF
```

### Player Inventory
```
Sword: $00–$07                  Shield: $08–0F                  Armor: $10–14, $17
Have Life Medicine?: $00 = No, $FF = Yes                        Medicine Slot: $1C, $FE
Item Slots: $1B, $1D–$2F
```

### Notes
#### Player Stats
- The player can exceed their current maximum health (Pink and Blue Hearts) without incident, but changing scenes will reset the health to the expected maximum value.
- `$0E` is a hard limit for Blue Hearts — exceeding it causes severe graphical issues.
- Life Drops can exceed `$0a` up to `$FF` if the player has `$0E` Blue Hearts.
- The Gold display uses a fixed 6-digit decimal field, truncating any digits beyond the least significant six places.
> **Example:**<br>If the player has `$FADAC826` (4,208,642,086) gold, the HUD displays 642,086.
- Any Pepelogoo Level value beyond `$02` will disable the Pepelogoo.

#### Player Inventory
- Anything can go into any item slot, but items or the wrong kind of equipment in the equipment slots may lead to strange effects.
- "Debug Armor (Pepe)" (`$17`) can be obtained in-game by avoiding interaction with the Sage of Save in Rapadagna Town, which prevents the event flag at `0xCCCE` from being changed from `$00` to `$40`. After this condition is met, the hidden Magic Merchant NPC in the garden beyond the castle's right-hand wall becomes interactable.
 - The address `0xCCCE` appears to be a generic NPC interaction / event flag ("Have we spoken?" state). Many NPCs use similar flags, but this particular flag uniquely governs the interaction state of the Magic Merchant.
- The "Have Medicine" value is a boolean: `$00` means "no" while anything else means "yes".
 - The Medicine Slot is expected to have Healing Medicine (`$19`) while "Have Medicine" is set to true. 
- Attempting to place anything in the Medicine Slot will only work while in the menu. Leaving and coming back will either empty the slot, or replace the item with Healing Medicine, depending on the "Have Medicine?" boolean.
- The player cannot equip swords, shields, or armor from item slots.
- Using Healing Medicine from an item slot works, but it is not consumed. Instead, it clears the "Have Medicine?" flag (`$00`).

## Values
### Blanks
```
$80–$FF - Empty                 $18–$1A - Blank
```

### Swords
```
$00 - Asha's Sword              $01 - Khan's Sword              $02 - Shah's Sword
$03 - Cyrus's Sword             $04 - Caliph's Sword            $05 - Ishtar's Sword
$06 - Sword of Babel            $07 - Legendary Sword
```

### Shields
```
$08 - Plain Shield              $09 - Flame Shield              $0A - Thunder Shield
$0B - Ice Shield                $0C - Steel Shield              $0D - Rainbow Shield
$0E - Magic Shield              $0F - Legend Shield
```
### Armor
```
$10 - Traveler's Armor          $11 - Warrior's Armor           $12 - Knight's Armor
$13 - Hero's Armor              $14 - Legendary Armor
$15 - Debug Armor               $16 - Debug Armor               $17 - Debug Armor (Pepe)
```

### Usable Items
```
$1B - Herb                      $1C - Healing Medicine          $1D - Magic Lamp
```

### Quest Items
```
$1E - Pepelogoo Egg             $1F - Courage Crystal           $20 - Key
$21 - Bomb                      $22 - Bucket                    $23 - Water Bucket
$24 - Gold Bar                  $25 - Leopard Statue            $26 - Witch Statue
$27 - Desert Turtle Statue      $28 - Horned Owl Statue         $29 - Swallow Statue
$2A - Map                       $2B - Earth Medallion           $2C - Moon Medallion
$2D - Sun Medallion             $2E - Wind Medallion            $2F - Magic Carpet
```

### Value Notes
- There are numerous "blank" slots in the game:
 - Item values `$18–1A` and `$80–FF` are empty inventory slots.
 - Item values `$30–3F` have no icon and display various text strings.
 - Item values `$40–4F` pull random data for icons and display various text strings.
- All Debug Armors give +15 Endurance, just like the Legendary Armor.
- The third Debug Armor has a debugging text string that will allow the player to instantly raise their Pepelogoo to Level 1, 2, or 3. There is no option to get rid of it entirely.