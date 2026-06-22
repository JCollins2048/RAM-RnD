# *Cave Story MD* (Homebrew) RAM Addresses
RAM addresses and values in *[Cave Story MD](https://github.com/andwn/cave-story-md)* (Mega Drive, Homebrew).

Addresses are listed as WRAM offsets.<br> To obtain the corresponding Mega Drive address, add `$FF0000`.
> **Example:**<br> 0x00A0 → $FF00A0

All values are 8-bit unless otherwise stated.

## Player Status
### Weaponry (`0x0C` bytes each)
```
0x00A0 - Slot 1         0x00AC - Slot 2         0x00B8 - Slot 3
0x00C4 - Slot 4         0x00D0 - Slot 5
```

#### Byte Layout (`0x01` byte each)
```
+0x00: Experience       +0x04: Maximum Ammo     +0x06: Current Ammo
+0x08: Level            +0x09: Weapon Type
```

### Inventory (16-bit Words)
```
0x5788 - Items 1–2      0x578A - Items 3–4      0x578C - Items 5–6
0x578E - Items 7–8      0x5790 - Items 9–10     0x5792 - Items 11–12
0x5794 - Items 13–14    0x5796 - Items 15–16    0x5798 - Items 17–18
0x579A - Items 19–20    0x579C - Items 21–22    0x579E - Items 23–24
```

### Other Values
```
0X028D - I-Frames                       0X084B - Air
0X12B4 - Current Health                 0X57AE - Maximum Health
```

### Notes
#### Weaponry
- Offsets are applied in order: Weapon Slot → Field.
> **Example:**<br> Value `0x00B8` (Slot 3)<br>+ Offset `0x09` (Weapon Type)<br>= `0x00C1` (Weapon 3 Type)
- Some weapons "function" at levels below or beyond the expected ones:
  - Fireball (`$03`): Fires a single Level 3 Fireball that does 0 damage.
  - Machine Gun (`$04`): Fires large bullets that do 0 damage.
  - Missile Launcher (`$05`): Launches a missile that freezes in place. If an enemy hits it, dust covers the entire screen for 255 (`$FF`) frames, and a normal-sized hitbox lingers for that amount of time. This can be a *boss shredder*.
  - Super Missile (`$0A`): Fires a normal missile that does 6 damage instead of 5.
  - Nemesis (`$0C`): Fires a Level 3 projectile that sits still, but does the expected damage.
  - Spur (`$0D`): Functions normally, as it doesn't use Exp.
- If the Super / Missile Launcher is set to have 0 Maximum Ammo, then it will have unlimited ammo.
- The Bubbler will always set the Maximum Ammo counter to 100. The Machine Gun won't, but it still has a maximum of 100 ammo.

#### Inventory
- Each address contains two item values in big endian format.
> **Example:**<br>`0x5790` (hi byte) = Item 10<br>`0x5791` (lo byte) = Item 9

#### Other Values
- Setting "I-Frames" to any even value may cause the player character to vanish and be unable to turn around.
- Freezing "Air" to any value other than 100 (`$64`) will constantly display the Air Gauge.
- Using values beyond 99 (`$63`) for Current Health will cause the game to display non-numeric characters as the tens digit. This is because the HUD counter for that value only goes up to 99.

## Game Values
### Time Played
```
0x00E2 - Hours
0x00E4 - Minutes + Seconds (16-bit word)
0x00E7 - Frames
```

## Expected Value Ranges
### Player Status
#### Weaponry
```
Experience: $00–$A6                     Weapon Level: $01–$03
Maximum Ammo: $00–$63                   Current Ammo: $00–$63
Weapon Type: $00–$05, $07, $09–$0A, $0C–$0D
```

### Game Values
#### Time Played
```
Hours: $00–$FF
Minutes + Seconds: $0000–$3B3B
Frames: $00–$3B
```

### Other Values
```
Item: $00–$27
I-Frames: $00–$64                       Air: $00–$64
Current Health: $03–$37                 Maximum Health: $03–$37
```

### Notes
- If the Hours counter exceeds 99 (`$63`), the game will display non-numeric characters as the tens digit on the save screen. This is because the HUD counter for that value only goes up to 99.
- The frame counter runs at 60 frames-per-second in NTSC mode regardless of the *Cave Story+* speed setting.

## Values
### Weapon Types
```
$00 - No weapon.        $01 - Snake             $02 - Polar Star
$03 - Fireball          $04 - Machine Gun       $05 - Missile Launcher
$07 - Bubbler           $09 - Blade             $0A - Super Missile
$0C - Nemesis           $0D - Spur
```

### Items
```
$00 - No item.          $01 - Arthur's Key      $02 - Map System
$03 - Santa's Key       $04 - Silver Locket     $05 - Beast Fang
$06 - Life Capsule      $07 - ID Card           $08 - Jellyfish Juice
$09 - Rusty Key         $0A - Gum Key           $0B - Gum Base
$0C - Charcoal          $0D - Explosive         $0E - Puppy
$0F - Life Pot          $10 - Cure-All          $11 - Clinic Key
$12 - Booster v0.8      $13 - Arms Barrier      $14 - Turbocharger
$15 - Curly's Air Tank  $16 - Nikumaru Counter  $17 - Booster v2.0
$18 - Mimiga Mask       $19 - Teleporter Key    $1A - Sue's Letter
$1B - Controller        $1C - Broken Sprinkler  $1D - Sprinkler
$1E - Tow Rope          $1F - Clay Figure Medal $20 - Little Man
$21 - Mushroom Badge    $22 - Ma Pignon         $23 - Curly's Underwear
$24 - Alien Medal       $25 - Chaco's Lipstick  $26 - Whimsical Star
$27 - Iron Bond
```

### Value Notes
#### Weapon Types
- There are dummy weapons at `$06`, `$08`, and `$0B` which don't do anything but have unique graphics all the same.
- Values beyond `$0D` will crash the game when fired.

#### Items
- There are several caveats with hacking items into your inventory:
  - Some items require additional flags to become functional or relevant:
    - Example 1: Hacking in the Map System (`$02`) won't give the player access to the map.
    - Example 2: Hacking in the Silver Locket (`$04`) won't progress the story — the item still needs to be physically collected.
  - Equippable items such as the Booster v2.0 (`$17`), or usable items such as the Life Pot (`$0F`), can be used normally.
  - Usable quest items such as Arthur's Key (`$01`) or the Jellyfish Juice (`$08`) function normally.
- The Life Capsule (`$06`) is a dummied-out item and cannot be used.