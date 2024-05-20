# Emerald ACE Codes I have made
## Thumb-ARM Bootstrap (JAP)

Place the sacrifice Pokemon on Box 9, Slot 27 then execute this code.

```arm
mov r1, pc ; 4679
ldr r0, [pc, #0x24] ; 4809 ; Sets r0 to 0x3024
subs r1, r1, r0 ; 1A09 ; Sets r1 to address of Box 9, Slot 27
subs r2, r2, r2 ; 1A92 ; Sets r2 to 0
; 51FF - filler
str r2, [r1] ; 600A  ; The next few opcodes will blank the PID and TID
str r2, [r1, 4] ; 604A
b #4 ; E000
; FFFF - skipped
str r2, [r1, 12] ; 60CA
strh r2, [r1, 16] ; 820A
ldr r0, [pc, 12] ; 4803 ; Loads ARM code to misalign PC
str r0, [r1, 20] ; 6148 ; Stores ARM code in OT
; 51FF - filler
ldr r0, [pc, 16] ; 4804 - Load nickname
str r0, [r1, 8] ; 6088 - Store nickname
bx lr ; 4770
; FFFF
.word 0xE0DF03BE ; E0DF03BE - ldrh r0, [pc], #0x3e, misalign and skip
.word 0x00003024 ; 3024 0000 - Address of box 9
.word 0x4700A000 ; A000 4700 - adr r0, 0, bx r0 - Switch to ARM
```

```text
Box  1: ル ば け ぶ け は ヂ は	[ルばけぶけはヂは]
Box  2: ア こ タ ぼ タ _ l	[アこタぼタ l]
Box  3: P タ こ ェ う ぶ ぶ チ	[Pタこェうぶぶチ]
Box  4: ア え ぶ ギ タ ミ び	[アえぶギタミび]
Box  5: D う k l や ぃ _ _	[Dうklやぃ  ]
Box  6: ア ア ア _ ッ _ び	[アアア ッ び]

79 46 09 48 09 1A 92 1A FF 
51 0A 60 4A 60 00 E0 FF FF 
CA 60 0A 82 03 48 48 61 FF 
51 04 48 88 60 70 47 FF FF 
BE 03 DF E0 24 30 00 00 FF 
51 51 51 00 A0 00 47 FF FF 
```
