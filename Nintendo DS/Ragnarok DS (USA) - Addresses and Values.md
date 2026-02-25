# *Ragnarök DS* (USA) RAM Addresses
RAM addresses and values observed in *Ragnarök DS* (Nintendo DS, USA).

Addresses are WRAM offsets and correspond to Nintendo DS address `$20:xxxxxx` (add `$2000000` to the listed value).

All values are **8-bit** unless otherwise noted.<br>Multi-byte values (**16-bit or higher**) are stored in **little-endian** format: least significant byte first, most significant byte last.

##Addresses
### Equipment
```
Addresses (0x38 bytes each):
  0x0020F9E0 - Ales               0x0020FA18 - Sierra             0x0020FA50 - Lucifi
  0x0020FA88 - Viselc             0x0020FAC0 - Lisir

  0x0020FAF8 - Recruit 6          0x0020FB30 - Recruit 7          0x0020FB68 - Recruit 8
  0x0020FBA0 - Recruit 9          0x0020FBD8 - Recruit 10         0x0020FC10 - Recruit 11
  0x0020FC48 - Recruit 12         0x0020FC80 - Recruit 13         0x0020FCB8 - Recruit 14
  0x0020FCF0 - Recruit 15         0x0020FD28 - Recruit 16

Byte Values Within Each Range:
  Slots (Base Offsets):
    +0x00: Main Hand                +0x07: Off Hand                 +0x0E: Hat
    +0x15: Armor                    +0x1C: Cape                     +0x23: Shoes
    +0x2A: Accessory 1              +0x31: Accessory 2

  Equipment Slot Layout (7 bytes each)
    +0x00: Category                 +0x01: Sub–Type                 +0x02: Refinement Lv.
    +0x03–0x06: Cards (4 bytes)
  
Expected Value Ranges per Byte:
    Main Hand: $03–$0E, $00–$90      Off Hand: $03–$10, $00–$90     Hat: $11, $00–$3C
        Armor: $12, $00–$35              Cape: $13, $00–$10       Shoes: $14, $00–$10
  Accessory 1: $15, $00–$31       Accessory 2: $15, $00–$31
  
   Refinement: $00–$03              Cards: $00–$41 or $fe–$ff
```

#### Notes
- Only **Weapons** can naturally use all four Card Slot bytes. Arrows have no Card Slots, and everything else is limited to **2 bytes**.
- If a piece of equipment has X amount of Card Slots, any Cards modded onto it beyond that limit **will work normally**, despite not being visible. This applies for weapons *and* armor.
- **Thieves, Archers, and Hunters** can equip Arrows to their off hand, and **Assassins** can equip Short Swords, 1H Swords, and 1H Axes, which is why the Off Hand ranges are larger.

- Refinement Levels come with some quirks:
  - Refinement levels above 3 will not display correctly on menus.
  - Giving a **weapon** a Refinement level beyond 3 will **overflow it** into the next weapon level refinement bonus set. For example, a Knife is a "Tier 1" weapon. Increasing the Refinement Level to 4-7 give it Tier 2 Refinement bonuses, 8-11 Tier 3, and 12-15 Tier 4. 16 onward doesn't do much other than confusing the game.
  - Giving **armor** a Refinement level beyond 3 will work normally, **giving it +1 defense** for every Refinement level.
  - Giving an **Arrow** a Refinement Level does nothing, but giving an **Accessory** a Refinement Level increases its Defense by 1.

- Some Expected Value Ranges per Byte are fixed values. This is because the game only expects one category of equipment to be in that slot. (`$11` for Hats, `$15` for Accessories, et cetera.)

### Character Stats and Customization
```
Addresses (0x1F4 bytes each):
  0x00211316 - Ales               0x0021154E - Sierra             0x00211786 - Lucifi
  0x002119BE - Viselc             0x00211BF6 - Lisir

  0x00211E2E - Recruit 6          0x00212066 - Recruit 7          0x0021229E - Recruit 8
  0x002124D6 - Recruit 9          0x0021270E - Recruit 10         0x00212946 - Recruit 11
  0x00212B7E - Recruit 12         0x00212DB6 - Recruit 13         0x00212FEE - Recruit 14
  0x00213226 - Recruit 15         0x0021345E - Recruit 16

Byte Values Within Each Range:
  +0x0000 - Relation Lv. (16-bit)         +0x0013 - Base Lv.
  +0x0014 - Job Lv.

  +0x0016 - Current HP (16-bit)           +0x001A - Max HP (16-bit)
  +0x001E - Current SP (16-bit)           +0x0022 - Max SP (16-bit)
  +0x0026 - Base Exp. (24-bit)            +0x002A - Job Exp. (24-bit)
  +0x0032 - Strength (16-bit)             +0x0034 - Intelligence (16-bit)
  +0x0036 - Vitality (16-bit)             +0x0038 - Agility (16-bit)
  +0x003A - Dexterity (16-bit)            +0x003C - Luck (16-bit)

  +0x007A - Skill 1 Type                  +0x007F - Skill 1 Rank
  +0x0086 - Skill 2 Type                  +0x008B - Skill 2 Rank
  +0x0092 - Skill 3 Type                  +0x0097 - Skill 3 Rank
    … (each skill entry is 0x0C bytes apart)
  +0x01A6 - Skill 26                      +0x01AB - Skill 26 Rank

  +0x01B6 - Job + Gender                  +0x01BA - Hair Style
  +0x01BE - Hair Color                    +0x01DA - Trait
  +0x01E2 - Recruited?                    +0x01E6 - # of Skills
  +0x01E7 - Name (14 bytes)

Expected Value Ranges per Byte:
  Relation Lv.: $012c–$03E8                   Base Lv.: $01–$63
       Job Lv.: $01–$32             
                                    
    Current HP: $0100–$270F                     Max HP: $0100–$270F
    Current SP: $0100–$270F                     Max SP: $0100–$270F
     Base Exp.: $000000–$3D7B0D               Job Exp.: $000000–$0CA95F
      Strength: $01–$63                   Intelligence: $01–$63
      Vitality: $01–$63                        Agility: $01–$63
     Dexterity: $01–$63                           Luck: $01–$63
                                    
    Skill Type: $00–$b7                     Skill Rank: $01–$08
                                    
  Job + Gender: $00–$21                           Hair: $00–$16
    Hair Color: $00–$07                          Trait: $00–$0A, $0B (-- (Ales))
    Recruited?: $00, $01                   # of Skills: $00–$18
          Name: $20–$5A, $61–$6D
```

