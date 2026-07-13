# *Final Fantasy Mystic Quest* (W) - Values Appendix
All of the RAM values observed in *Final Fantasy Mystic Quest* (Super NES, World).

All values are **8-bit** unless otherwise noted.<br>Multi-byte values are listed in **little-endian order**.

## Item Types
```
$FF = Nothing
```

### Quest Items
```
$00 = Elixir            $01 = Tree Wither       $02 = Wakewater
$03 = Venus Key         $04 = Multi-Key         $05 = Mask
$06 = Magic Mirror      $07 = Thunder Rock      $08 = Captain Cap
$09 = Libra Crest       $0A = Gemini Crest      $0B = Mobius Crest
$0C = Sand Coin         $0D = River Coin        $0E = Sun Coin
$0F = Sky Coin
```

### Usable Items
```
$10 = Cure Potion                       $11 = Heal Potion       
$12 = Seed                              $13 = Refresher
```

### Magic Tomes
```
$14 = Exit      $15 = Cure      $16 = Heal      $17 = Life
$18 = Quake     $19 = Blizzard  $1A = Fire      $1B = Aero
$1C = Thunder   $1D = White     $1E = Meteor    $1F = Flare
```

### Weapons
```
$20 = Steel Sword       $21 = Knight Sword      $22 = Excalibur
$23 = Axe               $24 = Battle Axe        $25 = Giant's Axe
$26 = Cat Claw          $27 = Charm Claw        $28 = Dragon Claw
$29 = Bomb              $2A = Jumbo Bomb        $2B = Mega Grenade
$2C = Morning Star      $2D = Bow of Grace      $2E = Ninja Star
```

### Armor
```
$2F = Steel Helm        $30 = Moon Helm         $31 = Apollo Helm
$32 = Steel Armor       $33 = Noble Armor       $34 = Gaia's Armor
$35 = Relica Armor      $36 = Mystic Robe       $37 = Flame Armor
$38 = Black Robe        $39 = Steel Shield      $3A = Venus Shield
$3B = Aegis Shield      $3C = Ether Shield      $3D = Charm
$3E = Magic Ring        $3F = Cupid Locket
```

## Quest Item Bitmask Values (16-bit)
```
$0000 = None

$0100 = Thunder Rock    $0200 = Magic Mirror    $0400 = Mask
$0800 = Multi-Key       $1000 = Venus Key       $2000 = Wakewater
$4000 = Tree Wither     $8000 = Elixir

$0001 = Sky Coin        $0002 = Sun Coin        $0004 = River Coin
$0008 = Sand Coin       $0010 = Mobius Crest    $0020 = Gemini Crest
$0040 = Libra Crest     $0080 = Captain Cap
```

## Character Stats
### Status Ailments Bitmask Values
```
+$00 = Normal           +$01 = Silence          +$02 = Blind
+$04 = Poison           +$08 = Confusion        +$10 = Sleep
+$20 = Paralyze         +$40 = Petrify          +$80 = Fatal
```

### Owned Weapons Bitmask Values (16-bit)
```
$0000 = None

$0100 = Charm Claw      $0200 = Cat Claw        $0400 = Giant's Axe
$0800 = Battle Axe      $1000 = Axe             $2000 = Excalibur
$4000 = Knight Sword    $8000 = Steel Sword

$0010 = Mega Grenade    $0020 = Jumbo Bomb      $0040 = Bomb
$0080 = Dragon Claw
```

### Owned Armor Bitmask Values (24-bit)
```
$000000 = None

$040000 = Gaia's Armor  $080000 = Noble Armor   $100000 = Steel Armor
$200000 = Apollo Helm   $400000 = Moon Helm     $800000 = Steel Helm

$000100 = Magic Ring    $000200 = Charm
$000800 = Aegis Shield  $001000 = Venus Shield  $002000 = Steel Shield

$000080 = Cupid Charm
```

### Which Companion? (Companion-Only, 4-bit)
```
$0 = Benjamin
$1 = Kaeli      $2 = Tristan    $3 = Phoebe     $4 = Reuben
$5 = Kaeli 2    $6 = Tristan 2  $7 = Phoebe 2   $8 = Reuben 2
```

### Companion Equipment (4-bit)
#### Helmet
```
    Nothing = $0, $1
Apollo Helm = $2, $3, $6, $7, $A, $B, $E, $F
  Moon Helm = $4, $5, $C, $D
 Steel Helm = $8, $9
```

#### Armor
```
     Nothing = $0
 Mystic Robe = $1, $3
Relica Armor = $2
  Black Robe = $4, $5, $6, $7, $C, $D, $E, $F
 Flame Armor = $8, $9, $A, $B
```

#### Shield
```
     Nothing = $0
Venus Shield = $1, $3
Steel Shield = $2
Ether Shield = $4, $5, $6, $7, $C, $D, $E, $F
Aegis Shield = $8, $9, $A, $B
```

#### Accessory
```
   Nothing = $0, $4, $8, $C
Magic Ring = $1, $3, $5, $7, $9, $B, $D, $F
     Charm = $2, $6, $A, $E
```

### Held Magic Tomes Bitmask Values (16-bit)
```
+$0000 = None

+$0100 = Aero   +$0200 = Fire   +$0400 = Blizz. +$0800 = Quake
+$1000 = Life   +$2000 = Heal   +$4000 = Cure   +$8000 = Exit

+$0010 = Flare  +$0020 = Meteor +$0040 = White  +$0080 = Thunder
```

## Value Notes
### Item Types
- The only items which are *actually* usable are `$10–$13`, but any item can be placed into a Usable Item slot.
- If all four usable item slots have non-usable items and the player opens an item chest, the game will write the information to the next value pair in line: the Quest Items address.
  - Due to bit math rounding, this results in the Quest Items value becoming `$1002`, erasing all items except the Venus Key and Sun Coin.
- Weapon values `$2C–$2E` are equippable only by companion characters. If forced into the player, they have no overworld functionality, but work fine in combat.
- Armor values `$35–38` and `$3C` are equippable only by companion characters.
- When "equipped" by a companion character, Magic Tomes show a proper attack / defense power and grant resistance to the appropriate elements.
- Equipping a Magic Tome as a weapon on either character is not advised as it will crash the game if used in combat.

### Character Stats
- Only Silence, Blind, and Poison linger outside of battle. All other ailments heal after combat.
- While ailments *can* be stacked, only the top-most ailment will show.
> **Example:** Confusion (`$08`) + Blind (`$02`) + Petrify (`$20`) = Just Petrify
- All ailments are cured after a revival from Fatal (`$80`) status.
- I have no idea why the Owned Armor value uses *three* bytes and in such a weird manner.
- Benjamin (`$0`) as a companion character goes completely unused in the game.
- The duplicate companions ("Kaeli 2" (`$5`), for example) are used when a companion rejoins the player later on. There is no difference between either version that I can tell.
- The duplicated Companion Equipment values appear to follow a consistent pattern, suggesting they are decoded rather than stored as simple item IDs. The exact logic behind this encoding remains unknown.