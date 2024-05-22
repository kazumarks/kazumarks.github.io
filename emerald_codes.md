# Emerald ACE Codes I have made

Most are for Japanese as that language is easier to write ACE codes for

## Thumb-ARM Bootstrap (JAP)

Name any Pokemon \[ちッいぃ␣\] then write these box names and execute.

```text
Box  1: ル ば ギ ゲ け は _ み	[ルばギゲけは み]
Box  2: ア く タ ぶ タ _ l	[アくタぶタ l]
Box  3: び み ぶ モ ミ び や ぃ	[びみぶモミびやぃ]

79 46 88 8A 09 1A 00 20 FF 
51 08 60 48 60 00 E0 FF FF 
47 20 48 73 70 47 24 30 FF
```
How does the setup code works:

```arm
mov r1, pc ; 4679
ldrh r0, [r1, #0x14] ; 8A88 ; Sets r0 to 0x3024
subs r1, r1, r0 ; 1A09 ; Sets r1 to address of Box 9, Slot 27
mov r0, 0 ; 2000 ; Sets r0 to 0
; 51FF - filler
str r0, [r1] ; 6008  ; PID = 0
str r0, [r1, #0x4] ; 6048 ; OTID = 0
b #4 ; E000
; FFFF - skipped
mov r0, #0x47 ; 2047
strb r0, [r1, #0xD] ; 7348 ; Complete bootstrap nickname 
bx lr ; 4770
.halfword 0x3024
```

How does bootstrap nickname work \[ちッいぃ␣び\]:
```
add r0, pc, #0x44 ; A011 @ Store address of next word of next box slot
add r0, #0x2 ; 3002 @ Misaligns PC, essential for console ARM codes
bx r0 ; 4700 @ Jump to next box slot and switch to ARM
```
## Create EGG from Nothing

```text
Box  1: ル ば す ぶ け は こ ぶ	[ルばすぶけはこぶ]
Box  2: ア き ぼ ィ ね _ l	[アきぼィね l]
Box  3: か め ぼ ミ N ゥ け ぼ	[かめぼミNゥけぼ]
Box  4: ア こ ガ ィ ね _ l	[アこガィね l]
Box  5: ぶ ゥ ミ び $ $ _ _	[ぶゥミび$$  ]
Box  6: ア ア ア ￥ ￥ _ _	[アアア￥￥  ]
Box  7: ア ア つ ぃ _ _	[アアつぃ  ]
Box  8: ア _ ぞ _ _	[ア ぞ  ]
```

$ = (ZZ)(zz)\
￥  = (YY)(yy)

```arm
mov r1,pc
ldr r0,[pc,#52]
subs r1,r1,r0 ; Set r1 to address of Box 9, Slot 27
ldr r0,[pc, #40] ; Load YYyy
ldr r2,[pc, #28] ; Load ZZzz
adds r0,r0,r2 ; Calculate species number
b 4
movs r2, #6 ; isEgg = true, isSpecies = true
strb r2,[r1,#1] ; Store isEgg and isSpecies flag
strh r0,[r1,#0xE] ; Store species
ldr r2, [pc,#36] ; Load substructure egg flag
strh r2, [r1,#56] ; Store egg flag in substructure
b 4
adds r0, r0, r2 ; (species + 0x4000) = final checksum
strh r0,[r1,#0xA] ; store final checksum, ignore upper 16 bits of final checksum
bx lr
```
