# Emerald ACE Codes I have made

## Change and freeze PRNG seed

This code has similar limitations to the original ARM version of this code (do not stay on the summary for too long, get into a battle as quick as possible etc.)

Calculate vvVVuuUU, wwWWzzZZ through the same method that Sleipnir17's codes use. Or you can use the version that is available on [E-Sh4rk's Code Generator](https://e-sh4rk.github.io/CodeGenerator)

```text
Box  1: く べ か み く タ く べ	[くべかみくタくべ]
; Use べ from the blue layer
Box  2: _ い み く ミ _ l	[ いみくミ l]
Box  3: き べ く ぶ こ ぼ ィ ね	[きべくぶこぼィね]
; Use べ from the blue layer
Box  4: _ く タ ミ び	[ くタミび]
Box  5: ゾ わ い い ベ ら _ う	[ゾわいいベら う]
; Use べ from the red layer
Box  6: _ _ _ l コ _ う _	[   lコ う ]
Box  7: ア ア * ° § @ _ _	[アア*°§@  ]
; index of *=VV; index of °=vv; index of §=UU; index of @=uu
Box  8: ア * ° § @ _ _ _	[ア*°§@   ]
; index of *=ZZ; index of °=zz; index of §=WW; index of @=ww
```

Some of the comments were directly lifted from the documentation on [E-Sh4rk's Code Generator](https://e-sh4rk.github.io/CodeGenerator/?lang=jap).

```arm-asm
ldr r1, [pc, #0x18] ; 4908 @ r1 = gBattleTypeFlags (0x02022c90)
mov r0, #0x6 ; 2006 @ bit 24,21,20,19,18,17,16 or 1 (LE) of gBattleTypeFlags must be activated
str r0, [r1] ; 6008
ldr r1, [pc, #0x20] ; 4908 @ r1 = inBattle (0x03002799)
mov r0, #0x2 ; 2002 @ bit 1 of inBattle must be activated (but preferably not bit 0 and 2)
strb r0, [r1] ; 7008
b #0x4 ; E000
ldr r1, [pc, #0x1C] ; 4907 @ r1 = PRNG state (0x0x03005AE0)
ldr r0, [pc, #0x20] ; 4808 @ r0 = uuUUvvVV
ldr r2, [pc, #0x28] ; 4A0A @ r2 = wwWWzzZZ
add r0, r0, r2 ; 1880 @ r0 + r2 = xxXXyyYY
str r0, [r1] ; 6008
bx lr ; 4770

.word 0x02022c90
.word 0x03002799
.word 0x03005AE0
```

## Place Any PID in Daycare

Calculate vvVVuuUU, wwWWzzZZ through the same method that Sleipnir17's codes use. You can also generate a code through copying [this](#input-for-e-sh4rk-code-generator) to the code generator.

```text
Box  1: ル ば か ぶ け は き ッ	[ルばかぶけはきッ]
Box  2: _ し N X ね _ l	[ しNXね l]
Box  3: こ タ ミ び _ _ _ _	[こタミび    ]
Box  4: _ く ゾ _ _ _ _ _	[ くゾ     ]
Box  5: * ° § @  \ | ~ >	[*°§@\|~>]
; index of *=VV; index of °=vv; index of §=UU; index of @=uu
; index of \=ZZ; index of |=zz; index of ~=WW; index of >=ww
```

```arm-asm
mov r1, pc ; 4679
ldr r0, [pc, #0x18] ; 4806
sub r1, r1, r0 ; 1A09
add r0, pc, #0x1C ; A007
ldmia r0!, {r2, r3} ; C80C
add r2, r2, r3 ; 18D2
b #4 ; E000
str r2, [r1] ; 600A
bx lr ; 4770
.word 0x00009008
```

## Thumb-ARM Bootstrap (JAP)

Name any Pokemon \[ちッいぃ␣\] place it in Box 9, Slot 27 then write these box names and execute.

```text
Box  1: ル ば ギ ゲ け は _ み	[ルばギゲけは み]
Box  2: ア く タ ぶ タ _ l	[アくタぶタ l]
Box  3: び み ぶ モ ミ び や ぃ	[びみぶモミびやぃ]
```

How the setup code works:

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

How the bootstrap nickname works \[ちッいぃ␣び\]:
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
Refer to Sleipnir17's codes on how are yy and zz variables are determined:\
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
{UVdata}
{ZWdata}
    </pre>
</details>