#### Notes
- Since Ales is never meant to leave your party, it's generally not possible to edit him through the Guild Stats and Customization. However, It *can* be done by forcibly swapping him out, making edits, and putting him back.
  - Changing Ales' **hair** and **job** through memory editing works as expected, but changing his **gender** will **crash the game**. No other character is hard-locked to their default gender or even Job.

### Other Addresses
```
0x001eb9e0 - Party Slot Map (24-bit)    0x001eb9e3 - Previous Party Slot Map (24-bit)
  Expected Value Range for Each Byte: $00–$0F, $FF (Empty)

0x001ecfa4 - Mirage Tower Name (14 bytes)
  Expected Value Range for Each Byte: $30–$7D

0x001ecfbf - Mirage Tower Appearance (24-bit)
  Expected Value Ranges:
    +0x00 - Gender: $00–$01               +0x01 - Hair Style: $00–$16
    +0x02 - Hair Color: $00–$07

0x0020f078 - Zeny (32-bit)
  Expected Value Range: $00000000–$3B9AC9FF

0x0022de08 - Status Points (16-bit)     0x0023d4a2 - Skill Points (8-bit)
  Expected Value Range: $0000–$03E7       Expected Value Range: $00–$59
```

#### Notes
- The **Party Slot Map** does *not* directly change your active party. Instead, it determines which **Guild Roster slots** your current party members occupy when exiting the Party Formation menu.
  - When you exit the menu, the value updates to reflect the selected roster slots.
    - Example: Selecting characters 2 and 3 results in `$020100` (little-endian).
  - If this value is modified externally and you re-enter the Party Formation menu, your current party members will be **cloned** into the specified roster slots.
    - Example: Changing the value to `$0f0900` will clone the current party members into roster slots 16 and 9.
  - Attempting to duplicate Ales (`$00`) is not advised. His clone behaves as Player 2 or Player 3 and will not act.
  - Attempting to override Ales with another character is also not advised and may cause crashes upon leaving town.
  - Modifying this value and leaving town without reopening the Party Formation menu will generally crash the game.
  - Replacing Ales can lead to save corruption, memory instability, or crashes. Do not save with the game in this state.

- The **Previous Party Slot Map** stores a copy of the Party Slot Map when entering the Mirage Tower. After completing the challenge, this value is restored.
  - Unlike the Party Slot Map, modifying this value *does* affect the party composition after a Mirage Tower challenge.
  - This can be used to temporarily replace Ales; however, he will return when the world "reloads" (shops, town, warping).
  - Replacing Ales through this method may still result in save corruption or crashes. Again, do not save with the game in this state.

- For Mirage Tower Appearance data, Hair Style `$16` appears to be unused and cannot normally be unlocked.

## Values
### Equipment Category
```
$03 - Short Sword       $04 - 1H Sword          $05 - 2H Sword
$06 - 1H Spear          $07 - 2H Spear          $08 - 1H Axe
$09 - 2H Axe            $0a - Club              $0b - Rod
$0c - Bow               $0d - Katar             $0e - Book
$0f - Arrow             $10 - Shield            $11 - Hat
$12 - Armor             $13 - Cape              $14 - Shoes
$15 - Accessory
```

### Equipment Sub-Type Ranges
```
$00–$90 - Short Sword   $00–$81 - 1H Sword      $00–$40 - 2H Sword
$00–$27 - 1H Spear      $00–$40 - 2H Spear      $00–$18 - 1H Axe
$00–$36 - 2H Axe        $00–$4F - Club          $00–$31 - Rod
$00–$40 - Bow           $00–$40 - Katar         $00–$3B - Book

$00–$13 - Arrow         $00–$09 - Shield

$00–$3C - Hat           $00–$35 - Armor         $00–$10 - Cape
$00–$10 - Shoes         $00–$31 - Accessory
```

### Job and Gender
#### Male Characters
```
$00 - Novice            $01 - Swordsman         $02 - Magician
$03 - Archer            $04 - Acolyte           $05 - Thief
$06 - Merchant          $07 - Taekwon Kid       $08 - Knight
$09 - Wizard            $0A - Hunter            $0B - Priest
$0C - Assassin          $0D - Blacksmith        $0E - Taekwon Master
$0F - Shaman            $10 - Dark Knight
```

#### Female Characters
```
$11 - Novice            $12 - Swordsman         $13 - Magician
$14 - Archer            $15 - Acolyte           $16 - Thief
$17 - Merchant          $18 - Taekwon Kid       $19 - Knight
$1a - Wizard            $1b - Hunter            $1c - Priest
$1d - Assassin          $1e - Blacksmith        $1f - Taekwon Master
$20 - Shaman            $21 - Dark Knight
```

### Notes
- For specific item, skill, card values, value notes, please refer to **Ragnarok DS (W) - Value Appendixes.md*.
