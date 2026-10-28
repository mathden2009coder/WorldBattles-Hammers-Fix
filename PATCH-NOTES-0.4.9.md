# WorldBattles Hammers 0.4.9 — cooldown gate fix

Video analysis showed a likely source of skipped 3x3 neighbors: the `BlockEvent.BreakEvent` handler rejected new mining events until eight server ticks had elapsed since the previous event. With Efficiency V and fast-breaking blocks, normal center-block breaks can occur inside that window, so vanilla removes only the center block and the 3x3 neighbor queue is never created for that break.

This patch changes only that gate's `ifge` opcode to an unconditional `goto` with the same branch offset and bytecode length. No instruction offsets or stack-map frames are shifted. The original queued 3x3 selection, tool-aware drops, and resources are otherwise preserved.

Checks performed: archive CRC/integrity passed; `javap` successfully disassembled the class and shows the gate now branches directly to the mining logic. Not yet tested in a running Forge 1.20.1 game; verify rapid repeated mining, Fortune, XP, durability, and protection integrations on a backup world.