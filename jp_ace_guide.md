# Some Guide on Getting 0x085F

## 1. Prerequisites

- Know how to do a single corruption (Glitzer Popping)
- Have the trade Pokemon Dots and Pluses
- All slots from Box 11, Slot 25 must not contain any Pokemon data

## 2. Getting a 0x0615 Egg

Give Dots 21HP/6Atk in EVs, this will allow it to become 0x0615 during corruption. If you want to make the process of counting EVs easier, do not equip Dots with a Macho Brace or let it have Pokerus, they will mess up your EV count.

Perform a single corruption using your favourite method and make sure the Dots is PID corrupted. You can tell if it is PID corrupted if it is in a Nest Ball and it has Pokerus.

## 3. Getting 0x085F

Name Boxes 1 to 7 the following:

```text
Box  1: 4 へ U n い し ッ o	[4へUnいしッo]
Box  2: _ _ _ / _ m m _	[   / mm ]
Box  3: _ _ く し ッ o _ _	[  くしッo  ]
Box  4: _ ソ _ ィ n _ _ _	[ ソ ィn   ]
Box  5: / _ G m D _ G m	[/ GmD Gm]
Box  6: _ _ _ い _ ま q た	[   い まqた]
Box  7: ぁ m ぅ コ く く _ _	[ぁmぅコくく  ]
```

**Read this if you are using an emulator that is not mGBA 0.9.0+**

There is a well known issue where box name codes does not work as it does on console. To fix this make the following changes to the box names:
- `/` --> `B` in Box 2
- `い` --> `_` in Box 6

Then hatch the 0x0615 egg and check Box 10, Slot 19. There should be a glitch Pokemon with species name `あ*` with * representing the new line character. To make sure that we actually have the correct Pokemon, change the name of Box 1 to ` ぶ びぅコくく` and view the summary. If you are brought back to the overworld, you have the correct Pokemon.

## 4. Congratulations

You have 0x085F now, here are some things to know.

You can dispose of 0x0615, the safest way to do it is to place it at the front of the party, enter the PC in deposit mode and release it from there.

You can run codes created by the Japanese glitchers (if you know where to find them), or you can use most of the codes found in Sleipnir17's [Pastebin](https://pastebin.com/u/Sleipnir17).

## Troubleshooting

### I found out the box names are wrong, what to do?

Luckily 0x0615 can be reused but you need to view its summary by viewing another Pokemon's, switching to the statistics page and then switch to 0x0615's page, the code should still execute properly.

### The game crashed! 

If you are on mGBA 0.9.0+ or on console, you have most definitely got the box names (more likely) or the Pokemon wrong. If you are on an inaccurate emulator, double check if you replaced the correct characters then check if you made mistakes elsewhere.

For this case, you most likely made a mistake in Box 6 or Box 7's name.

### I did not get the correct Pokemon

If you are on an inaccurate emulator, check if you have replaced the characters. If not, replace them, then check for mistakes elsewhere.

For this case, you most likely made a mistake in Box 3 or Box 4's name.

### GBARunner2/3

ACE does not work on those hypervisors (as of June 4th 2024), for reasons I do not know. They are somehow more inaccurate than VBA.

## Bonus: Creating an Thumb-ARM bootstrap

0x085F executes the box names in the Thumb instruction set. That means codes meant for 0x0615/0x6789 will not work without a bootstrap. This is fine for Japanese as most codes in that language (with exception to E-Sh4rk's ACE codes) being written in Thumb. Here is the box name code that will generate a Thumb-ARM bootstrap in Box 9, Slot 27:

```text
Box  1: ル ば か ぶ け は き ッ	[ルばかぶけはきッ]
Box  2: _ ざ N わ G _ l _	[ ざNわG l ]
Box  3: ザ タ R タ ミ び _ _	[ザタRタミび  ]
Box  4: _ ふ ぃ _ _ _ _ _	[ ふぃ     ]
Box  5: ち ッ い ぃ _ び _ _	[ちッいぃ び  ]
Box  6: _ _ _ _ _ _ い _	[      い ]
```

The resulting Pokemon should have the nickname of `ちッいぃ `

Place this in Box 12, Slot 15 and remember to move this to an earlier slot if you want to run Thumb codes.

## Bonus: Generating a stable ARM Pokemon

Don't want to use a bootstrap but you still want to run ARM codes? This code generates 0x6789 in Box 9, Slot 27 which functions largely the same as 0x0615 with the ability to now view its summary normally without crashing.

```
Box  1: ル ば け ぶ け は き ぶ	[ルばけぶけはきぶ]
Box  2: _ お ぼ ィ ね _ l _	[ おぼィね l ]
Box  3: き ぼ こ ィ ぶ ゥ N ゥ	[きぼこィぶゥNゥ]
Box  4: _ ミ び _ _ _ _ _	[ ミび     ]
Box  5: グ ヌ _ _ つ ぃ _ _	[グヌ  つぃ  ]
Box  6: _ _ _ _ い _ _ _	[    い   ]
```
