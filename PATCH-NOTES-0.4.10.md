# WorldBattles Hammers 0.4.10 — filter-preserving cooldown patch

Based on the 0.4.9 test JAR. This patch addresses two confirmed bytecode regressions:

1. The 0.4.9 cooldown edit replaced the conditional branch with `goto`, which left the comparison result on the operand stack. 0.4.10 instead replaces the cooldown constant `8L` with `0L` using a same-length `lconst_0; nop; nop` sequence, leaving `lcmp` and the existing conditional branch intact. This removes the eight-tick gate without changing instruction offsets or stack-map frames.
2. The 0.4.9 neighbor-processing edit replaced the pickaxe-tag and harvestability branches with `pop`/`nop`, allowing dirt and other non-pickaxe blocks to pass. 0.4.10 restores those checks and their existing loop-back targets, so only blocks tagged `mineable/pickaxe` and harvestable by the player are processed by this path.

Validation performed: ZIP CRC test passed; `javap` successfully disassembled the patched class and showed the intended instructions/branches. This is not a live Forge runtime test. Test on a backup world; verify rapid consecutive 3x3 mining, Fortune, XP, durability, and claim/protection behavior.